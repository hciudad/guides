# RoundingWell LESS/CSS Style Guide 

```Example
/* comments are best as slash-star for LESS compiler */
/* classes and ids should be lowercase dash-divided, underscores for input names, no camelCasing */
.selector{   /* no space between selector and bracket */
      margin: 10px;            /* property:[space]value; */
      .opacity(10);               /*  mixins for browser prefix should be alphabetical */
      padding: 10px           /* properties should be listed alphabetically */
      .darken(#777, 5%);     /*  other mixins should follow properies */
     &:hover, + div, > p{     /* extending selectors should be below */
          color: @red;          /* use variables.less when possible */
     }
     a{ text-decoration:underline; } /* selectors with only one property should be listed on one line (selector[curly][space][property...;][space][close curly]) */
} /* /.selector */ /* large blocks should have /end comments following the close curly */
```
