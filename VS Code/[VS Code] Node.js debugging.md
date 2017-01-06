## node2(Experimental Node.js debugger)
- VS Code는 V8 Inspector Protocol을 사용하여 Node.js를 debug할 수 있는데, 이를 node2라고 한다.
- node2는 Node.js 6.3+ 에서만 사용할 수 있고 --inspect flag를 통해 사용한다.
- node2는 vscode-chrome-debug-core lib에서 실행된다.
- Node.js <6.3 에서는 node debugger를 사용해야 한다. 

### Launch.json Attribute
1.launch or attach에 작성가능한 Attributes
- restart: debugger를 restart하고나면 debugging session이 끝난 지점에서 debugging을 시작할지를 결정
           (true or false)


참조 링크

[ - Node.js Debugging](https://code.visualstudio.com/docs/editor/node-debugging)
