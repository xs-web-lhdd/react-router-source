# 看的都是react-router v6.19.0版本的源码 

记录几个核心的文件：

packages/router/router.ts：这个文件里有createRouter、createStaticHandler等方法，createRouter很关键，createHashRouter、createBrowserRouter、createMemoryRoter内部都是调用的createRouter

packages/router/historty.ts：这个文件里面有createMemoryHistory、createBrowserHistory、createHashHistory、getUrlBasedHistory等方法

- createMemoryHistory内部自己维护了一个数组，来存放location的记录，返回一个histroy对象，支持push、replace、go等方法
- createBrowserHistory、createHashHistory都是通过浏览器的histroy对象进行的操作，支持push、replace、go等方法

packages/router/utils.ts

- matchRoutes：找匹配的路由分支
- flattenRoutes：将路由数组进行扁平化处理
- computeScore：计算路由权值
- rankRouteBranches：通过路由的score排序，比较权重值
- compareIndexes：比较 route 的 index，判断是否为兄弟 route，如果不是则返回 0，比较没有意义，不做任何操作
- matchRouteBranch：通过 branch 和当前的 pathname 得到真正的 matches 数组

packages/router-router-dom/indext.tsx：里面有createHashRouter、createBrowserRouter

- BrowserRouter：基于Router组件包了一层
- HistoryRouter：基于Roter组件包了一层
- HashRouter：基于Router组件包了一层



packages/react-router：

- index.ts：里面有createMemoryRouter，其他两个在router-router-dom的index.tsx中
- lib/components.tsx：
  - MemoryRouter：react-router包里面只有 MemoryRouter，其余的 router（HashRouter、BrowserRouter）在 react-router-dom包里，它内部用到了Router组件
  - createRoutesFromChildren：将 Route 组件转换为 route 对象,提供给 useRoutes 使用
  - renderMatches：内部调用`_renderMatches`进行渲染对应的页面
  - Routes：内部调用useRoutes，根据pathname找到匹配路由组件，然后进行渲染
  - Router：提供渲染的上下文，但是一般不直接使用这个组件，会包装在 BrowserRouter 等二次封装的路由中，Router 的作用就是格式化传入的原始 location 并渲染全局上下文 NavigationContext LocationContext（这两个Context来自隔壁文件context.ts）
  - Route：Route组件内部没有进行任何操作，仅仅只是定义 props，而我们就是为了使用它们的 props
- lib/hook.tsx：里面有很多hooks，useRoutes这个核心hook也在里面
