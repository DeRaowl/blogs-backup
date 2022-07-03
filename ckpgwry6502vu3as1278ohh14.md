## ::Before and ::After in CSS made easy

Hello, People

Today we are going to learn about pseudo-elements, one of the most useful CSS properties.
Pseudo-elements in CSS allow us to add content to a page without adding additional HTML elements.
Seems confusing? Okay, in simple terms.

<blockquote>Pseudo-elements are like a shadow, which can be seen but not able to touch.</blockquote>

I can assure you that if you master these topics, you will use them all over your project. Without wasting time let us dive in.

<h1 style="color: #022e57;">::Before</h1>
Before selector is used to position content before the content of the selected element.
### Syntax
We need to add the item with the keyword ::before with the required content property. The content can be any string or even blank.

```
     element::before{
      content: "";
     }

``` 
>Note: before and after pseudo-elements will not work without content property.  

### Example

%[https://codepen.io/Archisol/pen/poeLzLR]


<h1 style="color: #022e57;">::After</h1>
The after pseudo-element can be used to position content after the content of the selected element.
### Syntax

We need to add the item with the keyword ::after with the required content property.

```
     element::after{
      content: "";
     }

``` 

### Example
%[https://codepen.io/Archisol/pen/JjWLPMZ]

> Note: These elements are inline by default

I Hope, the blog was useful. If there are any queries feel free to ping me on <a href="https://twitter.com/DeRaowl">Twitter</a>. **Now as a task you can create the below image** using before and after pseudo-elements.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1622716152574/FjzGLaOXJ.png)

The solution can be found here <a href="https://codepen.io/Archisol/pen/QWpmLVK">Codepen</a>

For more about Pseudo Elements, refer below websites:

- <a href="https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-elements">MDN Web-Docs</a> 
- <a href="https://css-tricks.com/almanac/selectors/a/after-and-before/">CSS  Tricks</a> 
 