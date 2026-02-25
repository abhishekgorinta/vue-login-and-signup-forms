<template>
    <div class="login-container">
        <div class="login-card">
            <div class="login-left">
                <div class="text">
                    <h2>Welcome Back</h2>
                    <p>Sign in to your account</p>
                </div>
            </div>
            <div class="login-right">
                <form @submit.prevent="handleLogin">

                    <input type="text" placeholder="Enter Email / User name" v-model="identifier" required />

                    <input :type="showPassword ? 'text' : 'password'" placeholder="Password" v-model="password"
                        required />

                    <div class="show-password">
                        <input type="checkbox" id="showPassword" @change="togglePasswordVisibility" />
                        <label for="showPassword"> Show Password</label>
                    </div>

                    <button type="submit" class="btn">Sign In</button>

                    <p class="message" v-if="message">{{ message }}</p>

                    <p class="link">
                        New user?
                        <router-link to="/signup">Create an account</router-link>
                    </p>
                </form>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "Login",
    data() {
        return {
            identifier: "",
            password: "",
            showPassword: false,
            message: ""
        };
    },
    methods: {
        handleLogin() {
            const users = JSON.parse(localStorage.getItem("users")) || [];

            const id = (this.identifier || "").trim().toLowerCase();

            const user = users.find(u => {
                const email = (u.email || "").trim().toLowerCase();
                const name = (u.name || "").trim().toLowerCase();
                return (email === id || name === id) && u.password === this.password;
            });

            if (!user) {
                this.message = " Invalid credentials";
                return;
            }

            localStorage.setItem("currentUser", JSON.stringify(user));

            this.message = "Login successful! Redirecting...";

            setTimeout(() => {
                this.$router.push("/home");
            }, 1000);
        }
        ,
        togglePasswordVisibility() {
            this.showPassword = !this.showPassword;
        }
    }
};
</script>

<style scoped>
.login-container {
    min-height: 90vh;
    display: flex;
    justify-content: center;
    align-items: center;
    font-family: "Segoe UI", sans-serif;

}

.login-card {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    background: #fff;
    width: 600px;
    min-height: 400px;
    border-radius: 12px;
    box-shadow: 0 10px 25px rgba(0, 0, 0, 0.2);
    transition: all 0.3s ease;
}

.login-card:hover {
    box-shadow: 0 15px 35px rgba(0, 0, 0, 0.3);
    transform: translateY(-2px);
}

.login-left {
    color: white;
    background-color: #5a67d8;
    border-radius: 12px 0px 0px 12px;
    display: grid;
    place-items: center;
}

.login-right {
    padding: 20px;
    display: grid;
    place-items: center;
}

.login-card h2 {
    text-align: center;
    margin-bottom: 5px;
}

.subtitle {
    text-align: center;
    font-size: 14px;
    color: white;
    margin-bottom: 20px;
}

input[type="text"],
input[type="password"] {
    width: 100%;
    padding: 10px 12px;
    border: 1px solid #ddd;
    border-radius: 6px;
    font-size: 14px;
    margin-bottom: 15px;
    transition: all 0.3s ease;
}

input:focus {
    border-color: #667eea;
    outline: none;
    box-shadow: 0 0 8px rgba(102, 126, 234, 0.4);
}

.btn {
    width: 100%;
    padding: 10px;
    background: #667eea;
    color: #fff;
    border: none;
    border-radius: 6px;
    font-size: 15px;
    cursor: pointer;
    transition: all 0.3s ease;
}

.btn:hover {
    background: #5a6fd8;
    transform: translateY(-2px);
    box-shadow: 0 5px 15px rgba(102, 126, 234, 0.4);
}

.message {
    color: grey;
    margin-top: 15px;
    text-align: center;
    font-size: 14px;
}

.link {
    margin-top: 15px;
    text-align: center;
    font-size: 14px;
}

.link a {
    color: #185a9d;
    text-decoration: none;
    font-weight: 600;
}

@media(max-width:650px) {
    .login-card {
        display: grid;
        grid-template-columns: repeat(1, 1fr);
        background: #fff;
        width: 90%;

    }

    .login-left {
        color: black;
        background-color: white;
    }
    
}
</style>
