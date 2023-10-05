<template>
    <header>
        <router-link to="/">
            <h1><span>Vue</span> movies</h1>
        </router-link>
    </header>
    <main>
        <router-view />
    </main>
</template>

<style lang="scss">
* {
    padding: 0;
    margin: 0;
    box-sizing: border-box;
}

body {
    background-color: whitesmoke;
    font-family: "Inter", sans-serif;
}

a {
    color: #000;
    text-decoration: none;
}

header {
    display: flex;
    justify-content: center;
    align-items: center;
    box-shadow: 1px 5px 5px rgb(255, 200, 150);
    padding: 20px;
    h1 {
        font-size: 35px;
    }
}
</style>
