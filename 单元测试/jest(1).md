##Jest 单元测试（一）

Jest既简单又强大，内置支持以下功能：

- 灵活的配置：比如，可以用文件名通配符来检测测试文件。
- 测试的事前步骤(Setup)和事后步骤(Teardown)，同时也包括测试范围。
- 匹配表达式(Matchers)：能使用期望expect句法来验证不同的内容。
- 测试异步代码：支持承诺(promise)数据类型和异步等待async / await功能。
- 模拟函数：可以修改或监查某个函数的行为。
- 手动模拟：测试代码时可以忽略模块的依存关系。
- 虚拟计时：帮助控制时间推移。



###引入 Jest & vue/test-utils

- npm install --save-dev jest @vue/test-utils

```json
// package.json
{
  "scripts": {
    "test": "jest"
  }
}
```

- npm install --save-dev vue-jest

```javascript
// jest.conf.js
module.exports = {
  moduleFileExtensions: ['js', 'json', 'vue'],
  moduleNameMapper: {
    '^@/(.*)$': '<rootDir>/src/$1'   // 别名
  },
  transform: {
    '^.+\\.js$': '<rootDir>/node_modules/babel-jest',
    '.*\\.(vue)$': '<rootDir>/node_modules/vue-jest'
  },
}
```



###执行测试用例

```
// 执行测试用例
vue-cli-service test:unit
// 更新快照文件
npx jest xxx.spec.js -u
```



###Matcher 匹配器 [API](<https://jestjs.io/docs/en/expect.html>)

- 相等匹配
  - 使用 toBe 来比较字符串,数字或布尔值等基本数据类型
  - 使用 toEqual 来比较数组、对象等引用数据类型
  - toBeNull、toBeUndefined、toBeDefined、toBeTruthy、toBeFalsy、.not
- 数字型匹配
  - toBeGreaterThan、toBeGreaterThanOrEqual、toBeLessThan、toBeLessThanOrEqual
  - 需要注意的是对于float类型的浮点数计算的时候，需要使用toBeCloseTo而不是 toEqual ，因为避免细微的四舍五入引起额外的问题
- 字符型匹配
  - 使用 **toMatch**  匹配规则，支持正则表达式匹配
- 数组类型匹配
  - 使用 **toContain** 检查是否包含
- 异常匹配
  - 如果想要测试function是否会抛出特定的异常信息，可以用 **toThrow** 规则。并支持正则匹配。



###测试异步代码

- callback

  ```javascript
  test('callback测试例子', done => {
      const wrapper = mount(Async);
      const doneCallbackSpy = jest.fn(function () {
        console.log('回调函数被执行');
        done();
      });
      wrapper.vm.asyncFun1(doneCallbackSpy);
  })
  ```

- Promise

  ```javascript
  test('promise测试例子', () => {
      const wrapper = mount(Async);
      wrapper.vm.asyncFun2().then(data => {
        expect(data).toBe('nextVal');
      });
  });
  ```

- Async/Await

  ```javascript
  test('Async/Await测试例子', async () => {
      const wrapper = mount(Async);
      const data = await wrapper.vm.fetchData(1);
      expect(data.error.code).toBe(4041);
  });
  ```



### Mock Function 函数模拟器

- 所有的Mock Function都带有 .mock的属性，它保存了此函数被调用的信息。 `.mock` 属性还追踪每次调用时 `this`的值，

  ```javascript
  test('mock function', () => {
      const wrapper = mount(MockFunc);
      const mockCallback = jest.fn();
      wrapper.vm.showAll([0, 1], mockCallback);
      expect(mockCallback.mock.calls.length).toBe(2);
      expect(mockCallback.mock.calls[0][0]).toBe(0);
      expect(mockCallback.mock.calls[1][0]).toBe(1);
    })
  ```

  ```javascript
  // 这个函数只调用一次
  expect(someMockFunction.mock.calls.length).toBe(1);
  
  // 这个函数被第一次调用时的第一个 arg 是 'first arg'
  expect(someMockFunction.mock.calls[0][0]).toBe('first arg');
  
  // 这个函数被第一次调用时的第二个 arg 是 'second arg'
  expect(someMockFunction.mock.calls[0][1]).toBe('second arg');
  
  // 这个函数被实例化两次
  expect(someMockFunction.mock.instances.length).toBe(2);
  
  // 这个函数被第一次实例化返回的对象中，有一个 name 属性，且被设置为了 'test’ 
  expect(someMockFunction.mock.instances[0].name).toEqual('test');
  
  myMock.mockReturnValueOnce(true)
    	  .mockReturnValue(true);
  ```

  

