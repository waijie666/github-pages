<template>
    <div id="counter" v-bind:title="message">
        Counter: {{ counter }}
    </div>
    <button v-on:click="resetCounter">Reset Counter</button>
    <div>{{ message }}</div>
    <button v-on:click="reverseMessage">Reverse Message</button>
    <div><input v-model="currentRouteName" size="50"/></div>
    <span v-if="seen">Now you see me </span>
    <button v-on:click="toggleVisibility">Toggle Visibility</button>
    <ol>
        <li v-for="todo in todos" :key="todo.text">
            {{todo.text}}
        </li>
    </ol>
</template>

<script>
export default {
    name: 'Counter',
    data()  {
        return  {
            counter: 0,
            message: 'You loaded this page on ' + new Date().toLocaleString(),
            seen: true,
            todos: [
                { text: "First "},
                { text: "Second "},
                { text: "Third "},
                { text: "Fourth"}
            ],
            datestring: new Date().toLocaleString()
        }
    },
    created() {
    },
    mounted() {
        setInterval(() => {
            this.counter++,
            this.datestring = new Date().toLocaleString();
        }, 1000)
    },
    updated() {
    },
    methods:{
        reverseMessage()
        {
            this.message = this.message.split('').reverse().join('')
            //this.message = "Apple"
        },
        resetCounter()
        {
            this.counter = 0
        },
        toggleVisibility()
        {
            this.seen = !this.seen
        }
    },
    computed: {
        currentRouteName() {
            return this.$route.name + " " + this.datestring
        }
    }
}
</script>