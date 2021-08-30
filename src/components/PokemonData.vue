<template>
    <div class="data-container">
        <div class="group">
            <p>NOMBRE: </p>
            <div>
                <ul>
                    <li>{{ name }}</li>
                </ul>
            </div>
        </div>

        <div class="group">
            <p>TIPO: </p>
            <div>
                <ul>
                    <li v-for="tipo in types">- {{ tipo.type.name }}</li>
                </ul>
            </div>
        </div>

        <div class="group">
            <p>HABILIDADES: </p>
            <div>
                <ul>
                    <li v-for="ability in abilities">- {{ ability.ability.name }}</li>
                </ul>
            </div>
        </div>


    </div>
</template>

<script>
export default {
    props: {
        types: {
            type: Array,
            required: true
        },
        abilities: {
            type: Array,
            required: true
        },
        name: {
            type: Array,
            required: true
        }
    }

}
</script>

<style scoped>
    .data-container {
        display: block;
        background-color: #032D29;
        border-radius: 15px;
        padding: 10px;
        width: 80%;
        margin: 0 auto;
    }
    .group {
        border: 1px solid #FFFFFF;
        display: grid;
        grid-template-columns: 40% 60%;
    }
    .group p{ 
        color: #FCDB04;
        font-weight: bold;
        text-align: right;
    }
    .group li {
        color: #00EE07;
        list-style: none;
        text-align: initial;
        padding-left: 10px;
    }
</style>