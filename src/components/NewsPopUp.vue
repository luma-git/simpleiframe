<template>
<div v-if="this.isDisplayed" class="card">
    <button @click="closePopUp()" type="button" class="btn btn-outline-info">Fermer</button>
    <p><span>Il y a du nouveau ! 🆕</span>
    {{ this.message }}</p>
</div>
</template>

<script>
export default {
    data() {
        return {
            isDisplayed: true
        }
    },
    props: {
        message: {
            type: String,
            required: false
        }
    },
    methods: {
        closePopUp() {
            this.isDisplayed = false
        }
    }
}
</script>

<style scoped>
.generated-code {
    position: relative;
}

.generated-code-btn {
    position: absolute;
    right: 0;
    top: -35px;
}
</style>

<style scoped>
div {
    background-color: #fff;
    color: #222222;
    text-align: center;
    padding: 20px;
    width: 100%;
    margin-bottom: 20px;
    position: relative;
}

div button {
    position: absolute;
    top: 10px;
    right: 10px;
    font-size: 0.8em;
}

div p {
    margin-top: 20px;
}

div p span {
    font-size: 1.3em;
    display: block;
}
</style>