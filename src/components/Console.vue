<template>
    <div ref="container" >
      <ConsoleLine v-for='line in lines' :key="line" @cmdexec="addLine" />
    </div>
</template>
<script>

import ConsoleLine from './ConsoleLine.vue'
//import Vue from 'vue'

export default {
  name: 'Console',
  components: {
    ConsoleLine
  },
  data() {
    return { 
        lines: [1]
    }
  },
  methods: {
    addLine () {
      this.lines.push(this.lines[this.lines.length - 1]+1);
      /*
        var ComponentClass = Vue.extend(ConsoleLine)
        var instance = new ComponentClass({
            propsData: { type: 'primary' }
        })
        instance.$slots.default = ['']
        instance.$mount() // pass nothing
        console.log("event parent");
        this.$refs.container.appendChild(instance.$el)
        */
    }
  }
};
</script>