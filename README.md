# BEM-parent-selector
SASS / SCSS mixin for adding selectors into parent using &amp; and without duplicating selectors before parent

## Quick start

Several quick start options are available:

- Clone the repo: `git clone https://github.com/Darex1991/BEM-parent-selector`
- Install with npm: `npm install bem-parent-selector`
- Install with yarn: `yarn add bem-parent-selector`

## Examples

### In normal SCSS/SASS file code:
````
.calendar-container--theme-third {
  .calendar-reservation {
    &__checkout-wrapper:not(&--modifier):before {
      content: 'abc';
    }
  }
}

````

will be parsed to:

````
.calendar-container--theme-third .calendar-reservation__checkout-wrapper:not(.calendar-container--theme-third .calendar-reservation--modifier):before {
  content: 'abc';
}
````

so when U need to use ie. `not` with ampersand U will get the whole parent selector

`:not(.calendar-container--theme-third .calendar-reservation--modifier)`

instead of the last parent in `&` place

`:not(.calendar-reservation--modifier)`

This mixin gives you an option to add selector only for the last parent. 

````
.calendar-container--theme-second-2 {
  .calendar-reservation {
    @include BEM-parent-selector('&__checkout-wrapper:not(&--modifier):before') {
      content: 'abc';
    }
  }
}
````

will be parsed to:

````
.calendar-container--theme-second-2 .calendar-reservation__checkout-wrapper:not(.calendar-reservation--modifier):before {
   content: 'abc';
 }
````


## another example with many selectors:

````
.calendar-container--theme-second-2 {
  .calendar-reservation {
    @include BEM-parent-selector('&__checkin-wrapper:before', '&__checkout-wrapper:not(&--modifier):before', '.cos-wrapper:before') {
      content: 'abc';
    }
  }
}
````
will be parsed to:

```

.calendar-container--theme-second-2 .calendar-reservation__checkin-wrapper:before,
.calendar-container--theme-second-2 .calendar-reservation__checkout-wrapper:not(.calendar-reservation--modifier):before,
.calendar-container--theme-second-2 .calendar-reservation '.cos-wrapper:before' {
  content: 'abc';
}
````
