# 从零到CRUD

## 安装dva-clli并创建应用

安装n
```bash
sudo npm install -g n
```
升级node
```bash
sudo n stable
```
安装dva-cli
```bash
npm i dva-cli@0.7 -g
```
遇到Cannot find module 'internal/fs'问题，从官网下载node重新安装。

创建应用

```bash
dva new user-dashboard
```

## 配置antd和babel-plugin-import

babel-plugin-import 用于按需引入 antd 的 JavaScript 和 CSS，这样打包出来的文件不至于太大。

```bash
$ npm i antd --save
$ npm i babel-plugin-import --save-dev
```

修改 `.roadhogrc`，在 `"extraBabelPlugins"` 里加上：

```
["import", { "libraryName": "antd", "style": "css" }]
```

安装cnpm，使用国内源

```bash
sudo npm install -g cnpm --registry=https://registry.npm.taobao.org
```
修改 `.roadhogrc`，在 `"extraBabelPlugins"` 里加上：

```
["import", { "libraryName": "antd", "style": "css" }]
```

## 配置代理，能通过 RESTFul 的方式访问 

修改 `.roadhogrc`，在`env`后加上 `"proxy"` 配置：

```
"proxy": {
  "/api": {
    "target": "http://jsonplaceholder.typicode.com/",
    "changeOrigin": true,
    "pathRewrite": { "^/api" : "" }
  }
},
```

然后启动应用：(这个命令一直开着，后面不需要重启)

```
$ npm start
```

## 生成 users 路由

用 dva-cli 生成路由：

```
$ dva g route users
```

然后访问 <http://localhost:8000/#/users> 。

## 构造 users model 和 service

用 dva-cli 生成 Model ：

```
$ dva g model users
```

修改 `src/models/users.js` ：

```javascript
import * as usersService from '../services/users';

export default {
  namespace: 'users',
  state: {
    list: [],
    total: null,
  },
  reducers: {
    save(state, { payload: { data: list, total } }) {
      return { ...state, list, total };
    },
  },
  effects: {
    *fetch({ payload: { page } }, { call, put }) {
      const { data, headers } = yield call(usersService.fetch, { page });
      yield put({ type: 'save', payload: { data, total: headers['x-total-count'] } });
    },
  },
  subscriptions: {
    setup({ dispatch, history }) {
      return history.listen(({ pathname, query }) => {
        if (pathname === '/users') {
          dispatch({ type: 'fetch', payload: query });
        }
      });
    },
  },
};
```

新增 `src/services/users.js`：

```javascript
import request from '../utils/request';

export function fetch({ page = 1 }) {
  return request(`/api/users?_page=${page}&_limit=5`);
}
```

由于我们需要从 response headers 中获取 total users 数量，所以需要改造下 `src/utils/request.js`：

```javascript
import fetch from 'dva/fetch';

function checkStatus(response) {
  if (response.status >= 200 && response.status < 300) {
    return response;
  }

  const error = new Error(response.statusText);
  error.response = response;
  throw error;
}

/**
 * Requests a URL, returning a promise.
 *
 * @param  {string} url       The URL we want to request
 * @param  {object} [options] The options we want to pass to "fetch"
 * @return {object}           An object containing either "data" or "err"
 */
export default async function request(url, options) {
  const response = await fetch(url, options);

  checkStatus(response);

  const data = await response.json();

  const ret = {
    data,
    headers: {},
  };

  if (response.headers.get('x-total-count')) {
    ret.headers['x-total-count'] = response.headers.get('x-total-count');
  }

  return ret;
}
```