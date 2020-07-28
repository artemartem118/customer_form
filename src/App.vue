<template>
    <div class="app" id="app">
        <div class="wrapper">
            <CustomersForm/>
        </div>
    </div>
</template>

<script>
    import CustomersForm from './components/CustomersForm'

    export default {
        components: { CustomersForm }
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
