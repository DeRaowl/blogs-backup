## SASS - CSS with a superpower

Hi Folks,

If we work on small projects, there won't be a lot of need to maintain CSS, but if you're dealing with major projects? Maintaining CSS will be difficult. That's when SASS comes into play.

SASS or Syntactically Awesome Style Sheets is a scripting language and CSS preprocessor which compiles into CSS. This means when we write code in SASS, it automatically converts sass code into CSS.

### Why SASS?

- It follows, "Don't repeat yourself principle" also called **DRY PRINCIPLE**
- Helps us to maintain our CSS code in a more organized manner.

### SASS comes up with 2 syntaxes:

1. SCSS: Sassy CSS is a superset of CSS. In simple terms, a valid CSS file is a valid SCSS file. SCSS files have .scss file extension
2. Intended syntax: Intended syntax mainly focuses on indentation. Intended files have a .sass file extension. 

SASS comes with a lot of features such as variables, nested rules, mixins, inline imports, built-in functions, etc. What we learn in detail.

### SASS features.

1. Variable

You can declare variables globally and can use its placeholder at multiple places.

SCSS,
```
$color-primary: #000;
$color-secondary: #333;
.nav-links{
       background-color: $color-primary;
       color: $color-secondary;
}
``` 
CSS,
```
.nav-links{
          background-color: #000;
          color: #333;
}
``` 
2.
Nesting

We can nest selectors which share the same parent name which makes CSS more readable.
SCSS,

```
li{
display: inline-block
margin-left: 30px;
&:first-child{
margin: 0;
}
``` 
CSS,

```
li{
display: inline-block;
margin-left: 30px;
}
li:first-child{
margin:0;
}
``` 
3.
Mixins & Include - Mixins allow us to define CSS rules as a blueprint and we can use these rules in our selectors. To use mixins we have to use @ include followed by mixin name.
SCSS,
```
$color-primary: #333;
@mixin header-main($bg-color){
color: $color-primary;
font-size: 3rem;
border: 2px solid $color-primary;
background-color: $bg-color;
}
.header {
@include header-main(#2b2b2b);  /*We can use this statement at multiple places if 
required by passing different bg-color parameter*/
}
``` 
CSS,

```
.header {
color: #333;
font-size: 3rem;
border: 2px solid #333;
background-color: #2b2b2b;
}
``` 
4.
Functions: Yes, SASS allows us to create functions. To use functions we prefix function keyword with @ symbol.
```
@function divide($a/$b){
@return $a/$b;
}
.header{
padding: divide(30,7);
}
``` 
### Conclusion
These are some of the most useful features SASS comes with. You can read more about SASS here <a href="https://sass-lang.com/documentation/syntax">Official Doc</a>. This is one of the good things about learning SASS as a developer that saves so much time. However, there are disadvantages too in SASS, which you can read here <a href="https://www.javatpoint.com/sass-advantages-and-disadvantages">Disadvantages</a>

Regarding SAAS, please let me know if this article was helpful in the comments. And your feedback is welcomed.