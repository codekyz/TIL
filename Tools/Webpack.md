[인프런 프론트엔드 개발자를 위한 웹팩](https://inf.run/6AGY) / [장기효(캡틴판교)](https://joshua1988.github.io/)  

[웹팩 핸드북](https://joshua1988.github.io/webpack-guide/)  

[웹팩 공식문서](https://webpack.js.org/concepts/)  


# Node.js와 NPM
> 웹팩을 사용하기 위해 Node.js와 NPM이 설치되어 있어야 함
> Node.js를 설치하면 NPM은 함께 설치가 됨

## Node.js
> 브라우저 밖에서도 자바스크립트를 실행할 수 있는 환경을 의미

## NPM(Node Package Manager)
> 자바스크립트 라이브러리(패키지)를 관리해주는 도구(jQuery, Tensorflow, express 등)
> 라이브러리를 공개된 저장소에 올려놓고 npm 명령어로 편하게 다운로드 받을 수 있음
- `node -v` : 노드 버전 확인
- `npm -v` : NPM 버전 확인
- `npm init [-y]` : NPM 초기화 명령어(-y 기본값으로 package.json파일 생성)
- `npm install [library] (--save-prod)` : 라이브러리 지역 설치1(node_modules/library/dist/library.js)
- `npm install [library] --save-dev(-D)` : 라이브러리 지역 설치2(devDependencies로 관리)
- `npm uninstall [library]` : 라이브러리 삭제
- `npm install [library] --global(-g)` : 라이브러리 시스템 레벨에 전역(global)으로 설치

### 지역 설치 vs 전역 설치
- 지역 설치 : 해당 폴더 내에서 node_modules 폴더를 생성하여 설치
- 전역 설치 : 시스템 레벨에 전역으로 설치하여 터미널에서 라이브러리 이름을 입력했을때 명령어로 인식

### NPM을 사용하는 이유
1. 프로젝트에 사용하는 package(라이브러리)와 버전 관리
2. 해당 package CDN을 직접 찾아서 가져오지 않고 npm install로 바로 설치 가능
3. 대부분의 웹팩 프로젝트는 기본적으로 npm이 동반됨

### dependencies와 devDependencies
- dependencies : npm i [library]
    - 애플리케이션의 화면로직과 직접적 관련이 있는 라이브러리(ex.jquery, vue, react, angular, chart 등)
- devDependencies : npm i [library] -D
    - 개발을 할때 도움을 주는 개발 보조 라이브러리(ex.webpack, sass, js-compression 등)

## 배포용 라이브러리 dependencies
- `npm run build` 로 빌드를 하면 최종 애플리케이션 코드 안에 포함됨

## 개발용 라이브러리 devDependencies
- 최종 배포 시 포함되지 않음


# 웹팩 Webpack
> 프론트엔드 프레임워크에서 가장 많이 사용되는 모듈 번들러(Module Bundler)
> 모듈 번들러란? 웹 애플리케이션을 구성하는 자원을 모두 각각 모듈로 보고 조합해서 병합된 하나의 결과물을 만드는 도구
- `webpack webpack-cli` 
- `lodash`
- `dist/main.js` : 웹팩으로 구성한 결과물(즉시실행함수IIFE 구성)
- 자바스크립트만을 위한 도구가 아닌 웹을 구성하는 모든 리소스에 대한 도구임
- `devtool: 'source-map'` : 빌드 후 원래 파일로 연결

## 모듈 번들링이란?
> 웹 애플리케이션을 구성하는 몇십, 몇백개의 자원들을 하나의 파일로 병합 및 압축해주는 동작(빌드==변환==번들링)

## 모듈 이란?
> 프로그램에서 특정 기능을 갖는 작은 코드 단위를 의미

## 웹팩의 등장배경
1. 파일 단위의 자바스크립트 모듈 관리
    - 파일단위로 스코프가 구분되지 않음(전역변수)
2. 웹 개발 작업 자동화 도구
3. 웹 애플리케이션의 빠른 로딩 속도와 높은 성능
    - 웹팩은 기본적으로 필요한 자원은 미리 로딩하는게 아니라 그 때 그 때 요청하자는 철학을 갖고 있음

## 웹팩으로 해결하려는 문제
1. 브라우저별 HTTP 요청 숫자의 제약
    - TCP 스펙에 따라 브라우저에서 한번에 서버로 보낼 수 있는 HTTP요청 숫자는 제약되어 있음
2. Dynamic Loading & Lazy Loading 미지원

# 웹팩의 주요속성
0. mode
    - 버전4 이상에서 추가된 속성
    - `'none'` `'production'` `'development'`
1. Entry
    - 웹팩에서 웹 자원을 변환하기 위해 필요한 최초 진입점이자 자바스크립트 파일, 경로
    - 웹 애플리케이션의 전반적인 구조와 내용이 담김
2. Output
    - 웹팩을 돌리고 난 결과물의 파일 경로
    - 최소한 `filename`은 지정해줘야함
    - 파일 이름 옵션에 매 빌드시 고유 해시값을 붙여 새로고침해야하는 상황을 방지할 수 있음
3. Loader(module)
    - 웹팩이 웹 애플리케이션을 해석할때 자바스크립트 파일이 아닌 웹 자원들을 변환할 수 있도록 도와주는 속성
    - 
    ```
    {
        test: /\.css$/,
        use: ['style-loader', 'css-loader']
        // 모든 css파일에 대해 로더 적용
        // rules 아래에 객체를 추가해 나가면서 각 파일들에 적용
        // 로더 순서도 영향이 있음(오른쪽에서 왼쪽순서로 적용)
    }
    ```
4. plugin(plugins)
    - 웹팩의 기본적인 동작에 추가적인 기능을 제공하는 속성
    - 플러그인은 결과물의 형태를 바꾸는 역할


# Webpack Dev Server
> 웹 애플리케이션을 개발하는 과정에서 유용하게 쓰이는 도구
> 웹팩의 빌드 대상 파일이 변경 되었을 때 코드만 변경하고 저장하면 웹팩으로 빌드한 후 새로고침 해줌
> 웹팩의 빌드 시간 또한 줄여줌
```
// package.json
"scripts": {
    "dev": "webpack serve",
    "build": "webpack"
}

//webpack.config.js
devServer: {
    port: 9000,
}
```
- 웹팩 데브 서버로 빌드한 결과물은 메모리에 저장되고 파일로 생성하지 않음(파일 시스템에 나오지 않음)
- 웹팩 데브 서버는 개발할 때만 사용하다가 완료되면 웹팩 명령어를 이용해 결과물을 파일로 생성
- 컴퓨터 구조 관점에서 파일 입출력보다 메모리 입출력이 더 빠르고 자원이 덜 소모됨