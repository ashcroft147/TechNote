# WepPage에 Social Button 추가하기

## Font Awesome Download
 - 아래의 링크를 통하여 Font Awesome을 DownLoad하고, 해당 CSS파일을 추가한다.
 [DownLoad Font Awesome](http://fontawesome.io/get-started/)

## HTML 코드 추가
 - 아래와 같이 html코드를 Social 버튼을 추가할 페이지에 추가한다.
 - target="_blank" 속성을 사용하여 새페이지에서 링크가 열리도록 한다. 
~~~
<a className="bg-facebook" href="https://www.facebook.com/facebook" target="_blank" title="facebook">
    <i className="fa fa-facebook-square fa-5x"></i> 
</a>
~~~

## CSS 속성 추가
 - Font Awesome에서 제공하는 Social Button은 Gray 색상으로 표시가 되므로, Google 검색을 통해 각 Social 버튼의 Color Code를 검색한후
   CSS 에 색상을 정의 한다. 
~~~
.fa-facebook-square {
    color: #3b5998;
}
~~~

## 결과
 ![Social Buttons](./img/Firebase/08.fb.png)