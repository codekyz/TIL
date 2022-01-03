[인프런 프론트엔드 개발자를 위한 웹팩](https://inf.run/6AGY) / [장기효(캡틴판교)](https://joshua1988.github.io/)  

[웹팩 핸드북](https://joshua1988.github.io/webpack-guide/)  


# Node.js와 NPM
> 웹팩을 사용하기 위해 Node.js와 NPM이 설치되어 있어야 함
> Node.js를 설치하면 NPM은 함께 설치가 됨

## Node.js
> 브라우저 밖에서도 자바스크립트를 실행할 수 있는 환경을 의미

## NPM(Node Package Manager)
> 자바스크립트 라이브러리를 관리해주는 도구(jQuery, Tensorflow, express 등)
> 라이브러리를 공개된 저장소에 올려놓고 npm 명령어로 편하게 다운로드 받을 수 있음
- `node -v` : 노드 버전 확인
- `npm -v` : NPM 버전 확인
- `npm init [-y]` : NPM 초기화 명령어(-y 기본값으로 package.json파일 생성)
- `npm install [library]` : 라이브러리 설치(node_modules/library/dist/library.js)

### NPM을 사용하는 이유
1. 프로젝트에 사용하는 package와 버전 관리
2. 해당 package CDN을 직접 찾아서 가져오지 않고 npm install로 바로 설치 가능

