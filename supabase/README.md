# supabase

백엔드 기능을 지원하는 클라우드 서비스

백엔드를 개발 하려면

데이터 보관할 database 필요하고

업로드 한 파일을 보관한 파일 서버 storage

회원가입 로그인 로그아웃을 구현할 인증 기능 auth

프로그래밍 쪽으로 다양한 작업을 수행할 시스템이 필요 edge function

이런 백엔드 기능만 쏙 담은게 supabase임 vs로 firebase가 있음

supabase 구조 

account 일단 사용자의 계정이 있음

하나의 계정엔 여러개의 Organizations 가 들어갈수 있고

실질적인 개념의 프로젝트 = supabase 의 project로 동일

프로젝트 안에 database, storage, auth, egde function이 있음

그 데이터베이스 안에 테이블이 있고

테이블 안에 행이 있음

간단 실습

- supabase 로그인 / 무료는 두개 프로젝트 만들기 가능 / 일주일 뒤면 정지됨

![image.png](image.png)

- new project로 프로젝트 아무거나 하나 만들기

![image.png](image%201.png)

- 이름과 DB 비밀번호를 생성 후, 서비스 지역을 최대한 현지와 가까운 곳으로 설정 후 프로젝트 생성

![image.png](image%202.png)

- Table editor 들어가서 new table 생성한 뒤, 테이블 이름 적어주고,

이번에는 RLS 해제함(Row Level Security를 기본적으로 enable 돼있는데 일단은 어려워서 끔)

![image.png](image%203.png)

- 밑으로 내리면 컬럼을 지정할 수 있는데

기본적으로 id 컬럼은 primary로 지정돼있고, is identity가 지정돼 있어서 

행을 만들 때 마다 id 컬럼의 값이 1씩 증가돼서 식별자가 됨.

- created_at 타임스탬프z 타입에 기본값이 now라서 행을 생성할 때 마다 자동으로 현재 시간이 적히게 된다.
- 나머지는 추가해서 text로 지정

![image.png](image%204.png)

- 테이블을 만든 뒤에 insert row로 행을 추가할 수 있다.

![image.png](image%205.png)

- 원래 관계형 데이터베이스에서는 sql이라고 하는 관계형 데이터베이스용 컴퓨터 언어를 이용해서 표도 만들고 행도 추가하고 하는데 **supabase는 ai와 굉장히 강하게 통합돼있어서 SQL Editor에서 ctrl + k 를 누르면 ai가 동작해서 sql문을 자동으로 만들어줌.**

**이제부터는 웹애플리케이션에 supabase를 통합하는 방법임**

설치없이 간단하게 js bin 서비스를 이용해서 코딩함!

sql을 이용하는 방법도 있겠지만 그럼 nodejs, python, java 같은 중간 존재 시스템이 필요해서

웹사이트에서 html과 js만을 이용해서 백엔드 시스템을 생략하고 바로 데이터베이스랑 접속해서

간결하고 빠르게 어플리케이션을 만들어볼것임

![image.png](image%206.png)

- supabase js라고 인터넷에 검색하면 docs 문서가 나오는데, 라이브리리를 설치하는 법이 나옴
- node.js를 사용하면 위에 npm istall로 설치하면 되고, 브라우저에서 사용한다면 아래의 스크립트 코드를 붙여넣으면 됨.

![image.png](image%207.png)

- 라이브러리 스크립트와 기본 UI를 만든것.

![image.png](image%208.png)

- Project settings - Data API 를 들어가면 URL이 있고 이게 프로젝트의 식별자임, 그 밑에 API Keys 들어가면 비밀번호에 해당되는 키가 있는데 secret 키는 사용하지않고 public 키를 사용함.

![image.png](image%209.png)

- URL과 공개 API 키를 사용해서 **Supabase 클라이언트 객체**를 생성함

이제 라이브러리를 사용할 수 있는 기본적인 준비는 끝남!

이제 page 테이블의 데이터를 가져와서 ui에 끼워 넣을건데

![image.png](image%2010.png)

- API Docs - page - Read rows 들어가면 테이블의 행들을 가져올 수 있는 코드들이 적혀저 있음

![image.png](image%2011.png)

- await 뒤에 있는 코드들은 비동기적으로 동작하는 코드인데 동기적으로 바꿔주는 코드가 await임.

await 키워드를 사용하고 있는 코드는 반드시 async로 시작하는 함수 안에 담아야함.

- 그러면 refreshHistory(); 로 함수호출 가능하고 콘솔로그로 찍음.

![image.png](image%2012.png)

- tag 변수를 만들어서 id가 history에 들어가도록 동적으로 생성함

![image.png](image%2013.png)

- 실행하면 데이터를 잘 가져옴

![image.png](image%2014.png)

- create 버튼을 누르면 title과 body를 받아서 그걸 데이터로 추가하는 insert 기능을 만든 코드임.

![image.png](image%2015.png)

- 마찬가지로 API Docs - page - insert rows에 들어가면, 코드가 있어서 붙여넣으면 된다.

![image.png](image%2016.png)

![image.png](image%2017.png)

- create버튼을 눌러 title과 body를 누르면(위 사진) 데이터가 추가가 된 걸 볼수있다(아래 사진)

![image.png](image%2018.png)

- supabase의 테이블에디터에도 열이 추가 된 것을 확인할 수 있다!

최종 코드

```jsx
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width">
  <script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2"></script>
</head>
<body>
  <h1>Supabase</h1>
  <div id="history"></div>
  <input type="button" value="create" id="create_btn" />

  <script>
    const supabaseUrl = 'https://owqioycnqdzfjqknjtbt.supabase.co';
    const supabaseKey = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6Im93cWlveWNucWR6Zmpxa25qdGJ0Iiwicm9sZSI6ImFub24iLCJpYXQiOjE3NTUwNzk3NjksImV4cCI6MjA3MDY1NTc2OX0.9GlIFRQSP0CCu2uQBx1lwZXxoj4wHmhFJNT8JD6H_u0';
const client = supabase.createClient(supabaseUrl, supabaseKey);
    async function refreshHistory() {
      let { data: record, error } = await client.from('page').select('*');
        console.log('record', record);
      let tag = "";
      for (let i=0; i<record.length; i++) {
        tag += `<h2>${record[i].title}</h2>${record[i].body}`;
      }
      document.querySelector("#history").innerHTML = tag;
    }

    refreshHistory();
    
async function recordHandler() {
  const { data, error } = await client
  .from('page')
  .insert([{ title: prompt("title?"), body: prompt("body?") }])
  refreshHistory();
}
document
 .querySelector("#create_btn")
 .addEventListener("click", recordHandler);
  </script>
</body>
</html>
```