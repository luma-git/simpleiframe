<template>
    <div class="mt-3">
        <h2>Votre code ✨</h2>
        <div class="mt-4 generated-code">
            <button @click="copyCode()" type="button" class="btn btn-outline-info btn-sm mb-1 generated-code-btn">{{ this.copyCodeButton }}</button>
            <div>
                <code>{{ generatedCode }}</code>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            copyCodeButton: 'Copier'
        }
    },
    props: {
        generatedCode: {
            type: String,
            required: true
        },
        copyCodeButton: {
            type: String,
            required: true
        }
    },
    methods: {
        copyCode() {
            this.copyCodeButton = 'Copié ! 🎉'
            navigator.clipboard.writeText(this.generatedCode)
            setTimeout(() => {
                this.copyCodeButton = 'Copier'
            }, "1000")
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