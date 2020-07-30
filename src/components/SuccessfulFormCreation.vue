<template>
    <div :style="{ height: windowHeight + 'px' }" class="container">
        <div class="form-success">
            <div class="form-success__title">Клиент создан</div>
            <div class="form-success__btn"><input @click="backToForm" value="Вернуться" type="button"/></div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'SuccessfulFormCreation',
    data() {
        return {
            windowHeight: window.innerHeight
        }
    },
    methods: {
        backToForm() {
            this.$emit('backToForm')
        },
        onResize() {
            this.windowHeight = window.innerHeight
        }
    },
    mounted() {
        window.addEventListener('resize', this.onResize)
        this.onResize()
    },
    beforeDestroy() {
        window.removeEventListener('resize', this.onResize)
    }
}
</script>

<style lang="scss" scoped>
@import "../styles/variables";
@import "../styles/mixins";

.container {
    display: flex;
    justify-content: center;
    align-items: center;
}

.form-success {
    @include box-shadow-container;

    display: flex;
    flex-direction: column;
    justify-content: space-between;
    padding: $base * 50;
    width: $base * 300;
    height: $base * 200;
    border-radius: $base * 5;

    &__title {
        font-size: $base * 20;
        align-self: center;
    }

    &__btn {
        align-self: center;

        @include button;
    }
}

@media (max-width: $max-width-sm) {
    .form-success {
        width: $base * 250;
    }
}
</style>
