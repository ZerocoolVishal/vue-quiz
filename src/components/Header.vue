<template>
  <div>
    <b-nav tabs>
      <b-nav-item disabled>
        <Logo/>
      </b-nav-item>
      <b-nav-item disabled><b>Fancy Quiz App</b></b-nav-item>
      <b-nav-item disabled>Counter 4/10</b-nav-item>
    </b-nav>
  </div>
</template>

<script>

import Logo from './Logo'

export default {
  components: {Logo},
  comments: {
    Logo
  }
}
</script>
