<template>
  <div class="hello">
    <div class="holder">
      <form @submit.prevent="addSkill">
        <input type="text" placeholder="Enter skill you have.." v-model="skill" v-validate="'min: 5'" name="skill">
        <transition name="alert-in" enter-active-class="animated rollIn" leave-active-class="animated flipOutX">
          <p class="alert" v-if="errors.has('skill')">{{ errors.first('skill') }}</p>
        </transition>
      </form>
      <ul>
        <transition-group name="list" enter-active-class="animated bounceInUp" leave-active-class="animated bounceOutDown">
          <li v-for="(data, index) in skills" :key="index">
            {{ data.skill }} 
            <i class="fa fa-minus-circle" @click="remove(index)"></i></li>
        </transition-group>
      </ul>
      <p>These are the skills that you possess</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Skills',
  data() {
    return {
      skill: '',
      skills: [
        { 'skill': 'Vue.js'},
        { 'skill': 'Node.js'}
      ]
    }
  },
  methods: {
    addSkill() {
      this.$validator.validateAll()
        .then((result) => {
          if(result) {
            this.skills.push({skill: this.skill})
            this.skill = ''
          }
        })
    },
    remove(id) {
      this.skills.splice(id, 1)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import url('https://cdnjs.cloudflare.com/ajax/libs/animate.css/3.7.0/animate.css');
@import url("https://use.fontawesome.com/releases/v5.3.1/css/all.css");

   .holder {
    background: #fff;
  }

  ul {
    margin: 0;
    padding: 0;
    list-style-type: none;
  }
  
  ul li {
    padding: 20px;
    font-size: 1.3em;
    background-color: #E0EDF4;
    border-left: 5px solid #3EB3F6;
    margin-bottom: 2px;
    color: #3E5252;
  }

  p {
    text-align:center;
    padding: 30px 0;
    color: gray;
  }

  .container {
    box-shadow: 0px 0px 40px lightgray;
  }
  input {
    width: calc(100% - 40px);
    border: 0;
    padding: 20px;
    font-size: 1.3em;
    background-color: #323333;
    color: #687F7F;
  }
  .alert {
    background: #fdf2ce;
    font-weight: bold;
    display: inline-block;
    padding: 5px;
    margin-top: -20px;
  }

  i {
    float: right;
    cursor: pointer;
  }
</style>
