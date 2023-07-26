# LESS
Repo to learn and practice LESS

# Variables
### syntacsis

```
    @regularFontSize: 20px;

    header {
        font-size: @regularFontSize; // Note: SCSS uses $ for variables
    }
```

It is possible to do math operations with variables:

```
    @regularFontSize: 20px;

    header {
        font-size: @regularFontSize+10; // result: 30px; Note: SCSS can do this too
    }
```

# Nesting selectors

Works exactly the same as for SCSS

# Mixins
Are used to define a set of rules that can be then applied to a selector. Note: they work the same way as mixins in SCSS, the syntacsis is different, simpler.

### syntacsis

```
    .regularText(@fontWeight) {
        font-size: 16px;
        color: #00000f;
        font-family: 'Arial', sans-serif;
        font-weight: @fontWeight;
    }

    header {
        .regularText(400);
    }
```

Note: a use-case for mixins: defining vendor-prefixes for rules that need them. Example:

```
    .border-radius(@radius) {
        -webkit-border-radius: @radius;
        -moz-border-radius: @radius;
        -o-border-radius: @radius;
        -ms-border-radius: @radius;
        border-radius: @radius;
    }

    .box {
        .border-radius(10px);
    }
```

Note: mixins can be used inside other mixins (this works in SCSS too):

```
    .regularText {
        font-size: 16px;
        font-family: 'Arial', sans-serif;
        .red; // mixin inside mixin
    }

    .red {
        color: red;
    }

    header {
        .regularText;
    }
```

It is possible to set a default value for a mixin taking parameters:

```
    .border-radius(@radius: 10px) {
        -webkit-border-radius: @radius;
        -moz-border-radius: @radius;
        -o-border-radius: @radius;
        -ms-border-radius: @radius;
        border-radius: @radius;
    }

    .box {
        .border-radius; // default of 10px is applied
    }
```

Mixins can accept multiple parameters:

```
    .border(@width:1px, @style: solid, @color: #000){
        border: @width @style @color;
    }

    .box {
        .border; // apply border mixin with default parameters
    }
```

# Guarded mixins
Mixins with condition

```
.set-text-color (@bg-color) when (lightness(@bg-color) >= 50%) { 
  color: @dark;
  background: @bg-color;
}

.set-text-color (@bg-color) when (lightness(@bg-color) < 50%) { 
  color: @light;
  background: @bg-color;
}

    header {
        .set-text-color(#000); // 2nd rule will be applied
    }
    footer {
        .set-text-color(#fff); // 1st rule will be applied
    }
```

# Built-in functions

```

    @colorToUse: #f3c;

    color: lighten(@colorToUse, 20%);
    color: darken(@colorToUse, 20%);

```

[Full reference for built-in functions](https://lesscss.org/functions)

# Importing files

Use case: it is a good practice to define all mixins and variables in one file and then import it to the others with the @import directive

```
    @import url(https://maxcdn.bootstrapcdn.com/bootstrap/3.3.1/css/bootstrap.min.css);
```