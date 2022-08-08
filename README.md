<h1>Learning Sass -my notes</h1>
<link>https://sass-lang.com/install</link>
<h2>Syntactically Awesome Style Sheets</h2>
<h4>Css Pre-Processor</h4>
<p>Sass - Compiler - Css (Live Sass compiler extension install)</p>
<h3>Features of Sass :</h3>
<pre>
Variables
Nesting
Partials & Imports
Mixins
Extends
Operators
Functions
Conditional Directives
Loops
</pre>

<h4>Variables :</h4>
<pre>
<p>common css</p>
p{                                           Variables
    color:  $primary-color;                  $primary-color: blue;
}
.top-area{
    color:  $primary-color;
}
.box1{
    color:  $primary-color;
}
</pre>

<h4>Nesting :</h4>
<pre>
Style.scss                                                                  Style.css                                                                               
nav {                                                                       nav ul {    
    ul {                                                                    margin: 10px;
        margin: 10px;                                                       paddin: 0;
        padding: 0;                                                         list-style: none;
        list-style: none;                                                 
    }                                                                      }                                                  
                                                                           
    li {                                                                    nav li {                                                    
        display: inline-block;                                              display: inline-block;
    }                                                                      }
                                                        
    a {                                                                     nav a {                                                                               
        text-decoration: none;                                              text-decoration: none;  
        display: block;                                                     display: block;
        padding: 10px 20px;                                                 padding: 10px 20px;
    }                                                                     }
}
</pre>

<h4>Partials :</h4>
<p>-different file as component based for easy manage</p>
<pre>
          - header _header.scss
          - banner _banner.scss
main.scss - about _about.scss
          - services _services
          - footer _footer

 @import "header"         
</pre>

<h4>Mixins :</h4>
<p>when same property different value</p>
<pre>
                                          CSS File
@mixin bd-radius($value){                 .abc{
    -webkit-border-radius: $value;         -webkit-border-radius: 5px;
    -moz-border-radius: $value;            -moz-border-radius: 5px;
    border-radius: $value;                 border-radius: 5px;
}                                        }
.abc{                                     .xyz{
    @include bd-radius(5px);               -webkit-border-radius: 5px;
}                                         -moz-border-radius: 10px;
.xyz{                                     border-radius: 10px;
    @include bd-radius(10px);
}
</pre>
<h4>Extends :</h4>
<p>for one different</p>
<pre>
                                                    Sass File
.a{                                                .a{
    color: red;                                       color: red;
    font-size: 5px;                                   font-size: 5px;
    font-weight: 700;                                 font-weight: 700;
    text-transform: uppercase;                        text-transform: uppercase;
}                                                    }
.b{                                                .b{
    color: blue;                                      color: blue;
    font-size: 5px;                                   @extend .abc;
    font-weight: 700;
    text-transform: uppercase;                     .c{
}                                                     color: blue;
.c{                                                   @extend .abc;
    color: blue;
    font-size: 5px;
    font-weight: 700;
    text-transform: uppercase;
}
</pre>
<p>Extends with placeholders - don't show in css file</p>
<pre>
                                                    Sass File
%a{                                                .a{
    color: red;                                       color: red;
    font-size: 5px;                                   font-size: 5px;
    font-weight: 700;                                 font-weight: 700;
    text-transform: uppercase;                        text-transform: uppercase;
}                                                    }
.b{                                                .b{
    color: blue;                                      color: blue;
    font-size: 5px;                                   @extend %abc;
    font-weight: 700;
    text-transform: uppercase;                     .c{
}                                                     color: blue;
.c{                                                   @extend %abc;
    color: blue;
    font-size: 5px;
    font-weight: 700;
    text-transform: uppercase;
}
</pre>

<h4>Operators :</h4>
<p>Type of Operators in Sass :</p>
<ul>
<li>Equality</li>
<li>Relational</li>
<li>Numeric</li>
<li>String</li>
<li>Boolean</li>
</li>

<pre>
Equality Operators :
== equal to
!= not equal to - return true/false
Ex- .a{
    scss                     css
    padding: 10px == 10px; - true
    padding: 10px == 20px; - false
    padding: arial == 'arial'; - true
    padding: (6px 10px) == (6px 10px); - true
    padding: (6px 10px) == (6px 8px); - false
    padding: (6px 10px) != (6px 8px); - true
}
</pre>

<pre>
Relational Operators :
< Less than
> Greater than
<= Less than equal to
>= Greater than equal to - use with if()
Ex - .a{
    scss                     css
    padding: 10px > 20px; - false
    padding: 1000ms >= 2s; - false
</pre>

<pre>
Boolean Operators : (and or not) - return true/false
Ex - .a{
    padding: not 10 = 10px; - false
    padding: not 10 1= 10px; - true
}
     .a{
    padding: arial == 'arial' or 10px == 20; - true
}
</pre>

<pre>
Numeric : (+ - * / %)

</pre>

<pre>
String : (+ concatenation)
Ex - 10 + px - 10px
 $var1 : 10
 $var2 : 5
.test{
    padding: $var1 + px; - 10px
}
.test{
    padding: $var1 - $var2 + px; - 5px
}
</pre>


<h5>Interpolation - #{}</h5>
<pre>
10 + px - 10px

margin- + $position: 20px;        margin-#{$position}: 20px;
.icon- + $name {                  .icon-#{$name}{

}                                }
Ex - 
@mixin margin($position, $unit){
    margin-#{$position} : $unit + px;
}

.test{
    @include margin(right, 20);
}

// .test {
//     margin-right: 20px;
// }

@mixin set-icon($name){
    .icon-#{$name}{
        background-image: url("/icons/#{$name}.png");
    }
}

@include set-icon(duck);

// .icon-duck {
//    background-image: url("/icons/duck.png");
// }
</pre>

<h4>Functions :</h4>
<pre>
@function function-name($value){
  @return ($value/2) + px;
}

.half-column{
    width: function-name(1000);
}

//Ex - 
$container-width: 1000;
@function half($width){
    @return ($width/2) + px;
}

@function one-third($width){
    @return ($width/3) + px;
}  

half-width{
    width: half($container-width);
}  

one-third-width{
    width: one-third($container-width);
} 

// half-width{
//     width: 500px;
// } 
// one-third-width{
//     width: 400px;
// }  
<h5>Number Funtion :</5>
<span>abs() ceil() floor() round() max() min() comparable() percentage() random() unit() unitless()</span>
Ex - 
scss                    
.test{                     .test{ 
    margin: abs(-10px)          margin: 10px;
}                           }
.test{
    margin: ceil(6.2); - 7
}
.test{
    margin: percentage(100px / 50px); - 200%
}
.test{
    margin: comparable(2cm, 1mm); - true
}

<h5>String Funtion :</5>
.test{
    font-family: quote(abc); - "abc"
    //or class
    font-family: unquote(".abc"); - .abc
    //or
    font-family: to-upper-case("abc"); - ABC
    //or
    font-family: to-lower-case("abc"); - abc
    //or
    font-family: str-length("abc"); - 3
    //or
    font-family: str-index("abc", "xyz"); - 1
    //or
    font-family: str-insert("abc", "xyz",4); //insert as index
    //or
    font-family: str-slice("abc",1); //cut
    //or
    font-family: unique-id(); //randomly
}

<h5>Color Funtion :</5>
<p>lighten() darken() adjust-hue() saturate() desaturate() mix() transparentize()</p>
<pre>
$base-color: pink;

#oneDiv, #twoDive{
    width: 400px;
    height: 100px;
    margin-bottom: 15px;
    border: 1px solid #000;
}
#oneDiv{
    background-color: $base-color;
}
#twoDive{
    //background-color: darken($base-color,70);
    //background-color: lighten($base-color,30);
    //background-color: adjust-hue($base-color,80);
    //background-color: saturate($base-color,90);
    //background-color: desaturate($base-color,90);
    //background-color: mix($base-color,red,50);
    //background-color: transparentize($base-color,0.3);
    background-color: red($base-color);
    background-color: green($base-color);
    background-color: hue($base-color);
}
</pre>

<h5>List Function :</h5>

<p>length() nth() set-nth() join() append() zip() index() list-separator() is-bracketed()</p>

$list: 10px 20px 30px; //or
$list2: 12px, 22px, 32px; //or
$list3: [10px, 20px, 30px];

Ex - 
.test{
    paddig: length($list); - 3
    //or
    paddig: length((width: 10px, height: 20px)); - 2
    //or
    paddig: nth($list, 2); - 20px
    //or
    paddig: set-nth($list, 2, 2em); - 10px 2em 30px
    //or
    paddig: join($list, $list2); - 10px 22px 30px 12px 22px 32px
    //or
    paddig: join((1 2 3),(4 5), comma); - 1,2,3,4,5
    //or
    paddig: append($list, 65px); - 10px 20px 30px 65px
    //or
    paddig: zip($list, $list2); - 10px 12px 20px 22px 30px 32px
    //or
    paddig: index($list, 20); - 
    //or
    paddig: list-separator($list2); - space
    //or
    paddig: is-bracketed($list3); - true

}

<h5>Selector Function :</h5>
<p>selector-nest, selector-append, selector-replace, is-superselector, simple-selectors, selector-unify, selector-extend</p>
Ex - 
$selector : selector-nest("ul", "li");

#($selector){              - ul li {
    width: 10px;                 width:: 10px;
}                            }

$selector : selector-append(".abc", "_copy", _img);

#($selector){              - .abc_copy, .abc_img {
    width: 10px;                 width:: 10px;
}

$selector : selector-replace("a.abc", ".abc", ".link");

#($selector){              - a.link {
    width: 10px;                 width:: 10px;
}

$selector : is-superselector("a", "a.active");

#($selector){              - true {
    width: 10px;                 width:: 10px;
}

$selector : is-superselector("a.active", "a");

#($selector){              - false {
    width: 10px;                 width:: 10px;
}

$selector : is-superselector("a", "nav a");

#($selector){              - true {
    width: 10px;                 width:: 10px;
}

$selector : is-superselector("nav a", "a");

#($selector){              - false {
    width: 10px;                 width:: 10px;
}

$selector : simple-selector("a.abc");

#($selector){              - a, .abc {
    width: 10px;                 width:: 10px;
}

<h5>Map Function :</h5>
<p>>map-get() map-merge() map-remove() map-keys() map-values() map-has-key()</p>
$map:("regular": 400, "medium": 500);
$map:("red": #ff0000, "green": #00ff00);
Ex - 
$font-weights: ("regular": 400, "medium": 500, "bold": 700);
$light-weights: ("lightest": 100, "light": 400);

$merge: map-merge($font-weights, $light-weights);
$mr: map-remove($font-weights, "regular");

.test{
    font-weight: map-get($font-weights, "medium"); - 500
    //or
    font-weight: map-keys($font-weights);
    font-weight: values($font-weights);
    //or
    font-weight: map-keys($merge);
    font-weight: map-keys($mr);
}
<h5>Introspection Functions :</h5>
<p>variable-exists()  global-variable-exists() mixin-exists() function-exists() type-of() inspect()</p>
$num: 10px;
$char: "Arial";
$list: 10px 20px 30px;
$map: ("regular": 400, "medium": 500);

@function sum($a, $b){
    @return $a + $b;
}

.test{
    paddig: variable-exists(num); - true
    //or
    paddig: variable-exists($list); - true
    //or
    paddig: global-variable-exists(num); - true
    //or
    paddig: mixin-exists(char); - false
    //or
    paddig: function-exists(sum); - true
    //or
    paddig: type-of($char); - string
}
</pre>

<h4>Conditional Directives :</h4>
<pre>
<h5>Content Directive :</h5>
<p>add extra property using @content</p>
relatable with mixin
<img src="https://i.ibb.co/xs0c3D6/o.jpg" alt="o" border="0">
@mixin test{                 #menu .block{
    #menu{                     color: green;
        @content;                  }
    }
}
@include test{
    .block{
        color: green;
    }
}

@content Directive most use with media query

css
@media screen and(max-width: 1300px){
    body{
        background: red;
    }
}
@media screen and(max-width: 1000px){
    body{
        background: blue;
    }
}
@media screen and(max-width: 700px){
    body{
        background: green;
    }
}

scss
@mixin media($width){
    @media screen and(max-width: $width){
    @content;
    }
}

@include media(1300px){
    body{
        background: red;
    }
}
@include media(100px){
    body{
        background: green;
    }
}
@include media(700px){
    body{
        background: blue;
    }
}

<h5>@media & @at-root :</h5>
    .container{
        width: 1100px;
        margin: 0px auto;
    
    @media screen and(max-width: 1150px){
        width: 900px;
    }
    @media screen and(max-width: 950px){
        width: 900px;
    }
}

<p>@at-root -for hide .parent time by time by @at-root</p>
<img src="https://i.ibb.co/RcJYgqb/Screenshot-123.png" alt="Screenshot-123" border="0">
</pre>

<h5>@if and @else</h5>
<pre>
    @if<Condition>{

    }

$test: 3;

p{
    @if $test < 5 {
        color: blue;
    }
}
Ex - 
$test: 3;

p{                                      p{
    @if $test < 5 {                       color: blue; 
        color: blue;                      font-size: 12px;                       
    }                                    }
    font-size: 12px;
}

p{                                     
    @if $test < 5 {color: blue;}            p{           
    @if 2 + 2 = 4 {font-size: 12px;}          color: blue; 
}                                             font-size: 12px;
                                             }
p{
    @if $test < 5 {
        color: blue;
    }@else{
        color: red;
    }
}                                             
</pre>

<h5>@for loop :</h5>
<pre>
@for <var> from <start> through <end>{
    
}

@for $i from 1 through 3 {
    .list-#{$i}{
        width: 100px * $i;
    }
}
.list-1{
    width: 100px;
}
.list-2{
    width: 200px;
}
.list-3{
    width: 300px;
}
</pre>

<h5>@while loop(condition) :</h5>
<pre>
@while(condition){

}

$i = 10;
@while $i <= 30 { //condition
    .pad-#{$i}{
        padding-left: 1px * $i; //statement
    }
    $i : $i + 10; //increment/decrement
}
.pad-1{
    padding-left: 10px;
}
.pad-2{
    padding-left: 20px;
}
.pad-3{
    padding-left: 30px;
}
</pre>

<h5>@each loop(condition) :</h5>
<pre>
    @each <var> in <list or map>{
     <statement>
    }

@each $i in(normal, bold, italic){
    #{$i}{
        font-weight: $i;
    }
}
.normal{
    font-weight: normal;
}
.bold{
    font-weight: bold;
}
.italic{
    font-weight: italic;
}
<p>3 type of @each loop directive:</p>
@each with simple list
multiple assignment(multi-dimensional list)
multiple assignment with maps
</pre>
