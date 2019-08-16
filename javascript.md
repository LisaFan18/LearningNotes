
# React
## what
1. [React](https://reactjs.org/) is a Javascript library for building user interfaces. React Native是目前最火的前端技术，它可以做到实时热更新。它是Facebook提供的一套解决方案/前端的UI组件库，它利用JavaScript作为开发语言，可以同时来编写前端，移动终端，后台应用程序。这项技术“Learn Once, Write AnyWhere”
2. 官网 [Online Tutuorial](https://reactjs.org/tutorial/tutorial.html)
3. React 特点：
* React采用JSX的语法， 直接在js的函数里写html的代码, 然后利用专门的工具把它转换为普通的js和html。
 ```javascript
 render() {
   return <div> hello react </div>;
 }
 ```
 * 采用组件化的思想，把能封装的都封装起来。因此用js来封装html，使得html有了面向对象的能力。提高了复用性，不用重复造轮子。
 * React使用虚拟DOM, 规避了原生js操作DOM太频繁的问题，这大大提高了性能。

## set up environment
1. react Developer Tools
* set up Chrome tools for React: go to chrome webstore, search "React Developer Tools", click "add to chrome". 
* inspect React sites: go to https://www.airbnb.com/ , press "cmd + option + j" ; 
2. create-react-app
* by "npm install -g create-react-app", install [Create React App](http://create-react-app.dev/docs/getting-started) is an officially supported way to create single-page React applications. It offers a modern build setup with no configuration.
* [npm](https://www.npmjs.com/) is a package manager for the JavaScript programming language. It is the default package manager for the JavaScript runtime environment Node.js.
* [Node.js](https://nodejs.org/en/)  is an open-source, cross-platform JavaScript run-time environment that executes JavaScript code outside of a browser.
