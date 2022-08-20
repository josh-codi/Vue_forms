<template>
    <form @submit.prevent="handleSubmit">
        <label for="email">Email</label>
        <input type="text" name="email" id="email" v-model="email" required>

        <label for="password">Password</label>
        <input type="password" name="password" id="password" v-model="password" required>

        <div v-if="passwordError">{{ passwordError}}</div>

        <label for="role">Role</label><br>
        <select name="role" id="role" v-model="role">
            <option value="developer">Web Developer</option>
            <option value="designer">Web Desiginer</option>
        </select>


        <label for="skill">Skills</label>
        <input type="text" v-model="tempSkill" @keyup="addSkill">

        <div v-for="skill in skills" :key="skill" class="skill" @click="deleteSkill">
            {{ skill }}
        </div>


        <div class="terms">
            <input type="checkbox" name="" required v-model="terms">
            <label>Accept terms and conditions</label>
        </div>

        <!-- <div>
            <input type="checkbox" value="Josh" v-model="names">
            <label>Josh</label>
        </div>
        <div>
            <input type="checkbox" value="Debby" v-model="names">
            <label>Debby</label>
        </div>
        <div>
            <input type="checkbox" value="Emma" v-model="names">
            <label>Emma</label>
        </div> -->


    <div class="submit">
        <button>Create an Account</button>
    </div>


    </form>
</template>

<script>
export default {
    data(){
        return {
            email: '',
            password: "",
            role: 'designer',
            terms: false,
            tempSkill: '',
            skills: [],
            passwordError: ''
        }
    },
    methods: {
        addSkill(e){
            if(e.key === ',' && this.tempSkill) {
                this.tempSkill = this.tempSkill.replace(/,/g, "")
                if(!this.skills.includes(this.tempSkill)){
                    this.skills.push(this.tempSkill)
                }                
                this.tempSkill = ''
            }
        },
        deleteSkill(e){
            this.skills.forEach((val, idx)=>{
                if (val === e.target.innerText) {
                    this.skills.splice(idx, 1)
                }
            })
        },
        handleSubmit(e){
            this.passwordError = this.password.length > 5 ? '' : 'Password must be at least 6 characters long'
        }
    }

    
}
</script>

<style scoped>
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
.skill {
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
button{
    background: #0b6dff;
    border: 0;
    padding: 10px 20px;
    margin-top: 20px;
    color: white;
    border-radius: 20px;
}
.submit{
    text-align: center;
}
</style>