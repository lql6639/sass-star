<!--
  * @FileDescription: Sass星空
  * @Author: liqinglin
-->

<template>
    <div class="layer1"></div>
    <div class="layer2"></div>
    <div class="layer3"></div>
    <div class="title">{{ title }}</div>
</template>

<script>
export default {
  name: 'App',
  data () {
    return {
      title: 'Sass星空'
    }
  }
}
</script>

<style lang="scss">
html {
  height: 100%;
  background: radial-gradient(ellipse at bottom, #1b2735 0%, #090a0f 100%);
  overflow: hidden;
}

.title {
  position: absolute;
  top: 50%;
  left: 0;
  right: 0;
  color: #fff;
  text-align: center;
  font-family: 'Lato', sans-serif;
  font-size: 4em;
  font-weight: 300;
  letter-spacing: 10px;
  margin-top: -40px;
  padding-left: 10px;
  background: linear-gradient(white, #38495a);
  background-clip: text;
  color: transparent;
}

// 颜色列表
$list: #fff;

@function getShadows($n) {
  $random-color: random(length($list));
  $shadows: '#{random(100)}vw #{random(100)}vh #{nth($list, $random-color)}';

  @for $i from 2 through $n {
    $shadows: '#{$shadows},#{random(100)}vw #{random(100)}vh #{nth($list, $random-color)}';
  }

  @return unquote($shadows);
}

$duration: 200;
$count: 500;

@for $i from 1 through 3 {
  $duration: floor(calc($duration / 2));
  $count: floor(calc($count / 2));

  .layer#{$i} {
    $size: #{$i}px;
    position: fixed;
    width: $size;
    height: $size;
    border-radius: 50%;
    left: 0;
    top: 0;
    box-shadow: getShadows($count);
    animation: moveUp #{$duration}s linear infinite;

    &::after {
      content: '';
      position: fixed;
      left: 0;
      top: 100vh;
      width: $size;
      height: $size;
      border-radius: inherit;
      box-shadow: inherit;
    }
  }
}

@keyframes moveUp {
  100% {
    transform: translateY(-100vh);
  }
}
</style>
