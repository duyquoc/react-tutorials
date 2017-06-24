# [React](http://react.theme1.com) documentation
## Introduction
Welcome! First of all, thank you for purchasing this theme. We prepared a throughout documentation to make your experience as pleasant as possible. We tried to cover every aspect of this theme, however, if you still have any questions or need clarification, feel free to email us via [user's page contact form](http://themeforest.net/user/theme1?rel=theme1#contact).

This theme is built using [Materialize](http://materializecss.com/), a modern responsive front-end framework based on Material Design. Make sure you visit their web-site to learn more about it. Feel free to use all of the elements that framework provides.

## Requirements
This theme requires a pretty basic setup. In fact, the only thing your server needs is PHP installed, which is usually 99.9% of the cases. If you happen to be that 0.1%, please contact your hosting administrator and let him know you need PHP installed on your server. PHP is needed for the Contact form to function, but if you don't need that, any kind of hosting will do the trick.

This theme works great in all of the modern browsers, as well as mobile browsers. It supports Internet Explorer 10+, except for some advanced features, but we've written fallbacks for that.

## Theme installation
Installing our theme is extremely simple — just upload all the files to your server. In fact, you can test your theme locally as well, except for the contact form functionality, which requires a server side language.

## File structure
```
├── assets/
|   ├── build/
│   ├── config/
│   ├── css/
│   ├── font/
│   ├── images/
│   ├── js/
|   |   ├── skins/
├── favicons/
├── libs/
├── mailer/
│   ├── templates/
│   src/
│   ├── jade/
│   ├── sass/
│   |   ├── skins/
```

### `assets`
- `build` contains minified and optimised core `.css` and `.js` files
- `config` contains general JavaScript config file and [Snazzy Maps](http://snazzymaps.com) styles JSON
- `css` contains compiled `react.css` and `linea.css`
- `font` contains the font files
- `images` contains the page's images, divided by category. Put all of your images in this directory, as that's where they get optimised via [Gulp tasks](#tasks)
- `js` contains the core JavaScript file as well as a `skins` directory, containing skin specific JavaScript files

### `favicons`
This directory contains favicons. And a file called `manifest.json`, which you should edit by placing your company's name in it.

### `libs`
The place for the libraries used in this template.

### `mailer`
PHP files that are needed to make the contact form function are located here. In `templates` directory you'll be able to find the predesigned mail templates.

### `src`
#### `jade`
- `./` (i.e. the directory itself) is the home directory of all your `.jade` files, particularly `base.jade` and all of the skin files
- `layout` contains header and footer layouts
- `posts` is a directory for the blog posts
- `projects` is where all your projects and their modals are located
- `section` contains all the sections, which are later included into `base.jade`
- `team-modals` contains team modals. Since team members are shown in a carousel, the modals couldn't share the same parent as their triggers. They need to be placed outside of the carousel.

#### `sass`
- `./` contains the main `react.scss` file as well as all of its components
- `linea` is where Linea icons source is kept
- `skins` contains the skin specific styles

## The layout
The theme is based on block layout. Or block grid, you can call it whatever you like. The fact is, it gives the page this smooth, measured look, unlike masonry grid, which might look a bit messy sometimes. To create these blocks you must follow a defined structure.

First of all, you need to use [Materialize's grid](http://materializecss.com/grid.html) to define the width of your block. Usually you'd start with a row and use a div with `col s12 l6` class in order to make it full width on small devices and half width for medium and large screens.

Then include a div with a corresponding class (`rectangle`, `rectangle-50` or `square`), which will have an image stretch to its whole size (via `background-size: cover`) and finally a div containing your content. The whole thing would look like this:
```html
<div class="row">
  <div class="col s12 l6">
    <div class="rectangle" style="background-image: url(path/to/image)">
      <div class="content">
        Your awesome content
      </div>
    </div>
  </div>
</div>
```

### Extending the layout
You can extend those classes and create your own shapes, say a vertical rectangle. All you need to do is define it in your styles, like this:
```css
.vertical-rectangle {
  padding-bottom: 200%; /* will create a rectangle with height = width * 2 */
}
```
There's no need to specify height of those shapes, since padding will do the trick and size them dynamically, depending on the width. Think of it as of a proportion: `padding-bottom: 100%` will give you a 1:1 square, `padding-bottom: 50%` will give you a 2:1 rectangle.

### Modals
This theme includes a lot of modals for secondary content, like project case study or blog post, as well as detailed modal about your team members.

While occupying quite a lot of rows of code, the overall structure is rather simple. There are two parts of modal.

#### Modal trigger
This will be an `<a>` element, which will act like a layout block. One thing you should notice though, is that it requires `modal-trigger` class and its `href` should point to the `id` of corresponding modal.

Let's take the first project as an example:
```html
<a href="#green-lamp" class="col s12 padding-bottom modal-trigger"> <!-- notice the .modal-trigger class and #green-lamp href -->
    <div style="background-image: url(./assets/images/work/lamp.png)" class="rectangle-50">
        <div class="content valign-wrapper center">
            <div>Green Lamp</div>
        </div>
    </div>
</a>
```

#### Modal window
The modal itself consists of several elements. First of all, it requires the `id`, which is being used in your trigger's `href`, as well as `modal` and `bottom-sheet` classes.

Besides that, the inner structure must include the following elements:
- A close button with particular classes – `modal-close` and `absolute`:
```html
<div class="modal-close absolute">&times;</div>
```
You can also add class `white-text` to make it light, in case you have a dark background.
- Modal cover, the div which also uses previously mentioned block layout:
```html
<div class="modal-cover">
    <div style="background-image: url(./assets/images/work/lamp.png)" class="rectangle-50"></div>
</div>
```
- Modal content, the part where you actually include everything else. It can be anything really. Use block layouts, include texts, quotes, images, videos, etc. Don't forget to include Materialize's grid divs, like `<div class="row">` and `<div class="col s12 m8 l6">` to ensure proper spacing and alignments.

## Contact forms
This theme gives you an ability to choose from two types of form. A "human" version and a classic form.

### Form via HTML
If you're not using Jade, you will have to copy the form container you require from one of the skins.

#### Classic
For classic form use the following, note `id="classic-form"`, that is required:
```html
<div class="col s12 l8 offset-l2">
    <div class="card-panel center hoverable">
        <form id="classic-form" action="mailer/mailer.php" novalidate autocomplete="off" class="row">
          ...
        </form>
    </div>
</div>    
```

#### Human
For human form, you'd need to include these lines, again with obligatory `id="human-form"`:
```html
<div class="col s12 l8 offset-l2">
    <div id="human-form" class="card-panel center hoverable">
      ...  
    </div>
</div>
```
There's no requirement for the `<form>` element for the human one. 

### Form via Jade
If you're using Jade, just include the wanted form inside of your `block vars` by specifying the form type:
```jade
- var formType = 'human'
```

### PHP mailer
In order to make the form work and send you the messages you need to configure it. The config file is placed in `mailer/` directory. Include all of the required information for the PHP mailer to do its magic. You can also specify the email template color in that configuration.

## JavaScript configuration
There's another config file, but this time it's located in `assets/config/` directory. It allows you to modify the [Toast](http://materializecss.com/dialogs.html) messages and their dismissal time.

Besides that you will configure your location to show on Google map. There you will also optionally include a marker and a path to the [SnazzyMaps](https://snazzymaps.com) configuration file. Make sure you place that file inside of the `assets/config/` directory.

## Ajax MailChimp subscription
First, check out the [original repository](https://github.com/scdoshi/jquery-ajaxchimp). There you can find a relatively simple guide on how to make the whole thing work.

Then you can also follow my guide to customise the form and give it a better look. As you choose the embedded form in your list category it will have some code you will need to remove:
- The line that says `<link href="//cdn-images.mailchimp.com/embedcode/slim-*.css" rel="stylesheet" type="text/css">`
- The inline styles `<style type="text/css">...</style>`
- Optionally, you can remove the label `<label for="mce-EMAIL">Subscribe to our mailing list</label>`

Then, you will have to add the following classes:
- `center` to the `div#mce-EMAIL`
- `btn btn-large btn-flat waves-effect waves-light` to `input#mc-embedded-subscribe`

That's it, you should now have a working and styled subscription form.

## Customising the hero animations
Feel free to customise any of the hero sections. Most of them allow you to change the colors as well as behaviours and other configurations. 

Besides that, you can customise the `<h1>` title, the styles for those are found in the `src/sass/skins/*.scss` files or the `assets/css/react.css`, if you prefer to work with the compiled version.

Now, let's walk through each and every hero section to see what and how exactly you can customise those.

### Combustion
The configuration files are `assets/js/combustion-*.js`. You can customise the following parameters:
- Background color
- Bloom
- Draw blur
- Red factor
- Blue factor
- Move factor
- Amount of planets

It's recommended not to change anything else besides those variables.

### Fuzzy
Fuzzy doesn't offer a lot of flexibility JavaScript-wise, but you can change the background color by changing the property for `div.hero`.

### Ring
Ring is a pure CSS animation, so you can head over to the `src/sass/skins/_ring-*.scss` files and change the predefined variables - ring colors and background color. The dimensions are set as the default ones, but they are going to be overwritten by JavaScript in order to fit the screen better.

### Tunnel
Tunnel also doesn't offer that much customising. You can only play around with the title.

### Waves
Check out [Sine Waves repository](https://github.com/isuttell/sine-waves) to learn more about how you can customise those. There's plenty of stuff you can change and don't forget about the background color modification via styles.

## Spinners
You can change the spinner simply by changing the class of div inside of a `div.spinner-container`. You can choose from `spinner-*`, where `*` equals:
- double-dot-in
- dot-in
- double-dot-stick
- dot-stick
- double-dot-out
- dot-out
- wave-in
- double-wave-in
- huge-wave-in
- wave-out
- double-wave-out
- huge-wave-out
- double-section-in
- section-in
- double-section
- section
- double-section-out
- section-out
- double-section-far
- section-far

Check them all out [live on Codepen](http://codepen.io/theme1/pen/OMdqBL).

## Favicons
Favicons are the icons of your web-site that are displayed on various mobile devices. For example, if someone wants to add your site to their home screen, they will view the icon you include. There are quite a few formats you need to handle, inculding iPhone, iPad, Android devices and Microsoft devices. To help you with this process, you can use a touch icons generator web-site, for example [realfavicongenerator.net](http://realfavicongenerator.net).

These icons are placed in `/favicons` directory. Make sure you also edit the `manifest.json` and change the `"Name"` to your company's title.

## Development process
The theme was programmed using two wonderful technologies - [Sass](http://sass-lang.com/) for the styles and [Jade](http://jade-lang.com/) to generate HTML files. As well as [Gulp](http://gulpjs.com/) to help manage those technologies. Gulp is also used to help optimise your resources for the production purpose.

### Sass
> Sass is the most mature, stable, and powerful professional grade CSS extension language in the world.

Writing styles with Sass is a pure pleasure. We've structured React's components to make them easily accessible and editable. The main file is `react.scss`, which contains `@import`s from all of the components, like common styles, buttons, modals, etc.

#### Bourbon
> A simple and lightweight mixin library for Sass.

This library provides a ton of awesome mixins, like prefixes for various properties, which really simplify cross-browser development. Make sure you have a look at [Bourbon docs](http://bourbon.io/docs/) to understand how much this library really does in terms of simplifying styles building.

#### Colors
The color variables are defined in `_constant-colors.scss` file. The reason for its name is that we also include skin file with colors, which are not constant per page. We've also included `_materialize-color.scss` to access the `color('name', 'shade')` function, which is provided by Materialize's source and allows you to easily use the [Material design palette](materializecss.com/color.html#palette).

#### Media query ranges
You can define your own media query ranges for small, middle and large displays. The variables are defined in `_media-query-ranges.scss`.

#### Skin files
In the `skins/` directory you will find customized skins, which customise some of the elements. Since we didn't want to make theme customisation overly complicated, there are only a few predefined things in those files. Although some skins do require a huge addition of the code, e.g. `_ring-*.scss` skins. Feel free to add any overwrites for the default styles in those files.

### Jade
This template engine runs on Node.js and allows you to be very flexible with your HTML layouts. The main file which serves as a skeleton for the page versions is `base.jade`. If you look around, you'll see how it includes various sections and layout components - header and footer, as well as defines the blocks that will be customised in the skin files.

Skins require the `extends base` declaration, in order to actually extend our skeleton. After that you simply define the blocks you need, e.g. the `block title`, which will contain the site title.

The `block vars` contains the body class declaration and the form type (human or classic), after which you have the `block hero` for the first section of the web-site and optional `block skin-script` to include any JavaScript files your skin requires.

### Package managers

#### npm
[npm](https://www.npmjs.com/) is a famous package manager on top of Node.js. Of course, you're going to need [Node.js](https://nodejs.org/en/) installed as well. Fortunately, it's relatively simple to do that, as you have to [download the installer](https://nodejs.org/en/download/) and run it. We've used this to define our dev dependencies, those we need in development process. You can see them in `package.json`.

Run `npm install` to install all of the dev dependencies.

#### Bower
[Bower](http://bower.io/) is another package manager and we've used it to define our non-dev dependencies. Those that are required for the theme to function. The dependencies are listed in `bower.json`.

Run `bower install` to install all of dependencies.

#### Composer
[Composer](https://getcomposer.org) is used to fetch [PHPMailer](https://github.com/PHPMailer/PHPMailer). Feel free to add any PHP dependecies via this package manager.

### Gulp
Gulp does so many things. First, it allows us to compile our source code into usable assets. Secondly, it optimises those assets for the production. All of the commands and configurations are located in `gulpfile.js`.

#### Gulp installation
Gulp is installed via npm.

Following the [Getting started with Gulp](https://github.com/gulpjs/gulp/blob/master/docs/getting-started.md) guide, run `npm rm --global gulp` to remove any previous versions. Then run `npm install --global gulp-cli` to install it globally or `npm install --save-dev gulp` to install it as a dev dependency of the project. 

It also ensures you're not going to have any conflicts with the previous version of Gulp.

#### Plugins
There's a number of plugins Gulp uses to run the required tasks, you can see those on the first lines of `gulpfile.js` as well as in `package.json` under `devDependencies`.

#### Tasks
The tasks themselves are pretty self-explanatory, we've also made sure to comment the file properly. There are:
- `gulp sass` to build `react.css` from `react.scss`, as well as compile `linea.css` from `linea.scss`, using source maps.
- `gulp build:css` to create `build.min.css`, which is optimised with cssnano and css-mqpacker. The file is placed in `assets/build/` directory. **Note**: This command depends on `gulp sass`, run it first.
- `gulp jade` to build the html files. You need to specify which files you want to compile. This task also beautifies the html, making it more readable and easier to modify
- `gulp watch` that watches for the changes in your scss files, as well as jade files and runs appropriate commands (`sass` and `jade`) accordingly
- `gulp build:scripts` to create `build.min.js`, consisted of the majority of JavaScript files. The file is placed in `assets/build/` directory.
- `gulp minify-skin-scripts` minifies the scripts in `assets/js/skins/` and places them in `assets/js/skins/min/` directory
- `gulp imagemin` to optimise the images found in `assets/images/` directory

## Code quality tools
To ensure the consistency of code as well as its best practices we've decided to use linters. [ESLint](http://eslint.org) for JavaScript and [scss-lint](https://github.com/brigade/scss-lint) for Sass.

### ESLint
This linter is very powerful and configurable. Write JavaScript like a pro, ESLint will give you hints and mark obvious errors. Check out the configuration file – `.eslintrc` to see how we configured this project.

### scss-lint
Writing styles can be quite difficult. Do you always remember the correct order of your properties, what goes first, an `@include` or `position`? Can you track whether the rules have been rightly nested or if you've used correct spacing? scss-lint is the answer :relieved: 

See our configuration file – `.scss-lint.yml`.
