# React
리액트는 단방향을 지원하며 이로인해 유지보수의 이점을 얻을 수 있게됐다.(전통적으로 개발자는 역할을 제한받으면서 성장해옴)
<br>
그리고 리액트는 가장 완벽하거나 빠르거나 합리적이다기보단 많이 사용하는 라이브러리일 뿐..
## React의 역사
2000년대까지 웹 생태계의 주류는 LAMP 스택(Linux, Apache, MySQL, PHP)를 이용한 웹 개발이 주를 이루던 시기였다.
<br>
전통적인 SSR
- 클라이언트 요청: 사용자가 웹 브라우저에서 URL을 입력하거나 링크를 클릭하면 HTTP 요청이 서버로 전송됩니다.
- 서버 처리: Apache 웹 서버는 이 요청을 받아서 PHP 스크립트(혹은 다른 서버사이드 언어)로 전달합니다. 이 스크립트는 요청을 분석하고 필요한 데이터를 MySQL(MariaDB) 데이터베이스에서 조회합니다.
- HTML 생성: PHP 스크립트는 데이터베이스에서 가져온 데이터를 사용하여 HTML 코드를 생성합니다. 이 과정에서 템플릿 엔진을 사용하여 동적인 콘텐츠를 HTML에 삽입하기도 합니다.
- HTML 응답: 생성된 HTML 문서는 Apache 웹 서버에 의해 클라이언트에게 HTTP 응답으로 전송됩니다.
- 클라이언트 렌더링: 클라이언트의 웹 브라우저는 서버로부터 받은 HTML 문서를 렌더링하여 사용자가 볼 수 있는 웹 페이지로 보여줍니다.
그리고 자바스크립트는 단순히 폼 처리와 같은 부수적인 역할만 담당했다.
<br>
그렇게 2010년대에 들어서 자바스크립트를 좀 더 편리하게 사용하기 위한 제이쿼리가 등장했고 인기를 끌었다. 그리고 이후 웹소켓, 캔버스, 로컬스토리지, 지오로케이션 등 많은 API들을 브라우저에서 제공하기 시작했다.
<br>
자바스크립트로 적극적으로 DOM을 수정해서 사용자에게 인터랙션을 보여줄일이 많아졌고 자바스크립트 코드 또한 길어졌다. 그래서 ㄹ이런 코드를 체계화하기 위해 coffeescript, angular, underscore.js 같은 프레임워크들이 나오게됐다.
<br>
이 당시 페이스북은 전세계 7억명정도가 사용하는 SNS서비스였고, 성능을 챙기기위해서 서버에서 렌더링하거나 자바스크립트 번들 크기를 줄이기 위해 노력했다. 하지만 많은 기능들을 위해서 자바스크립트의 크기가 늘어나는건 불가피했다.
<br>
그래서 이를 해결하기 위해 React가 개발됐고 html,css,js로의 수직적 관심사 분리는 컴포넌트별로 기능을 다루는 수평적 관심사 분리로 변경됐다.
<br>
당시 사용되던 backbone.js와 리액트의 코드 비교
```jsx
// Backbone Model
var MessageModel = Backbone.Model.extend({
  defaults: {
    message: "Hello, World!"
  }
});

// Backbone View
var MessageView = Backbone.View.extend({
  el: '#app', // DOM 요소를 타겟팅
  template: _.template('<h1><%= message %></h1><button>Update Message</button>'),

  events: {
    'click button': 'updateMessage'
  },

  initialize: function() {
    this.listenTo(this.model, 'change', this.render); // 모델이 변경되면 뷰를 다시 렌더링
    this.render(); // 초기 렌더링
  },

  render: function() {
    this.$el.html(this.template(this.model.toJSON())); // 템플릿을 사용하여 HTML 생성
    return this;
  },

  updateMessage: function() {
    this.model.set('message', 'Hello, Backbone.js!'); // 모델의 데이터 업데이트
  }
});

// 인스턴스 생성 및 애플리케이션 초기화
var messageModel = new MessageModel();
var messageView = new MessageView({ model: messageModel });


//리액트
import React, { useState } from 'react';

function App() {
  // useState 훅을 사용하여 컴포넌트 상태 관리
  const [message, setMessage] = useState('Hello, World!');

  // 버튼 클릭 핸들러
  const updateMessage = () => {
    setMessage('Hello, React!');
  };

  // JSX를 사용한 컴포넌트 렌더링
  return (
    <div id="app">
      <h1>{message}</h1>
      <button onClick={updateMessage}>Update Message</button>
    </div>
  );
}

export default App;
```
