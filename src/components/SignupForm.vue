<template>
  <form @submit.prevent="handleSubmit">
    <label>Email:</label>
    <input type="Email" required v-model="email">
    <label>Password:</label>
    <input type="Password" required v-model="Password">
    <div v-if="passwordError" class="error">{{ passwordError }}</div>
    <label>Role:</label>
    <select v-model="role">
        <option value="developer">Web Developer</option>
        <option value="designer">Web Designer</option>
    </select>
    <label>Skills:</label>
    <input type="text" v-model="tempSkill" @keyup.alt=addSkill>
    <div v-for="skill in skills" :key="skill" class="pill">
    <span @click="deleteSkill(skill)">{{ skill }}</span>
    </div>
    <div class="terms">
        <input type="checkbox" v-model="terms">
        <label>Accept terms and conditions</label>
    </div>

    <div class="submit">
        <button>Create sccount</button>
    </div>
  </form>
  <p>Email:{{ email }}</p>
  <p>Password: {{ Password }}</p>
  <p>Role: {{ role }}</p>
  <p>Terms accepted: {{ terms }}</p>
  <p>Names: {{ names }}</p>
</template>

<script>
export default {
    data(){
        return{
            email:'',
            Password:'',
            role:'developer',
            terms: false,
            tempSkill: '',
            skills:[],
            passwordError:'',
        }
    },
    methods:{
        addSkill(e){
            if(e.key == "," && this.tempSkill){
                if(!this.skills.includes(this.tempSkill)){
                    this.skills.push(this.tempSkill)
                }
                this.tempSkill = ''
            }
        },
        deleteSkill(skill){
            this.skills = this.skills.filter((item) => {
                return skill !== item
            })
        },
        handleSubmit(){
            this.passwordError = this.Password.length >5 ? '' :
            " password must ba at least 6 chars long"
        }
    }
}
</script>

<style>
button{
    background: #0d6dff;
    border: 0;
    padding: 10px 20px ;
    margin-top:20px;
    color: #Fff;
    border-radius: 20px;
}
.submit{
    text-align: center;
}
form{
    max-width: 420px;
    margin: 30px auto;
    background: white;
    text-align: left;
    padding: 40px;
    border-radius: 10px;
}
label{
    color: #aaa;
    display: inline-block;
    margin: 25px 0 15px;
    font-size: 0.6em;
    text-transform: uppercase;
    letter-spacing: 1px;
    font-weight: bold;
}
input ,select{
    display: block;
    padding: 10px 6px ;
    width: 100%;
    box-sizing: border-box;
    border: none;
    border-bottom: 1px solid #ddd;
    color: #555;
}
input[type="checkbox"]{
    display: inline-block;
    width: 16px;
    margin: 0 10px 0 0 ;
    position: relative;
    top: 2px;
}
.pill{
    display: inline-block;
    margin: 20px 10px 0 0;
    padding: 6px 12px ;
    background: #eee;
    border-radius: 20px;
    font-size: 12px;
    letter-spacing: 1px;
    font-weight: bold;
    color: #777;
    cursor: pointer;
}
.error{
    color: #ff0062;
    margin-top: 10px;
    font-size: 0.8em;
    font-weight: bold;
}
</style>