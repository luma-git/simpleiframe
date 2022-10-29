<script setup>
import Form from '@/components/Form.vue'
import NewsPopUp from '@/components/NewsPopUp.vue'
import { ref } from 'vue'

const message = ref("Simpleiframe évolue et passe en v0.2 sur VueJS. L'outil va continuer à évoluer pour intégrer de nouveaux services. N'hésitez pas à contribuer sur GitHub ou à signaler des bugs. Merci ! 😺")
</script>

<template>
    <NewsPopUp :message="message" />
    <header>
        <img src="3d-rocket.png" />
        <h1>simpleiframe <span class="badge bg-primary">Bêta</span></h1>
        <p class="lead">Bienvenue 👋 Remplissez le formulaire et générez un code prêt à intégrer,
            responsive et conforme au RPGD grâce à tarteaucitron.io</p>
    </header>
    <main>
        <Form />
    </main>
    <footer class="mt-5">
        <div class="footer-links">
            <a href="https://github.com/paulinegilg/simpleiframe" class="btn btn-outline-info" role="button">Contribuer sur GitHub 🧠</a>
            <a href="mailto:paulinegilg@protonmail.com" class="btn btn-outline-info" role="button">Signaler un bug 🐛</a>
            <!--<a href="#" class="btn btn-outline-info" role="button">Mentions légales & confidentialité 🛡️</a>-->
        </div>
        <div class="credentials">
        <span>Développé par <a href="https://paulinegilg.fr" target="_blank" class="link-info">Pauline Gilg</a> avec VueJS</span>
        <span>Illustration by <a href="https://icons8.com/illustrations/author/zD2oqC8lLBBA" target="_blank" class="link-info">Icons 8</a> from <a href="https://icons8.com/illustrations" target="_blank" class="link-info">Ouch!</a></span>
        </div>
    </footer>
</template>

<style scoped>
header img {
    width: 150px;
    display: block;
    margin: auto;
}

header {
    display: flex;
    flex-direction: column;
}

header * {
    text-align: center;
}
.footer-links {
    display: flex;
    flex-direction: column;
    justify-content: center;
    gap: 10px;
}

.credentials {
    font-size: 0.8em;
    text-align: center;
    margin-top: 20px;
    display: flex;
    flex-direction: column;
}
</style>
