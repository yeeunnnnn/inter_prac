# Node.js(express)

JS는 컴퓨터가 아닌 브라우저의 인터프리터를 통해 실행되기 때문에 별도의 설치가 필요없음

 근데 내 컴퓨터, 혹은 서버에서 자바를 실행하려면 node.js를 설치해야 함

npm은 필요한 툴들이 있으면 가져다가 쓸 수 있게 해주는거임. 

윈도우 설치할때 초기에 setup.exe로 설치하는 것 처럼

npm instll (모듈이름) 이런 식으로 설치 명령어가 있음

-g 라고 붙이면 글로벌로 설치돼서 컴퓨터 내의 모든 폴더에서 사용이 가능한데

충돌이 일어날 수 있어서 안하는게 좋음.

모듈을 설치하면 package.json, package-lock.json 이라는 두 파일이 생기는데

package.json : 모듈의 내용을 대략적으로 확인하기 위함

package-lock.json : 모듈의 내용을 상세하게 확인하기 위함 

express도 하나의 모듈인데 node.js 를 이용해서 웹 프레임워크를 만드는 건데

```jsx
import express from 'express'

const app = express()

app.get('/', (req, res) => {
  res.send('Hello World')
})

app.listen(3000)
```

(express - npm에서 가져온 예제코드)

port는 항구에서 유래된건데 들어가는 입구임. 정해진 규격이 있음. 포트마다 다른 프로그램을 켤수있음.

localhost는 자기 아이피도메인임.

**app.get( ’/ ’ , () ⇒ {} )**

get은 HTTP 메소드, / 은 라우팅, 그 뒤는 콜백 함수

listen은 포트를 열어두는 코드

```jsx
app.get('/user/:id', (req, res) => {
  const q = req.params
  console.log(q.id)
  
  res.json({'userid': q.id})
})
```

라우팅에 :(콜론)을 쓰고 변수명을 쓰면 그 값이 params에 들어간다 이게 params로 받는방법.

그다음 쿼리로 받는 방법은 물음표 뒤에

?q=jocoding&name=jo&age=20 이런식으로 적으면

params 값도 각각 들어간다.

출력은 console.log(q.name) 이런식으로 하면 나옴.

const p = req.params

[p.name](http://p.name) 이라고 찍어줘야 p에 그 값이 저장이 됐는데

const { name } = req.params 이렇게 중괄호에 넣으면 바로 저장이 됨. 

cors 모듈

```jsx
var cors = require('cors')
app.use(cors())
```

cors 설정 코드임 왜 해야된다는건진 이해가 안됨.