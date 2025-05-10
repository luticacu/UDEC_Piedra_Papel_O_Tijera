<template>
    <footer class="footer">
        <div class="footer-left">
            <img src="/resources/images/FotoPersonal.jpg" class="personal_image">
            <div class="myInformation">
                <div class="usernameAndLogos">
                    <h1>Luticacu</h1>
                    <div class="social-icons">
                        <a href="" target="_blank" class="icon"><img src="/resources/svgs/logo_x.svg"></a>
                        <a href="" target="_blank" class="icon"><img src="/resources/svgs/logo_instagram.svg"></a>
                        <a href="" target="_blank" class="icon"><img src="/resources/svgs/logo_youtube.svg"></a>
                        <a href="" target="_blank" class="icon"><img src="/resources/svgs/logo_threads.svg"></a>
                    </div>
                </div>
                <div>
                    <h2>Jorge Tirado Cacua</h2>
                    <p>Desarrollador Frontend</p>
                </div>
            </div>
        </div>
        <div class="footer-right">
            <p>&copy; 2025 Proyecto Realizado por @luticacu (Jorge Tirado Cacua)</p>
        </div>
    </footer>
</template>

<style scoped>
* {
    /* "*" selecciona todos los elementos */
    box-sizing: border-box; /* ancho y alto + pading y margin */
    margin: 0;
    padding: 0;
}

h1 {
    font-size: 2rem;
    margin: 0;
}

h2 {
    font-size: 1.2rem;
    margin: 0.5rem 0;
}

p {
    margin: 0;
}

.myInformation {
    display: flex;
    flex-direction: column;
}

.usernameAndLogos {
    display: flex;
    align-items: center;
    gap: 10px;
}

/* Footer General */
.footer {
    background-color: #222;
    color: white;
    display: flex;
    justify-content: space-between;
    /* position: fixed; */
    align-items: center;
    padding: 1rem 2rem;
    width: 100%;
    bottom: 0;
    z-index: 10;
}

/* Envoltura para la información de la izquierda */
.footer-left {
    display: flex;
    align-items: center;
}

/* Envoltura para la información de la derecha */
.footer-right {
    font-size: 0.9rem;
    color: #ccc;
    text-align: right;

}

.info {
    display: flex;
    flex-direction: column;
}

.name {
    display: flex;
    align-items: center;
    margin: 0;
}

.footer-right {
    display: flex;
    align-items: center;
}

.social-icons {
    display: flex;
    gap: 10px;
}

.icon img {
    width: 24px;
    height: 24px;
    filter: brightness(0) invert(1);
    transition: filter 0.3s ease;
}

.icon:hover img {
    filter: brightness(0.8) invert(1);
}

.personal_image {
    width: 100px;
    height: 100px;
    border-radius: 50%;
    margin-right: 15px;
}
</style>