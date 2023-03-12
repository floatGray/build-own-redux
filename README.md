# build-own-redux
实现整个 redux 里所有的 API

- 实现一个事件总线 + 数据（状态）中心
  - getState 获取数据（状态）
  - dispatch(action) 修改数据（状态）
  - subscribe(listener) 添加修改数据时的监听器，只要 dispatch 所有监听器依次触发
  - replaceReducer 用新 reducer 替换旧 reducer，一般人用不了，忘了吧
  - observable 为了配合 tc39 搞的，准确地说是为了配合 RxJS 搞的。一般人用不起，忘了吧
  - enhancer 传入已有 createStore 一通乱搞后返回增强后的 createStore，最最最常见的 enhancer 为 applyMiddlewares。一般人只会用 applyMiddlewares，记住这个就可以了
- 实现 applyMiddlewares，将一堆中间件通过 compose 组合起来，执行过程为“洋葱圈”模型。其中中间件的作用是为了增强 dispatch，在 dispatch 前后会做一些事情
- 实现 compose，原理为将一堆入参为旧 dispatch，返回新 dispatch 的函数数组，使用 Array.reduce 组合，变成 mid1(mid2(mid3())) 无限套娃的形式
- 实现 combineReducers，主要作用是将多个 reducer 组件成一个新 reducer，执行 dispatch 后，所有 map 里的 reducer 都会被执行。当你用到了多个子状态 Slice 时会用到，别的场景忘了吧
- combineActionCreators，将多个 actionCreators 都执行一遍，并返回 () => dispatch(actionCreator()) 这样的函数。这个直接忘了吧