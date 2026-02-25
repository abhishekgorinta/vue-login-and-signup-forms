<template>
    <div class="navbar">
        <div class="logo">
            <h1><router-link to="/">AB</router-link></h1>
        </div>
        <div class="links">
            <router-link to="/">Login</router-link>
            <router-link to="/signup">Signup</router-link>
        </div>
    </div>
</template>
<style>
.navbar {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    z-index: 1000;
    display: flex;
    justify-content: space-between;
    align-items: center;
    background-color: #5a67d8;
    padding: 10px 20px;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

.logo h1 a {
    font-size: 25px;
    text-decoration: none;
}

.links {
    display: flex;
    justify-content: space-evenly;
    align-items: center;
    gap: 20px;
}

a {
    font-size: 20px;
    color: white;
    text-decoration: none;
}

a:hover {
    text-decoration: underline;
    transition: 0.3s;
}
</style>
