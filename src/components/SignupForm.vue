<template>
  <h1>Create an Account</h1>
  <form @submit.prevent="handleSubmit">
    <label>Email</label>
    <!-- two way binding -->
    <input type="email" required v-model="email" />

    <label>Password</label>
    <input type="password" required v-model="password" />
    <div v-if="passwordError" class="error">{{ passwordError }}</div>

    <label>Role</label>
    <select v-model="role">
      <option value="developer">Web Developer</option>
      <option value="designer">Web Designer</option>
    </select>

    <label>Skills</label>
    <input type="text" v-model="tempSkill" @keyup="addSkills" />
    <div v-for="skill in skills" :key="skill" class="pill">
      <span @click="removeSkill(skill)">{{ skill }}</span>
    </div>

    <div class="terms">
      <input type="checkbox" required v-model="terms" />
      <label>Accept terms and conditions</label>
    </div>

    <div class="submit">
      <button>Sign Up</button>
    </div>
  </form>

  <!-- <div>
  <input type="checkbox" value="tanvir" v-model="names" />
  <label>Tanvir</label>
   <input type="checkbox" value="inzamam" v-model="names" />
  <label>Inzamam</label>
   <input type="checkbox" value="borhan" v-model="names" />
  <label>Borhan</label>
   <input type="checkbox" value="nabil" v-model="names" />
  <label>Nabil</label>
</div> -->

  <div class="successful" v-if="success">
     <img src="src/assets/avator.jpg" height="100px" width="100px" style="width:100%">
    <div class="container">
      <p>Email: {{ email }}</p>
      <p>Password: {{ password }}</p>
      <p>Role: {{ role }}</p>
      <p>Terms Accepted : {{ terms }}</p>
    </div>
  </div>

  <!-- <p>Names : {{names}}</p> -->
</template>

<script>
export default {
  data() {
    return {
      email: "",
      password: "",
      role: "designer",
      terms: false,
      tempSkill: "",
      skills: [],
      showSkill: true,
      passwordError: "",
      success: false,
      // names: []
    };
  },
  methods: {
    addSkills(e) {
      if (e.key === " " && this.tempSkill) {
        if (!this.skills.includes(this.tempSkill)) {
          this.skills.push(this.tempSkill);
        }

        this.tempSkill = "";
      }
    },
    removeSkill(skill) {
      this.skills = this.skills.filter((item) => {
        return skill !== item;
      });
    },
    handleSubmit() {
      console.log("form submitted");
      //validate password
      this.passwordError =
        this.password.length > 5
          ? ""
          : "Password must be at least six characters long";

      if (!this.passwordError) {
        console.log(this.email);
        console.log(this.password);
        console.log(this.skills);
        console.log(this.role);
        this.success = true;
      }
    },
  },
};
</script>

<style>
form {
  max-width: 420px;
  margin: 30px auto;
  background: rgb(32, 0, 11);
  text-align: left;
  padding: 40px;
  border-radius: 10px;
}
label {
  color: #aaa;
  display: inline-block;
  margin: 25px 0 15px;
  font-size: 0.6em;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: bold;
}
h1 {
  color: rgb(8, 49, 126);
}

input,
select {
  display: block !important;
  padding: 10px 6px;
  width: 100%;
  box-sizing: border-box;
  border: none;
  border-bottom: 1px solid #ddd;
  color: rgb(24, 20, 20);
}
input[type="checkbox"] {
  display: inline-block !important;
  width: 16px;
  margin: 0 10px 0 0;
  position: relative;
  top: 2px;
}
p {
  justify-content: baseline;
}

.pill {
  display: inline-block !important;
  margin: 20px 10px 0 0;
  padding: 6px 12px;
  background: #eee;
  border-radius: 20px;
  font-size: 12px;
  letter-spacing: 1px;
  font-weight: bold;
  color: rgb(119, 119, 119);
  cursor: pointer;
}
button {
  background: #ddd;
  border: 0;
  padding: 10px 20px;
  margin-top: 20px;
  color: rgb(2, 0, 0);
  border-radius: 20px;
}
.submit {
  text-align: center;
}
.error {
  color: #ff0062;
  margin-top: 10px;
  font-size: 0.8em;
  font-weight: bold;
}
.successful {
  /* Add shadows to create the "card" effect */
  background:#aaa;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
  transition: 0.3s;
}

/* On mouse-over, add a deeper shadow */
.successful:hover {
  box-shadow: 0 8px 16px 0 rgba(0, 0, 0, 0.2);
}

/* Add some padding inside the card container */
.container {
  padding: 2px 16px;
}
.img {
  width: 100px;
  height: 100px;
}
</style>