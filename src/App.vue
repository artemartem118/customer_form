<template>
    <div class="app" id="app">
        <div class="wrapper">
            <SuccessfulFormCreation @backToForm="backToForm"  v-if="isFormSuccess"/>
            <CustomersForm @successForm="successForm" v-else/>
        </div>
    </div>
</template>

<script>
import CustomersForm from './components/CustomersForm'
import SuccessfulFormCreation from './components/SuccessfulFormCreation'

export default {
    components: { CustomersForm, SuccessfulFormCreation },
    data() {
        return {
            isFormSuccess: false
        }
    },
    methods: {
        successForm() {
            this.isFormSuccess = true
        },
        backToForm() {
            this.isFormSuccess = false
        }
    }
}
</script>

<style lang="scss">
/* hide arrows input number */
input[type=number]::-webkit-inner-spin-button,
input[type=number]::-webkit-outer-spin-button {
    -webkit-appearance: none;
    margin: 0;
}

* {
    box-sizing: border-box;
}

html,
body {
    margin: 0;
    padding: 0;
    font-family: 'Lato', sans-serif;
}

:active, :hover, :focus {
    outline: 0;
    outline-offset: 0;
}

.app {
    padding: 0 15px;
}

.wrapper {
    margin: 0 auto;
    max-width: 500px;
}
</style>
