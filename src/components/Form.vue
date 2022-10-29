<template>
    <form @submit.prevent="convertURLtoID(), checkForm(), generateCode()">

        <BaseSelect :options="services" v-model="serviceToConvert.service" label="Type de contenu" />

        <ServiceInfos v-if="this.serviceToConvert.service" :service="serviceToConvert.service" />

        <BaseInput v-model="serviceToConvert.url" label="URL du contenu" type="text" error="L'URL n'est pas valide !" />

        <BaseInput v-model="serviceToConvert.title" label="Titre du contenu" type="text"
            error="Veuillez saisir un titre !" />

        <BaseSelect :options="videoSizes" v-model="serviceToConvert.size" label="Taille de la vidéo" />

        <BaseCheckbox v-model="serviceToConvert.centered" label="Centrer le contenu" />

        <div class="mt-4">
            <button type="submit" class="btn btn-primary">Générer le code</button>

            <button type="button" @click.prevent="clearForm()" class="btn btn-outline-primary m-2">Annuler</button>
        </div>

        <div v-if="errors.length" class="callout">
            <span><strong>Nous avons encore besoin de quelques informations pour préparer votre code :</strong></span>
            <ul>
                <li v-for="error in errors">🚨 {{ error }}</li>
            </ul>
        </div>

        <GeneratedCode v-if="this.generatedCode" :generatedCode="generatedCode" />

    </form>
</template>

<script>
import BaseSelect from '@/components/FormComponents/BaseSelect.vue'
import BaseInput from '@/components/FormComponents/BaseInput.vue'
import BaseCheckbox from '@/components/FormComponents/BaseCheckbox.vue'
import GeneratedCode from '@/components/GeneratedCode.vue'
import ServiceInfos from '@/components/ServiceInfos.vue'
export default {
    components: {
        BaseSelect,
        BaseInput,
        BaseCheckbox,
        GeneratedCode,
        ServiceInfos
    },
    data() {
        return {
            services: [
                'youtube',
                'dailymotion',
                'vimeo',
                'creacast'
            ],
            videoSizes: [
                '360px', '720px', '1200px'
            ],
            parcers: {
                youtube: 'https://youtu.be/',
                dailymotion: 'https://dai.ly/',
                vimeo: 'https://vimeo.com/'
            },
            serviceToConvert: {
                service: '',
                url: '',
                id: '',
                title: '',
                size: null,
                centered: false
            },
            generatedCode: '',
            errors: []
        }
    },
    methods: {
        convertURLtoID() {
            if (this.parcers[this.serviceToConvert.service]) {
                this.serviceToConvert.id = this.serviceToConvert.url.replace(this.parcers[this.serviceToConvert.service], '')
            }
        },
        checkForm() {
            if (this.serviceToConvert.service && this.serviceToConvert.url && this.serviceToConvert.title && this.serviceToConvert.size) {
                this.errors = []
                return true
            }

            this.errors = []

            if (!this.serviceToConvert.service) {
                this.errors.push('Veuillez saisir un service')
            }
            if (!this.serviceToConvert.url) {
                this.errors.push('Veuillez saisir une URL')
            }
            if (!this.serviceToConvert.title) {
                this.errors.push('Veuillez saisir un titre')
            }
            if (!this.serviceToConvert.size) {
                this.errors.push('Veuillez choisir une taille')
            }
        },
        generateCode() {
            if (this.errors.length) {
                return false
            }

            if (this.serviceToConvert.service === 'youtube' || this.serviceToConvert.service === 'dailymotion' || this.serviceToConvert.service === 'vimeo') {
                this.generatedCode = '<style>.iframe-container {' + (this.serviceToConvert.centered ? 'margin: auto; ' : '') + 'max-width: ' + this.serviceToConvert.size + '; width: 100%;} .iframe-container__wrapper {position: relative; overflow: hidden; width: 100%; padding-top: 56.25%;} .responsive-iframe {position: absolute; top: 0; left: 0; bottom: 0; right: 0;}</style><div class="iframe-container"><div class="iframe-container__wrapper"><div class="' + this.serviceToConvert.service + '_player responsive-iframe" videoID="' + this.serviceToConvert.id + '" width="100%" height="100%" title="' + this.serviceToConvert.title + ' (Vidéo ' + this.serviceToConvert.service + ')"></div></div></div>'
            }
            else if (this.serviceToConvert.service === 'creacast') {
                this.generatedCode = '<style>.iframe-container {' + (this.serviceToConvert.centered ? 'margin: auto; ' : '') + 'max-width: ' + this.serviceToConvert.size + '; width: 100%;} .iframe-container__wrapper {position: relative; overflow: hidden; width: 100%; padding-top: 56.25%;} .responsive-iframe {position: absolute; top: 0; left: 0; bottom: 0; right: 0;}</style><div class="iframe-container"><div class="iframe-container__wrapper"><iframe class="responsive-iframe" src="' + this.serviceToConvert.url + '" width="100%" height="100%" title="' + this.serviceToConvert.title + ' (player vidéo)" allowfullscreen frameborder="0"></iframe></div></div>'
            }
        },
        clearForm() {
            this.serviceToConvert.service = ''
            this.serviceToConvert.url = ''
            this.serviceToConvert.id = ''
            this.serviceToConvert.title = ''
            this.serviceToConvert.size = null
            this.serviceToConvert.centered = false

            this.generatedCode = ''

            this.errors = []
        }
    }
}
</script>

<style scoped>
li {
    list-style: none;
    margin-left: -35px;
}

.callout {
    margin-top: 20px;
    border-left: #70e2ff 4px solid;
    padding: 3px 10px 1px 10px;
}
</style>