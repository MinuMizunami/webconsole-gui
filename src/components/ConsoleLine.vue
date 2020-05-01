
<template>
    <div class="checkbox-wrapper" @click="check">
        <form
            @submit="checkForm"
            action="http://127.0.0.1:8000/cmd"
            method="post"
        >
            <span>
                <label for="cmd">cmd # -> </label>
                <input ref="cmd" id="cmd"  v-model="cmd" type="text" name="cmd" :disabled="result">
                <p>{{ result }}</p>
            </span>
            
        </form>
    </div>
</template>
<script>
import axios from 'axios';

export default {

  data() {
    return { 
        checked: false,
        cmd: null,
        result: null
    }
  },
  methods: {
    check() { this.checked = !this.checked; },
    submit(e) {
        
        const vm = this;
        console.log("submit");
        e.preventDefault();
        var args = this.cmd.split("-");
        var cmd = args[0]
        args = args.slice(1);
        var jArgs= Object();
        for(let arg of args){
            let tmp = arg.split(" ");
            jArgs[tmp[0]] = tmp[1];
        }
        //axios.post(e.target.action+"/"+this.cmd, {"-p": "asd","-t": "asd"} ) 
        axios.post(e.target.action+"/"+cmd, jArgs )
        .then(function (response) {  
            vm.result = response.data;
            vm.terminateLine();
        })
        .catch(function (error) {         
            console.log(error);
            vm.terminateLine();
        });
    

    },
    checkForm(e) {
        console.log("check");
        this.submit(e);
        e.preventDefault();
    },
    terminateLine(){
        console.log("event child");
        this.$emit('cmdexec');
    }
  },
  mounted () {
      
  },
  name: 'ConsoleLine'

};
</script>