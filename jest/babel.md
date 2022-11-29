jest를 사용하려고 하던 중 다음과 같은 오류가 났다.

```shell
❯ npm test

> test
> jest

 FAIL  ./middlewares.test.js
  ● Test suite failed to run

    Jest encountered an unexpected token

    Jest failed to parse a file. This happens e.g. when your code or its dependencies use non-standard JavaScript syntax, or when Jest is not configured to support such syntax.

    Out of the box Jest supports Babel, which will be used to transform your files into valid JS based on your Babel configuration.

    By default "node_modules" folder is ignored by transformers.

    Here's what you can do:
     • If you are trying to use ECMAScript Modules, see https://jestjs.io/docs/ecmascript-modules for how to enable it.
     • If you are trying to use TypeScript, see https://jestjs.io/docs/getting-started#using-typescript
     • To have some of your "node_modules" files transformed, you can specify a custom "transformIgnorePatterns" in your config.
     • If you need a custom transformation specify a "transform" option in your config.
     • If you simply want to mock your non-JS modules (e.g. binary assets) you can stub them out with the "moduleNameMapper" config option.

    You'll find more details and examples of these config options in the docs:
    https://jestjs.io/docs/configuration
    For information about custom transformations, see:
    https://jestjs.io/docs/code-transformation

    Details:

    /Users/suyeonpark/project/middlewares.test.js:1
    ({"Object.<anonymous>":function(module,exports,require,__dirname,__filename,jest){import { signup } from './controllers/user';
                                                                                      ^^^^^^

    SyntaxError: Cannot use import statement outside a module

      at Runtime.createScriptFromCode (node_modules/jest-runtime/build/index.js:1449:14)
```

핵심 부분은 `SyntaxError: Cannot use import statement outside a module`인데 test 코드 안에 있는 import를 읽어오지 못했다. 이를 해결한 방법은 다음과 같다. 



1. 나는 yarn이 설치되어 있지 않아 먼저 yarn을 설치해줬다. 아래는 해당 명령어이다.

```shell
sudo npm install yarn --location=global
```



2. 이후 이들을 추가해주었다.

```shell
 yarn add --dev babel-jest @babel/core @babel/preset-env
 yarn add @babel/node @babel/preset-env @babel/core
```



3. `package.json` 에 다음을 추가한다.

```json
  "scripts": {
    "start": "nodemon app",
    "test": "jest",
    "babel": "babel-node"
  }
```



4. 루트 폴더에 `babel.config.js` 파일을 만든다음 아래 내용을 입력해준다.

```javascript
module.exports = {
    "presets": [
        "@babel/preset-env"
    ]
}
```



이렇게 하면 테스트가 정상적으로 작동하는 것을 확인할 수 있었다.
