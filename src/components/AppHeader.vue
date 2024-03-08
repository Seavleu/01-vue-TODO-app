<template>
    <header>
        <h1><span class="icon" aria-hidden="true">✅</span>To Do</h1>
        <p>Building real work web application with Vue.js 3</p>
    </header>
</template>


<style scoped>
header{
    border-bottom: #333 1px solid;
    background-color: #fff;
    display: block;
    height: 11px;
    padding: 10px;
}
header::after{
    content: " ";
    display: block;
    height: 1px;
    box-shadow: 0px 0px 10px 0px rgba(0, 0, 0, 0.2);
}

header h1{
    font-size: 20px;
    font-weight: bold;
}

h1 .icon{
    font-size: 1rem;
    color: #333;
    margin-right: 10px;
    vertical-align: middle;
}
</style>
