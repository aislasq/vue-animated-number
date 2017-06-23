# AnimatedNumber

Simple animation for numbers in VueJS using an exponential function. (The increments get smaller as they reach the final value).

## Installation
```
$ npm install https://github.com/aislasq/vue-animated-number.git
```

## Usage

#### Props:

* **goal:** The number to which the animation will reach. Required.
* **outOff:** The max number it could achieve ( number / outOff ). Not required.
* **mainClass:** The classes for the \<p> holding the number. Not required.
* **seconds:** The amount of seconds the animation will run. Default 1 seconds.

#### Methods: 

* **on-finish:** Called after the animation has finished with the display value.
* **on-update:** Call after the value is updated with the current display value.

```vue
<template>
    <animated-number :goal="value"
                     :out-off="maxVal"
                     :seconds="seconds"
                     @on-update="val => onUpdate(val)"
                     @on-finish="val => onFinish(val)">
    </animated-number>
</template>

<script>
import AnimatedNumber from 'vue-animated-number';

export default {
  components: {
    'animated-number': AnimatedNumber
  }
  data: function(){
    value: 100, 
    seconds: 3,
    maxVal: 250
  },
  methods: {
    onFinish: function(value){
      console.log('Finished with value of: ' + value);
    },
    onUpdate: function(value){
      console.log('Updated with value of: ' + value);
    }
  }
}
</script>
```

## TODO

* Allow negatives.

## Badges

![](https://img.shields.io/badge/license-MIT-blue.svg)
![](https://img.shields.io/badge/status-stable-green.svg)
