---
title: "VS Code Extension 개발 시작하기"
categories: 
  - dev
last_modified_at: 2020-06-09T00:00:00+09:00
toc: true
author_profile: true
tag: 
  - vscode
  - extension
---

VS Code Extension을 개발하는 방법을 간략하게 소개해본다.

# Visual Code Extension 개발 시작하기

VS Code를 사용해보면 알겠지만 왼쪽의 Extensions탭에 들어가보면 수많은 Extension들이 출시되어 있다.

각 Extension을 클릭하면 설명에 개발자, 다운로드 횟수와 함께 *Repository* 버튼이 있는데 이 Extension의 소스를 직접 확인해 볼 수도 있다.
GitLens와 같이 복잡한 소스를 보면 소스 구성을 이런 식으로 하면 좋겠다 또는 단순한 한 두 가지의 기능을 제공하는 Extension의 소스를 보면 보다 명확하게 특정 기능을 구현하는 방법에 대해 알 수 있으므로 만들고 싶은 Extension이 있다면 비슷한 기능을 가지는 여러 Extension의 소스를 참고해보자.
_레퍼런스가 많지 않아 소스를 참고하는 것이 도움이 되었다._


아래의 방법은 VS Code에서 제공하는 [Tutorial](https://code.visualstudio.com/api/get-started/your-first-extension)을 토대로 작성되었다.

## Extension 프로젝트 생성하기

먼저 Node.js와 Git이 설치되어있다고 가정한다.
그리고 Yeoman을 설치한다. Yeoman은 프로젝트를 쉽게 생성할 수 있게 도와주는 제너레이터 툴이다. 이 프로젝트에서는 이미 생성되어 있는 [VS Code Extension Generator](https://www.npmjs.com/package/generator-code)를 이용해서 code 프로젝트를 생성해본다.

```sh
npm install -g yo generator-code
```


설치가 완료되었으면 아래와 같이 입력해서 yo cli를 이용하여 프로젝트를 생성해보자.

```sh
yo code

# ? What type of extension do you want to create? New Extension (TypeScript)
# ? What's the name of your extension? HelloWorld
### Press <Enter> to choose default for all options below ###

# ? What's the identifier of your extension? helloworld
# ? What's the description of your extension? LEAVE BLANK
# ? Initialize a git repository? Yes
# ? Which package manager to use? npm

code ./helloworld
```

code 명령어는 해당 폴더에서 VS Code를 띄우겠다는 명령어이다.
VS Code 에디터가 뜨면 extension.ts를 볼 수 있다.


기본적으로 나는 TypeScript를 사용하여 개발하였다. 이는 VS Code API가 TypeScript를 사용하고 있기 때문이다.  
Extension 개발이라는 것은 VS Code에서 제공하는 API를 이용해서 원하는 이벤트가 발생했을 때 특정 기능을 구현하는 것이다. 때문에 매우 자유롭게 원하는 모든 기능을 구현할 수 있는 것은 아니다.

*그래서 개발하면서 한계에 부딪힐 때가 많았다ㅠㅠ* 예를 들어 아이콘을 커스터마이징하고 싶은데 수정할 수 있는 방법이 없다거나, 특정 위치에 우클릭 액션을 넣고 싶은데 액션을 받을 방법이 없다거나, 다른 extension과 동시에 사용할 때의 호환성 등.. (다른 extension과 동일한 위치에 메시지를 표시하고 싶을 때 어떻게 나타나는 지등을 체크하고 개발해야한다. 특히 그 *'다른'* extension이 굉장히 많이 사용되는 extension인 경우.)


그렇지만 VS Code API 문서를 읽어보면 이런 기능도 넣을 수 있어? 하는 부분도 많으므로 먼저 어떤 기능을 제공하는 지 훑어보면 좋다.


아무튼 이 **extension.ts**가 main이나 index파일과 같은 용도이다. VS Code Extension에서는 주로 이 파일을 프로그램의 진입점으로 사용한다. 이벤트 리스너나 커맨드를 등록하고 구독하면 내가 원하는 기능을 수행할 준비가 된다.


Extension에 대한 설정은 **package.json**파일에 설정하게 된다. 여기는 Extension이 활성화 되는 시점, 커스터마이징하고 싶은 부분들이나 내가 만든 커맨드 등을 등록할 수 있다. 일반 package.json과 마찬가지로 dependency도 여기 등록한다.


VS Code Editor에서 **F5**키를 입력하면 디버깅 모드로 Extension Development Host라는 별도의 VS Code창이 뜨게 되는데 이 곳에서 내가 만든 Extension이 원하는 대로 동작하는 지 테스트해 볼 수 있고, Parent 창에서 Debug Console로 들어가면 내가 찍은 console.log나 에러 메시지 등을 볼 수 있다.


## 개발 시작하기

개발하기에 앞서 아래의 문서를 참고하면 좋다.

1. [VS Code API](https://code.visualstudio.com/api/references/vscode-api) : VS Code API로 건드릴 수 있는 기능
2. [Contribution Points](https://code.visualstudio.com/api/references/contribution-points) : VS Code의 어느 영역을 건드릴 지 정하기
3. [Activation Events](https://code.visualstudio.com/api/references/activation-events) : 어느 시점에 Extension을 활성화 시킬 지 정하기
4. [VS Code Extension Samples](https://github.com/Microsoft/vscode-extension-samples) : 간단한 Extension 샘플, 하나씩 보면서 기능을 마음대로 넣어봐도 좋다.

## References

[https://code.visualstudio.com/api/get-started/your-first-extension](https://code.visualstudio.com/api/get-started/your-first-extension)
