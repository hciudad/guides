# RoundingWell Guides

## <a name='TOC'>Table of Contents</a>

### Backend:
  1. [Code Style Guide](#code-style-guide)
  1. [Organization](#backend-organization)

### Frontend:
  1. [Javascript Style Guide](#javascript-style-guide)
  1. [Javascript Organization](#javascript-organization)
  1. [LESS/CSS Style Guide](#lesscss-style-guide)
  1. [LESS/CSS Organization](#lesscss-organization)
  1. [Font Icon](#font-icon)
  1. [Design Specifications](#design-specifications)

## <a name='code-style-guide'>Code Style Guide</a>

[RoundingWell Code Style Guide](https://github.com/RoundingWell/guides/blob/master/code.md)

*A mostly reasonable approach to code style*

Taken from style guides for: airbnb, kohana, pear

**[[⬆]](#TOC)**

## <a name='backend-organization'>Code Organization</a>

[Code Organization Guide](https://github.com/RoundingWell/guides/blob/master/organization.md)

What goes where in which class? 

**[[⬆]](#TOC)**

## <a name='javascript-style-guide'>Javascript Style Guide</a>

[RoundingWell Javascript Style Guide](https://github.com/RoundingWell/guides/blob/master/javascript.md)

*A mostly reasonable approach to JavaScript based on javascript by airbnb*

**[[⬆]](#TOC)**

## <a name='javascript-organization'>Javascript Organization</a>

Ideally app specific code and exceptions only exist at the lowest level. For example:  Global -> Desktop Global -> Desktop Provider
If at all possible no code specifically related to the provider side desktop app should be found in either Desktop Global or Global.

### mainapp JS *(/opt/code/mainapp/assets/js)*
+ **desktop-provider.js** *(objDesktop)*
+ **mobile-provider.js** *(objMobile)*
+ **provider.js**  *(objProvider)* - Any js shared by desktop and mobile provider apps

### shared JS *(/opt/code/shared/assets/js)*
+ **debug.js**  - Additional tool for debugging.  Useful in situations where you cannot get a debug panel (ie: BB6/7, older Android)
+ **desktop.js** *(objGlobals.objDesktop)* - Any js shared by desktop provider and patient apps
+ **global.js** *(objGlobals)*  - Any js shared by everything
+ **html5shiv.js (IE8)**
+ **jquery.datepicker.modified.js / ...min.js**  - (desktop non-iOS)
+ **jquery.js** - 1.9.1  fallback for the google CDN jquery
+ **jquery.password-strength.js / ...min.js**
+ **jquery.placeholder.js / ...min.js**  *(desktop / IE8/9)* - handles placeholder text for IE8
+ **jquery.tappable.js / ...min.js** *(mobile)* - handles touch targets for mobile  (not iPad)
+ **lte-ie7.js** - This is deprecated IE7 JS for handling the webfont
+ **mobile.js** *(objGlobals.objMobile)* - Any js shared by mobile provider and patient apps
+ **qunit.js** - Unit testing

### surveyapp JS  *(/opt/code/surveyapp/assets/js)*
+ **desktop-patient.js** *(objDesktop)*
+ **mobile-patient.js**  *(objMobile)*
+ **patient.js** *(objPatient)* - Any js shared by desktop and mobile provider apps
+ **tests.js** - Some tests for the weight algorithm

**[[⬆]](#TOC)**


## <a name='lesscss-style-guide'>LESS/CSS Style Guide</a>

[RoundingWell LESS/CSS Style Guide](https://github.com/RoundingWell/guides/blob/master/lesscss.md)

*A mostly reasonable approach to LESS/CSS*

**[[⬆]](#TOC)**


## <a name='lesscss-organzation'>LESS/CSS Organization</a>

All shared less files are imported by apps and not accessed directly.  If any changes are made to a shared less file, the app LESS file must have the modified date changed to trigger a new asset merge

### mainapp LESS (/opt/code/mainapp/assets/less)
+ **desktop-provder.less**
+ **mobile-provider.less**
+ **ie-all-provider.less**

### shared LESS (/opt/code/shared/assets/less)
+ **alert-dialog.less**
+ **buttons.less**
+ **desktop-forms.less**
+ **desktop.less**
+ **error-page.less**
+ **font-icons.less**
+ **global.less**
+ **grid.less**
+ **icons.less**
+ **ie-all.less**
+ **messaging.less**
+ **mixins.less**
+ **mobile-animations.less**
+ **mobile-forms.less**
+ **mobile.less**
+ **modals.less**
+ **pretty-inputs.less**
+ **progress-bar.less**
+ **tablet.less**
+ **tabs.less**
+ **tooltips.less**
+ **variables.less**
+ **zebra-datepicker.less**

### surveyapp LESS (/opt/code/surveyapp/assets/less)
+ **desktop-patient.less**
+ **mobile-patient.less**
+ **ie-all-provider.less**

**[[⬆]](#TOC)**


## <a name='font-icon'>Font Icon</a>

*Instructions for updating and maintaining*

[http://icomoon.io/app/#browse](http://icomoon.io/app/#browse)

You may need to reimport the roundingwell.dev.svg font found in the fonts folder on dropbox

Inside the source icon svgs there's a [template pdf](https://www.dropbox.com/s/kneekii66xs7px6/template.pdf?v=1mcis) for making new SVGs.  You should use SVG 1.0 format when saving and the vector should be a single color path or compound path with no stroke.

Fonts are relatively organized by character codes.

When making an update you should:

+ Download the font and replace all of the files in dropbox.
+ Update any modified .font-icon- classes at the bottom of @font-face
+ Update icons object lte-ie7.js in shared js  [DEPRECATED]
+ Copy font files to shared/font/roundingwell

**[[⬆]](#TOC)**


## <a name='design-specifications'>Design Specifications</a>

*TODO*

**[[⬆]](#TOC)**

