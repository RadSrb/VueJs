<template>
    <div class="wrapper">
        <div class="main">
            <h1>Simple Calculator</h1>
            <input v-model="currentValue" />
            <div class="row">
                <simple-button class="btn" beschriftung="+" @calculate="calculate" :class="{ active: previousOperator === '+' }"></simple-button>
                <simple-button class="btn" beschriftung="-" @calculate="calculate" :class="{ active: previousOperator === '-' }"></simple-button>
                <simple-button class="btn" beschriftung="*" @calculate="calculate" :class="{ active: previousOperator === '*' }"></simple-button>
                <simple-button class="btn" beschriftung="/" @calculate="calculate" :class="{ active: previousOperator === '/' }"></simple-button>
            </div>
            <simple-button id="large" class="btn" beschriftung="=" @calculate="calculate" :class="{ active: previousOperator === '=' }"></simple-button>
        </div>
    </div>
</template>

<script>
import SimpleButton from "./SimpleButton.vue";

export default {
    name: 'TheCalculator',
    components: {
        SimpleButton
    },
    data() {
        return {
            previousValue: 0,
            currentValue: "",
            previousOperator: ""
        }
    },
    methods: {
        calculate(beschriftung) {
            if (beschriftung === "+" | beschriftung === "-" | beschriftung === "*" | beschriftung === "/") {
                this.previousValue = parseInt(this.currentValue);
                this.currentValue = "";
                this.previousOperator = beschriftung;
            } else if (beschriftung === "=") {
                if (this.previousOperator === "+") {
                    this.currentValue = this.previousValue + parseInt(this.currentValue);
                } else if (this.previousOperator === "-") {
                    this.currentValue = this.previousValue - parseInt(this.currentValue);
                } else if (this.previousOperator === "*") {
                    this.currentValue = this.previousValue * parseInt(this.currentValue);
                } else if (this.previousOperator === "/") {
                    this.currentValue = this.previousValue / parseInt(this.currentValue);
                }
            } else {
                console.log("Falsche Beschriftung");
            }
        }
    }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
body,
* {
    --font-color: #023047;
    font-family: 'Roboto', sans-serif;
}

.wrapper {
    padding: 0px;
    margin: 0px;
    height: 100vh;
    width: 100vw;
    display: flex;
    flex-direction: column;
    align-items: center;
    background-color: #21349d;
}

.main {
    width: 80vw;
    padding: 20px;
}

.main>h1 {
    text-align: center;
    font-weight: 600;
    font-size: 3em;
    color: white;
}

input {
    width: 79.7vw;
    height: 10vh;
    padding: 0px;
    margin-bottom: 20px;
    border: 2px solid var(--font-color);
    font-size: 2em;
}

.row {
    display: flex;
    flex-direction: row;
    gap: 30px;
}

.row>.btn {
    border: 2px solid var(--font-color);
    background: #c2140b;
    height: 10vh;
    padding: 20px;
    width: 20vw;
    text-align: center;
    font-size: 2em;
    font-weight: 600;
}

#large {
    margin-top: 20px;
    width: 80vw;
    border: 2px solid var(--font-color);
    height: 10vh;
    background: #c2140b;
    padding: 20px;
    text-align: center;
    font-size: 2em;
    font-weight: 600;
}

.btn:hover,
#large:hover {
    background-color: white;
    cursor: pointer;
    transition: 0.3s;
}

.active {
    background: #5998b7 !important;
}
</style>