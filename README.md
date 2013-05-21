# RoundingWell Guides

## Javascript Style Guide

[RoundingWell Javascript Style Guide](https://github.com/RoundingWell/style-guides/blob/master/javascript.md)

*A mostly reasonable approach to JavaScript based on javascript by airbnb*

---

## Javascript Organization

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

---

## LESS/CSS Style Guide

[RoundingWell LESS/CSS Style Guide](https://github.com/RoundingWell/style-guides/blob/master/lesscss.md)

---

## LESS/CSS Organization

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

---

## Font Icon

## Design
