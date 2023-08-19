<template>
    <!--Handling submission-->
    <!--The 'prevent' modifier is used to prevent the form from refreshing on submission-->
    <form @submit.prevent="handleSubbmit">
        <label>Email: </label>
        <input type="text" required v-model="email">

        <label>Password: </label>
        <input type="password" required v-model="password">
        <div v-if="passwordError" class="error">{{ passwordError }}</div>

        <label>Role: </label>
        <select v-model="role">
            <option value="developer">Web developer</option>
            <option value="designer">Web designer</option>
        </select>

        <label>Skills: </label>
        <input type="text" v-model="tempSkill" @keyup.alt="addSkill">
        <div v-for="skill in skills" :key="skill" class="skill">
           <span @click="deleteSkill(skill)"> {{ skill }}</span>
        </div>

        <div class="terms">
            <input type="checkbox" v-model="terms" required>
            <label>Accept terms and conditions</label>
        </div>

        <div class="submit">
            <button>Create an Account</button>
        </div>
    </form>
    <p>Email: {{ email }}</p>
    <p>Password: {{ password }}</p>
    <p>Role: {{ role }}</p>
    <p>Terms accepeted: {{ terms }}</p>
</template>

<script>
    export default {
        data(){
            return{
                email: "",
                password: "",
                role: "",
                terms: false,
                tempSkill: "",
                skills: [],
                passwordError: ""
            }
        },
        methods: {
            addSkill(e){
                if (e.key === ',' && this.tempSkill) {
                    if (!this.skills.includes(this.tempSkill)) {
                        this.skills.push(this.tempSkill)
                    }
                    this.tempSkill = ''
                }
            },
            deleteSkill(skill){
                this.skills = this.skills.filter((item)=> {
                    return skill !== item
                })
            },
            handleSubbmit(){
                //Validating the password
                this.passwordError = this.password.length > 5? "" : "Password must be at least 5 characters long"
                if (!this.passwordError) {
                    console.log("email: ", this.email)
                    console.log("password: ", this.password)
                    console.log("role: ", this.role)
                    console.log("skills: ", this.skills)
                    console.log("terms accepted: ", this.terms)
                }
            }
        }
    }
</script>

<style>
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
        font-size: 0.6rem;
        text-transform: uppercase;
        letter-spacing: 1px;
        font-weight: bold;
    }
    input, select{
        display: block;
        padding: 10px 6px;
        width: 100%;
        box-sizing: border-box;
        border: none;
        border-bottom: 1px solid #ddd;
        color: #555;
    }
    input[type="checkbox"]{
        display: inline-block;
        width: 16px;
        margin: 0 10px 0 0;
        position: relative;
        top: 2px;
    }
    .skill{
        display: inline-block;
        margin: 20px 10px 0 0;
        padding: 6px 12px;
        background: #eee;
        border-radius: 20px;
        font-size: 12px;
        letter-spacing: 1px;
        font-weight: bold;
        color: #777;
        cursor: pointer;
    }
    .submit{
        text-align: center;
    }
    button{
        background: #0b6dff;
        border: 0;
        padding: 10px 20px;
        margin-top: 20px;
        color: white;
        border-radius: 20px;
    }
    .error{
        color: #ff0e62;
        margin-top: 10px;
        font-size: 0.8rem;
        font-weight: bold;
    }
</style>