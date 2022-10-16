<template>
    <div class="mt-3">
        <p v-for="(helpInfo, index) in this.helpInfos[service]" :key="index">{{ helpInfo }}</p>
        <p>Collez l'URL dans le champ du formulaire ci-dessous 😉</p>
    </div>
</template>

<script>
export default {
    data() {
        return {
            helpInfos: {
                youtube: [
                    'Pour récupérer la bonne URL, ouvrez la vidéo sur YouTube. Puis :',
                    'Cliquez sur "Partager".',
                    'Cliquez sur "Copier" pour récupérer l\'URL.'
                ],
                dailymotion: [
                    'Pour récupérer la bonne URL, ouvrez la vidéo sur Dailymotion. Puis :',
                    'Cliquez sur l\'icone en forme d\'avion en papier.',
                    'Cliquez sur "Copy link" pour récupérer l\'URL.'
                ],
                vimeo: [
                    'Pour récupérer la bonne URL, ouvrez la vidéo sur Vimeo. Puis :',
                    'Cliquez sur "Partager" au bas de la vidéo.',
                    'Récupérez l\'URL sous "Lien".'
                ],
                creacast: [
                    'Pour récupérer la bonne URL, utilisez l\'iframe fournie par le prestataire.',
                    'Sélectionnez l\'URL contenue dans l\'attribut "src" et copiez.',
                    'L\'URL devrait être de la forme https://creacast.com/nom-de-la-video.'
                ]
            }
        }
    },
    props: {
        service: {
            type: String,
            default: ''
        }
    }
}
</script>