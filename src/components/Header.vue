<template>
  <div>
    <b-nav tabs>
      <b-nav-item disabled>
        <Logo/>
      </b-nav-item>
      <b-nav-item disabled><b>Fancy Quiz App</b></b-nav-item>
      <b-nav-item disabled>Counter {{ numCorrect }}/{{ numTotal }}</b-nav-item>
    </b-nav>
  </div>
</template>

<script>

import Logo from './Logo'

export default {
  components: {Logo},
  comments: {
    Logo
  },
  props: {
    numCorrect: Number,
    numTotal: Number
  }
}
</script>
