## Reflow, Repaint

> 화면의 변경된 레이아웃을 계산하는 과정을 Reflow, 화면에 다시 그리는 과정을 Repaint
>
> 렌더링 최적화를 위해선 Reflow, Repaint를 줄여야 한다.



### Reflow(Layout)

Render Tree와 각 요소들의 크기와 위치를 다시 계산하는 과정.

다음과 같은 경우에 Reflow가 실행된다.

* 페이지 초기 렌더링
* 윈도우 리사이징
* 노드 추가 또는 제거
* 요소의 위치, 크기 변경
* 폰트 변경과 이미지 크기 변경
* 엘리먼트에 대한 offsetWidth, offsetHeight과 같은 위치값 계산 



### Repaint(Paint)

변경된 Render Tree를 화면에 다시 그려주는 과정.

Reflow는 일어나지 않지만 Repaint만 일어나는 경우가 있다.

* background-color 변경
* visibility 변경
  * visibility 같은 경우에는 hidden이어도 Render Tree에 포함된다.



### Reflow, Repaint를 줄이는 방법

**why ?** 

Reflow, Repaint가 많을수록 렌더링 속도에 영향을 주기 때문에 최소화할수록 좋다.



1. 클래스 변경을 통해 스타일을 변경할 경우, 최대한 말단의 노드를 변경해서 reflow의 영향을 최소화한다.
2. 인라인 스타일을 사용하지 않는다.
   * 인라인 스타일은 HTML이 다운로드될 떄 레이아웃에 영향을 미치면서 추가 reflow를 발생시킨다.
3. 애니메이션이 들어간 element는 ``position: fixed`` 또는 ``position: absolute``로 지정한다.
   * Render Tree에서 별도로 그려지기 때문에 다른 엘리먼트에 영향을 끼치지 않는다.
4. ``table`` 레이아웃을 피한다.
   * 테이블 레이아웃은 모두 로드되고 계산된 후에야 화면에 뿌려지게 된다. 또한 작은 변경만으로도 테이블의 모든 노드가 reflow된다.
   * 사용할거면 ``table-layout: fixed`` 속성을 주는 것이 좋다. 이때 열 너비가 머리글 행 내용을 기반으로 계산된다.
5. CSS에서의 JS 표현식을 피한다.
   * reflow될때마다 JS 표현식이 다시 계산된다.
6. CSS 하위셀렉터를 최소화한다.
   * 사용하는 규칙이 적을수록 reflow가 빠르다.
7. JS를 통해 스타일을 변경할 경우 작업을 그룹화한다.
   * className을 바꿔주거나 cssText를 바꿔주면 1번의 reflow만 일어난다.

8. DOM을 추가할 경우 , DOM Fragment를 활용한다
   * DOM에 매번 `appendChild` 할 경우 그떄마다 reflow를 일으킨다.
   * 따라서 메모리에 DOM을 만드는 Fragment를 활용하고, ``appendChild``와 같이 DOM을 직접 조작하는 작업은 최소화한다.
9. 캐시를 활용해 Reflow를 최소화한다.
   * offset을 계산한 정보를 변수에 저장해놓고 활용한다.





### Reference

* https://boxfoxs.tistory.com/408
* https://github.com/wonism/TIL/blob/master/front-end/browser/reflow-repaint.md
* https://gloriajun.github.io/frontend/2018/10/23/frontend-reflow-repaint.html