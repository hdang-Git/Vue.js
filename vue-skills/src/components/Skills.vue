<template>
  <!-- <div class="hello">
    {{name}}
    {{btnState ? 'The button is disabled' : 'The button is active'}}
    <button @click = changeName :disabled="btnState"> Change Name </button>
  </div> -->

  <div class="hello">
    <div class="holder">
      <form @submit.prevent="addSkill">
        <input type="text" placeholder="Enter a skill you have..." v-model="skill" v-validate="'min:5'" name="skill" >
        <transition name="alert-in" enter-active-class="animated flipInX" leave-active-class="animated flipOutX">
          <p class="alert" v-if="errors.has('skill')"> {{errors.first('skill')}}</p>
        </transition>

        <!-- {{skill}} -->
        <!-- <input type="checkbox" id="checkbox" v-model="checked"> -->
      </form>

      <ul >
        <transition-group name="list" enter-active-class="animated bounceInUp" leave-active-class="animated bounceOutDown">
          <li v-for="(data, index) in skills" :key = 'index'> 
            <!-- {{index}} .  -->
            {{data.skill}}
            <i class="fa fa-minus-circle" @click="remove(index)"></i>
          </li>
        </transition-group>
      </ul>


      <!-- <p v-if="skills.length >= 1"> You have more than 1 skill. </p>
      <p v-else>You have less than or equal to 1 skill.</p> -->

      <!-- <div :class="{ alert: showAlert, 'another-class': showClass}"></div> -->
      <!-- <div v-bind:class="{alertObject}"></div> -->
      <!-- <div :style="{backgroundColor: bgColor, width: bgWidth, height: bgHeight}"></div> -->

      
        <p>These are the skills that you possess.</p>

    </div>
  </div>

</template>

<script>
export default {
  name: 'Skills',
  data() {
    return {
      // name: 'Coursetro',
      // btnState: true
      skill: '',
      // checked: false,
      skills: [
        {"skill" : "Vue.js"},
        {"skill" : "Frontend Developer"}
      
      ],

      // showAlert: true,
      // showClass: true

      // alertObject: {
      //   alert: true
      // }

      // bgColor: 'yellow',
      // bgWidth: '100%',
      // bgHeight: '30px'
    }
  },
  props: {
  },
  methods: {
    addSkill() {
      this.$validator.validateAll().then((result) => {
        if(result){
          this.skills.push({skill: this.skill});
          this.skill = '';
        } else {
          console.log('Not valid');
        }
      })
      
      // console.log("This checkbox value is: " + this.checked);
    },
    remove(id) {
      this.skills.splice(id, 1);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style src="./Skills.css" scoped>
</style>
