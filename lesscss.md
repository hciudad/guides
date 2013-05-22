# RoundingWell LESS/CSS Style Guide{

 *A mostly reasonable approach to LESS/CSS*

## <a name='TOC'>Table of Contents</a>

  1. [Example](#example)
  1. [Resources](#resources)
  1. [License](#license)

## <a name='example'>Example</a>

*The following is LESS using CSS markdown,  some coloring is not correct*

```css
/* comments are best as slash-star for LESS compiler */
/* classes and ids should be lowercase dash-divided, underscores for input names, no camelCasing */
.selector{   /* no space between selector and bracket */
	margin: 10px;				/* property:[space]value; */
	.opacity(10);				/* mixins for browser prefix should be alphabetical */
	padding: 10px;				/* properties should be listed alphabetically */
	.darken(#777, 5%);			/* other mixins should follow properies */
	&:hover, + div, > p{		/* extending selectors should be below */
		color: @red;			/* use variables.less when possible */
		line-height: 1.4;		/* line-height should not be given units */
		padding: 10px 5px 0;	/* shorthand should be used when possible */
	}
    a{ text-decoration: underline; } /* selectors with only one property should be listed on one line (selector[curly][space][property...;][space][close curly]) */
} /* /.selector */ /* large blocks should have /end comments following the close curly */
```

  **[[⬆]](#TOC)**

## <a name='resources'>Resources</a>

**Read This**
  - [Scalable and Modular Architecture for CSS](http://smacss.com/)

**Other Styleguides**
  - [Google HTML/CSS Style Guide](http://google-styleguide.googlecode.com/svn/trunk/htmlcssguide.xml#CSS_Style_Rules)
  - [Principles of writing consistent, idiomatic CSS](https://github.com/necolas/idiomatic-css)
  - [Thinkup - Code Style Guide: CSS](https://github.com/ginatrapani/ThinkUp/wiki/Code-Style-Guide:-CSS)

**LESS Resources**
  - [LESS](http://lesscss.org/)
  - [LESSphp Compiler](http://leafo.net/lessphp/)


**[[⬆]](#TOC)**

## <a name='license'>License</a>

(The MIT License)

Copyright (c) 2013 RoundingWell

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
'Software'), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY
CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

  **[[⬆]](#TOC)**

# }
