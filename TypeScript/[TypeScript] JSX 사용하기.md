## 왜 JSX를 사용하는가 ?

## SetUp
 - .ts 대신해서 .tsx 확장자를 사용한다.
 - tsconfig.json의 compilerOptions에 "jsx" :  "react" 옵션을 추가한다. 
 - React의 JSX를 typescript에서 사용하기 위한 package를 설치한다.
    - @types/react
    - @types/react-dom
 - .tsx 파일에 react를 import 한다.
    ~~~
    import * as React from 'react'
    ~~~
    - 왜 react의 import React from 'react'와 다른가 ?
      The React lib doesn't have a default export. So when you ask it to import React, it looks for an export named React. Unfortunately, it doesn't exist. Instead, import the whole thing and namespace in this way: