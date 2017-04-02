# npm package 'create-react-app' [[README.md]('https://github.com/facebookincubator/create-react-app')]

## 그림, 폰트, 파일을 추가하기 [[link](https://github.com/facebookincubator/create-react-app/blob/master/packages/react-scripts/template/README.md#adding-images-fonts-and-files)]

1. 정석

    webpack은 static asset에 접근하기 위하여 JavaScript Module에서 파일을 `import` 할 수 있다.

    다음과 같은 이점을 가짐:

    - 파일에 바로 접근 가능한 path string으로 반환되어 src, href 등 attribute에 바로 사용 가능
    - 서버로의 요청을 줄이기 위해 10,000 bytes 이하의 이미지는 data URI로 반환됨 (SVG 제외)

    그래서 다음의 코드가 예제로 주어져있다.
    
    ``` js
    import React from 'react';
    import logo from './logo.png'; // Tell Webpack this JS file uses this image

    console.log(logo); // /logo.84287d09.png

    function Header() {
        // Import result is the URL of your image
        return <img src={logo} alt="Logo" />;
    }

    export default Header;
    ```

    __가만, 근데 이걸 적용해보려니..__

    복잡한 asset 구조의 프로젝트 내 하위 컴포넌트에서 file path에 접근해야 할 때
    
    다음과 같이 코드를 작성해야만 파일에 접근이 가능했다. (dev 단계의 코드였기 때문일수도 있다.)

    ``` js
    import React from 'react';
    import { Image } from 'react-bootstrap';
    // 문제가 될 수 있는 파일 경로.
    // 본 파일의 경로는 src\components\etc\Mark.js
    import circle from '../../../public/image/circle.png';

    const Mark = ({ pattern }) => (
        <Image src={circle} alt="circle"/>
    );

    export default Mark;
    ```

2. 그래서, 좀 더 쉽게? Escape Hatch [[link]('https://github.com/facebookincubator/create-react-app/blob/master/packages/react-scripts/template/README.md#using-the-public-folder')]

    component 코드의 물리적인 depth별로 달라질 수 있는 경로를 그대로 쓰지 말고, 상대경로를 쓸 수는 없을까?
    
    public 폴더 내의 파일은 minified / bundled 되지 않으며, 원본 상태 그대로 access 가능함.

    `index.html` 내부(사실 바로 위에서 얘기한 pre-precess를 타지 않는 파일들이 모두 포함되는 듯)에서 접근할 때와 JavaScript code(예를 들어, React Component)에서 접근할 때의 코드가 상이하다.

    발췌 :
    > Inside `index.html`. you can use it like this:

    ``` js
    <link rel="shortcut icon" href="%PUBLIC_URL%/favicon.ico">
    ```

    > In JavaScript code, you can use `process.env.PUBLIC_URL` for similar purposes:

    ``` js
    render() {
        // Note: this is an escape hatch and should be used sparingly!
        // Normally we recommend using 'import' for getting assets URLs
        // as described in "Adding Images and Fonts" above this section.
        return <img src={process.env.PUBLIC_URL + '/img/logo.png'} />
    }
    ```