<template>
<div class="hello">
  <h2 v-if="isLoaded">{{ computeRadius }}</h2>
  <button v-if="isLoaded" @click="changeSphere"> change sphere </button>
  <h2 v-else>Loading rhino3dm...</h2>
</div>
</template>

<script>
import Vue from 'vue';
import rhino3dm, { Sphere } from 'rhino3dm';

export default Vue.extend({
  name: 'HelloWorld',
  data() {
    return {
      sphere: Sphere,
      isLoaded: false
    }
  },
  created() {
    rhino3dm().then(Rhino => {
      var rad = Math.ceil(Math.random() * 1000);
      var sphere = new Rhino.Sphere([0,0,0],rad);
      this.sphere = sphere;
      this.isLoaded = true;
    });
  },
  methods: {
    changeSphere: function() {
      rhino3dm().then(Rhino => {
        var rad = Math.ceil(Math.random() * 1000);
        var sphere = new Rhino.Sphere([0,0,0],rad);
        this.sphere = sphere;
        this.isLoaded = true;
      });
    }
  },
  computed: {
    computeRadius: function() {
      return `${this.sphere.radius}`
    }
  }
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
