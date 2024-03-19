<template>
    <div id="login">
        <div class="background-container">
            <div class="login-container">
                <div class="logo-container">
                    <img alt="God Eye logo" src="../assets/god-eye.jpg" class="logo">
                </div>
                <h1>Phish Eye</h1>
                <div class="form-inputs">
                    <label for="username">Username</label>
                    <input type="text" id="username" name="username" v-model="input.username" placeholder="Username" />
                </div>
                <div class="form-inputs">
                    <label for="password">Password</label>
                    <input type="password" id="password" name="password" v-model="input.password" placeholder="Password" />
                </div>
                <button type="button" v-on:click="login()">Login</button>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'Login',
        data() {
            return {
                input: {
                    username: "",
                    password: ""
                }
            }
        },
        methods: {
            login() {
                if(this.input.username != "" && this.input.password != "") {
                    if(this.input.username == this.$parent.mockAccount.username && this.input.password == this.$parent.mockAccount.password) {
                        this.$emit("authenticated", true);
                        this.$router.replace({ name: "Home" });
                    } else {
                        console.log("The username and / or password is incorrect");
                    }
                } else {
                    console.log("A username and password must be present");
                }
            }
        }
    }
</script>

<style>
.login-container {
    position: relative;
    z-index: 1;
    padding: 20px;
    border-radius: 10px;
    max-width: 400px; /* Adjust as needed */
    margin: 0 auto;
    background-color: rgba(255, 255, 255, 0.8); /* Semi-transparent white */
    backdrop-filter: blur(10px); /* Adjust the blur strength as needed */
}
#login .form-inputs {
    padding-bottom: 10px;
}

#login .form-inputs label {
    padding-right: 10px;
}

.logo-container {
        width: 100px;
        height: 100px;
        overflow: hidden;
        border-radius: 50%;
        margin: 0 auto;
        margin-bottom: 20px; 
    }

    .logo {
        width: 100%;
        height: 100%;
        object-fit: cover;
    }

</style>