# Animate Stylus NPM
*Just-add-water CSS animation*

## Disclaimer
So this is a fork of a fork. [slang800](https://github.com/slang800/animate-stylus) and [Dan Eden](https://github.com/daneden/animate.css) deserve credit for their work on this, but I will be making some potentially substantial changes here.

## Install

`npm install animate-stylus-npm`

## Usage
To use animate-stylus-npm in your website, just `@import animate-stylus` and reference the animations you want in your style-sheet. That's it! You've got a CSS animated element. Super!

```stylus
@require 'animate-stylus'

#yourElement
  animation-name: bounceOutLeft
  animation-duration: 3s
  animation-delay: 2s
  animation-iteration-count: infinite
```

And in your js file:

```javascript
var stylus = require('stylus')
  , animate = require('animate-stylus-npm');

stylus(str)
  .include(animate.path)
  .render(...)
```

Or by using `gulp`:

```javascript
// gulpfile.js
var animate = require('animate-stylus-npm');

gulp.task('stylus', function() {
    return gulp.src('./src/stylus/style.styl')
        .pipe(stylus({
            include: [animate.path],
        }))
        .pipe(gulp.dest('./dist'))
});
```

You can do a whole bunch of other stuff with animate-stylus-npm when you combine it with jQuery or add your own CSS rules. Dynamically add animations using jQuery with ease:

```stylus
.bounceOutLeft
  animation-name: bounce
  animation-duration: 1s
  animation-fill-mode: both
```

```javascript
$('#yourElement').addClass('bounceOutLeft');
```

You can also detect when an animation ends:

```javascript
$('#yourElement').one('webkitAnimationEnd mozAnimationEnd oAnimationEnd animationEnd', doSomething());
```

##Include/Exclude Animations
There's no need to make custom builds because with Stylus you can import everything you want, and nothing you don't. For example, if you only use the `slideInDown` animation then don't `@import` the whole library - just `@import 'animate-stylus/sliders/slideInDown'`. Or, if you want all the sliders, you can `@import 'animate-stylus/sliders/*'`. See the Stylus Docs for an explanation of [file globbing](http://learnboost.github.io/stylus/docs/import.html#file-globbing).

##Vendor Prefixes
I've left the code unprefixed so you can support whatever browsers you're targeting without having them chosen for you. I recommend using [nib](http://visionmedia.github.io/nib/) or [auto-prefixer](https://github.com/ai/autoprefixer) to add the prefixes.

##Adding Animations with Class Names
First off, making classes like `.bounce` is [unsemantic](http://css-tricks.com/semantic-class-names/) because it states the style (which is the job of CSS), rather than describing what the element is. Your HTML is for content, and your CSS is for style - thus, class names (a feature of HTML) should describe the content, not the style.

But I suppose you don't really care about proper semantics, or you wouldn't be trying to do this. So, if you're really determined, you can add this:

```stylus
//list of animations that we are using
animations = (bounce slideInDown slideOutUp)

.animated
  animation-duration: 1s
  animation-fill-mode: both

for animation_name in animations
  .{animation_name}
    @extends .animated
    animation-name: animation_name
```

And then adding animations to elements with class names will work:

```html
<div class="bounce">This is bouncing</div>
```
