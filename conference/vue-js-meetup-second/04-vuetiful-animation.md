# Vuetiful 애니메이션: Framer 따라잡기 by 이승민 님

http://slides.com/smilee/vuetiful-animations/live

1회차 밋업에서 도전했던 게임에 애니메이션을 추가하는 과정

coffeescript 기반의 프로토타이핑 툴인 Framer로 만든 프로토타입을 Vue로 만들어보자!

## `<transition />`

Transition의 기본적인 내부구조
- `v-enter`
- `v-enter-to`
- `v-leave`
- `v-leave-to`

## 이걸로는 부족해!

이걸로 다 할 수 있을 것 같았지만, 이걸로는 당연히 부족해!
- Vue에 `jQuery`, `jQueryUI`를 끌어와서 구현
- 모바일에서의 터치이벤트를 구현하기 위해 `jQueryUI.touce-punch`를 사용
- 제한적인 `jQueryUI`의 easing을 보완하기 위해 `velocity.js`를 사용

## 부자연스러워!

슬라이딩으로 지우긴 했는데, 리스트에서 항목이 단박에 사라지는게 부자연스러워!

이를 보완하기 위해 `<transition-group />`

`*-move`
``` css
.*-move {
  transition: transform 0.2s;
}
```
