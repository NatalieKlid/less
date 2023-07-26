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