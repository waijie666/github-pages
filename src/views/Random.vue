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
    <todo-list :itemsProp="['Attribute0', 'Attribute1', 'Attribute2']" >
      <template v-slot:default="slotProps">
        <i class="fas fa-check"></i>
        <span class="green">{{ slotProps.item }}</span>
        <span class="green">{{ slotProps.index }}</span>
        <span class="green">{{ slotProps.apple }}</span>
        {{ slotProps.index+slotProps.apple }}
      </template>
    </todo-list>
</template>

<script>

const slotComponent = {
    props: {
      itemsProp : { default: ["Eat Apple", "Eat Orange"]}
    },
    data() {
        return {
            items: this.itemsProp
        }
    },     
    template: `
        <ul>
            <li v-for="(item, index) in items">
                <slot :item=item :index=index :apple=index+1></slot>
            </li>
        </ul>`
    
}

export default {
    name: 'Counter',
    components: {
        "todo-list": slotComponent
    },
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