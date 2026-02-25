<template>
    <div class="register-container">
        <div class="register-card">
            <div class="register-left">
                <div class="text">
                    <h2>Create Account</h2>
                    <p>Please fill in the details to register</p>
                </div>
            </div>
            <div class="register-right">
                <form @submit.prevent="handleRegister">

                    <input type="text" placeholder="User Name" v-model="form.name" required />

                    <input type="email" placeholder="Email Address" v-model="form.email" required />

                    <input type="password" placeholder="Password" minlength="8" v-model="form.password" required />

                    <input type="password" placeholder="Confirm Password" v-model="form.confirmPassword" required />

                    <label class="label">Gender</label>
                    <div class="radio-group">
                        <label>
                            <input type="radio" value="Male" v-model="form.gender" />
                            male
                        </label>
                        <label>
                            <input type="radio" value="Female" v-model="form.gender" />
                            Female
                        </label>
                        <label>
                            <input type="radio" value="Other" v-model="form.gender" />
                            Other
                        </label>
                    </div>

                    <select v-model="form.city" required>
                        <option value="" disabled selected>Select your city</option>
                        <option value="vizag">vizag</option>
                        <option value="Hyderabad">Hyderabad</option>
                        <option value="Mumbai">Mumbai</option>
                        <option value="Bangalore">Bangalore</option>
                        <option value="Chennai">Chennai</option>
                        <option value="Delhi">Delhi</option>
                    </select>

                    <div class="terms">
                        <input type="checkbox" id="terms" v-model="form.acceptTerms" />
                        <label for="terms"> I accept Terms &amp; Conditions</label>
                    </div>

                    <button type="submit" class="btn">Register</button>

                    <p class="message" v-if="message">{{ message }}</p>

                </form>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    name: "Register",
    data() {
        return {
            form: {
                name: "",
                email: "",
                password: "",
                confirmPassword: "",
                gender: "",
                city: "",
                acceptTerms: false
            },
            message: ""
        };
    },
    methods: {
        handleRegister() {
            if (!this.form.acceptTerms) {
                this.message = "⚠️ Please accept Terms & Conditions";
                return;
            }

            const users = JSON.parse(localStorage.getItem("users")) || [];

            const emailToCheck = (this.form.email || "").trim().toLowerCase();
            const nameToCheck = (this.form.name || "").trim().toLowerCase();

            const emailExists = users.some(user => (user.email || "").trim().toLowerCase() === emailToCheck);
            if (emailExists) {
                this.message = "Email already registered. Please login or use a different email.";
                return;
            }

            const nameExists = users.some(user => (user.name || "").trim().toLowerCase() === nameToCheck);
            if (nameExists) {
                this.message = "Username already taken. Please choose a different username.";
                return;
            }

            if (this.form.password !== this.form.confirmPassword) {
                this.message = "Passwords do not match.";
                return;
            }

            users.push({
                name: this.form.name,
                email: this.form.email,
                password: this.form.password,
                gender: this.form.gender,
                city: this.form.city
            });
            localStorage.setItem("users", JSON.stringify(users));

            this.message = "Registration successful! You can login now...";

            this.form = {
                name: "",
                email: "",
                password: "",
                confirmPassword: "",
                gender: "",
                city: "",
                acceptTerms: false
            };
        }
    }
};
</script>
<style>
.register-container {
    min-height: 90vh;
    display: flex;
    justify-content: center;
    align-items: center;
    font-family: "Segoe UI", sans-serif;
}

.register-card {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    background: #fff;
    width: 600px;
    border-radius: 12px;
    box-shadow: 0 10px 25px rgba(0, 0, 0, 0.2);
    transition: all 0.3s ease;
}

.register-card:hover {
    box-shadow: 0 15px 35px rgba(0, 0, 0, 0.3);
    transform: translateY(-5px);
}

.register-left {
    color: white;
    background-color: #5a67d8;
    border-radius: 12px 0px 0px 12px;
    display: grid;
    place-items: center;
}

.register-right {
    padding: 20px;
}

.register-card h2 {
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
input[type="email"],
input[type="password"] {
    width: 100%;
    padding: 10px 12px;
    border: 1px solid #ddd;
    border-radius: 6px;
    font-size: 14px;
    outline: none;
    margin-bottom: 15px;
    transition: all 0.3s ease;
}

input:focus {
    border-color: #667eea;
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
    margin-top: 10px;
}

.btn:hover {
    background: #5a67d8;
    transform: translateY(-2px);
    box-shadow: 0 5px 15px rgba(102, 126, 234, 0.4);
}

.message {
    color: red;
    margin-top: 15px;
    text-align: center;
    font-size: 14px;
}

.label {
    font-size: 14px;
    color: #555;
    margin-bottom: 6px;
    display: block;
}
.radio-group {
    display: flex;
    gap: 15px;
    margin-bottom: 15px;
}

select {
    width: 100%;
    padding: 10px 12px;
    border: 1px solid #ddd;
    border-radius: 6px;
    font-size: 14px;
    outline: none;
    margin-bottom: 15px;
    transition: all 0.3s ease;
}

select:focus {
    border-color: #667eea;
    box-shadow: 0 0 8px rgba(102, 126, 234, 0.4);
}


@media(max-width:650px) {
    .register-card {
        display: grid;
        grid-template-columns: repeat(1, 1fr);
        background: #fff;
        width: 90%;

    }

    .register-left {
        color: black;
        background-color: white;
    }
}
</style>