<template>
    <form @submit.prevent="handleSubmit">
        <label>Email</label>
        <div><p class="error">{{ Nulity }}</p></div>
        <input type="email" required v-model="email">
        <label>password</label>
        <input type="password" required v-model="password">
        <div><p class="error">{{ Nulity }}</p></div>
        <div><p class="error">{{ passwordError }}</p></div>
        <label>field</label>
        <select v-model="field">
            <option value="designer">web designer</option>
            <option value="developer">web developer</option>
        </select>

            <label>skills</label>
            <input type="text" v-model="tempskills" @keyup.alt="addSkills">
            <div v-for="skill in skills" :key="skill" class="pill">
                <span @click="deleteSkills(skill)">{{ skill }}</span>
            </div>
            <div><p class="error">{{ Nulity }}</p></div>

        <div>
            <input type="checkbox">
            <label>accept terms and conditions</label>
        </div>

        <div class="submit">
            <button>create An account</button>
        </div>

    </form>
    <p>email: {{ email }}</p>
    <p>password: {{ password }}</p>
    <p>skills : {{ skills }}</p>
    <p>field : {{ field }}</p>
</template>

<script>
export default {
    data() {
        return{
            email:'',
            password: '',
            field: 'designer',
            tempskills: '',
            skills: [],
            passwordError: '',
            Nulity: ''
        }
    },
    methods: {
        addSkills(e){
            if(e.key === ',' && this.tempskills){
                if(!this.skills.includes(this.tempskills)){
                    this.skills.push(this.tempskills);
                }
                this.tempskills = ''
            }
        },
        deleteSkills(skill){
            this.skills = this.skills.filter((item) => {
                return skill !== item
            })
        },
        handleSubmit() {
            if( this.password.length < 5 ){
                this.passwordError = "password must be atleast 6 chars"
            }
        }
    }
}
</script>
<style>
form{
    max-width: 400px;
    margin: 100px auto;
    background: white;
    text-align: left;
    padding: 40px;
    border-radius: 10px
}
label{
    color: #aaa;
    display: inline-block;
    margin: 20px 0 15px;
    font-size: 0.6rem;
    text-transform: uppercase;
    letter-spacing: 1px;
    font-weight: bold;
}
input, select {
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
.pill{
    display: inline-block;
    margin: 20px 10px 0 0;
    padding: 6px 12px;
    background: #eee;
    border-radius: 20px;
    font-size: 20px;
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
.error{
    color: crimson;
    font-family: bold;
}
</style>