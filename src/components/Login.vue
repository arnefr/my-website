
<template>
    <div class="login">


        <h2>Login Form</h2>

        <div v-if="isLoggedIn == true" class="imgcontainer">
            <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSD9iW2bmA5NsUwf7eZoyhJaQoQQBjiO4NsGg&usqp=CAU" alt="Avatar" class="avatar">
        </div>
    
        <div v-else class="container">
            <label for="uname"><b>Username</b></label>
            <input type="text" v-model="username" placeholder="Enter Username" name="uname" required>

            <label for="psw"><b>Password</b></label>
            <input :type="showPassword == true ? 'text' : 'password'" @keydown.enter="Login" v-model="password" placeholder="Enter Password" name="psw" required>
           <span ref="failedText" class="hasLoginfailed animate" v-if="hasLoginfailed">Login failed </span> 
            <button @click="Login() "  type="submit">Login</button>
            <label>
                <input type="checkbox" v-model="showPassword" checked="checked" name="remember"> Show Password
            </label>
            
        </div>
    </div>

</template>
<script setup>
import { nextTick } from 'vue';

function Login() {
    if(username.value == "arne" && password.value == "pommes") {
        isLoggedIn.value = true;
    } else {
        isLoggedIn.value = false;
        hasLoginfailed.value = true
        failedText.value.classList.remove("animate");
        setTimeout(() => failedText.value.classList.add("animate"), 10)

    }
} 
import { ref } from 'vue';

const password = ref('')
const username = ref('')
const showPassword = ref(false)
const isLoggedIn = ref(false);
const hasLoginfailed = ref(false)

const failedText = ref();

</script>

<style lang="scss">

.hasLoginfailed {
    display: inline-block;
    color: red;

    &.animate {
        animation: test 0.5s;
    }
    
}

.login {
    body {
        font-family: Arial, Helvetica, sans-serif;
    }

    form {
        border: 3px solid #f1f1f1;
    }

    input[type=text],
    input[type=password] {
        width: 100%;
        padding: 12px 20px;
        margin: 8px 0;
        display: inline-block;
        border: 1px solid #ccc;
        box-sizing: border-box;
    }

    button {
        background-color: #04AA6D;
        color: white;
        padding: 14px 20px;
        margin: 8px 0;
        border: none;
        cursor: pointer;
        width: 100%;
    }

    button:hover {
        opacity: 0.8;
    }

    .cancelbtn {
        width: auto;
        padding: 10px 18px;
        background-color: #f44336;
    }

    .imgcontainer {
        text-align: center;
        margin: 24px 0 12px 0;
    }

    img.avatar {
        width: 40%;
        border-radius: 50%;
    }

    .container {
        padding: 16px;
    }

    span.psw {
        float: right;
        padding-top: 16px;
    }

    /* Change styles for span and cancel button on extra small screens */
    @media screen and (max-width: 300px) {
        span.psw {
            display: block;
            float: none;
        }

        .cancelbtn {
            width: 100%;
        }
    }
}
</style>


