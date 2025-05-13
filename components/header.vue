<template>
    <header class="header">
        <h1 class="title">Piedra, Papel o Tijeras</h1>
        <nav class="nav">
            <ul>
                <li>Tu puntaje <p>{{ scores.usuario }}</p>
                </li>
                <li>Empates <p>{{ scores.empates }}</p>
                </li>
                <li>Puntaje bot <p>{{ scores.computadora }}</p>
                </li>
            </ul>
        </nav>
    </header>
</template>

<script>
export default {
    name: "Header",
    props: {
        scores: {
            type: Object,
            required: true,
        },
    },
};
</script>

<style scoped>
* {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
}

p {
    font-style: bold;
    font-size: 1.5rem;
    margin-top: 1vh;
}

.title {
    margin-top: 0.3rem;
    font-size: 1.8rem;
    font-weight: bold;
    color: white;
    margin-bottom: 1.5rem;
}

.header {
    position: fixed;
    width: 100%;
    background-color: #222;
    color: white;
    padding: 1rem;
    display: flex;
    flex-direction: column;
    align-items: center;
}

.nav ul {
    list-style: none;
    margin: 0;
    padding: 0.2rem 0 0 0;
    display: flex;
    gap: 1rem;
    align-items: center;
    text-align: center;
}

.nav a {
    color: white;
    text-decoration: none;
}

.nav a:hover {
    text-decoration: underline;
}
</style>