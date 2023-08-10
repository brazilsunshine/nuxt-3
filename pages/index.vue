<template>
    <div>
        <div>
            main index.vue
        </div>
        <Counter />
        <div>
            x: {{ x }}
            y: {{ y }}
        </div>

        <!-- users1 -->
        <div>
            <ul>
                <li v-for="user in users" :key="user.id">
                    {{ user.name }}
                </li>
            </ul>
        </div>

        <!-- users2 -->
        <div>
            <ul>
                <li v-for="user in users2" :key="user.id">
                    {{ user.name }}
                </li>
            </ul>
        </div>

        <!-- users3 -->
        <div>
            <ul>
                <li v-for="user in users3" :key="user.id">
                    {{ user.name }}
                </li>
            </ul>
        </div>

        <div>
            <ul>
                <li v-for="user in users3" :key="user.id">
                    {{ user.name }}
                </li>
            </ul>
        </div>
        <div>
            {{ user.name }}
        </div>
    </div>
</template>

<script setup>
    // <script setup> allows you to define variables, functions, and logic in a more concise way.
    import Counter from "./components/Counter";
    import { useMouse } from "./composables/useMouse";

    /**
     * Get x, y values from
     */
    const { x, y } = useMouse()

    const users = ref([]) // returns an array
    // ref is a function that is used to create a reactive reference to a value.
    // Reactive means that changes to the value will automatically trigger updates in the user interface

    /**
     * Rendered on the client's side
     */
    onMounted(() => { // API request to "https://jsonplaceholder.typicode.com/users" to fetch user data
        fetch('https://jsonplaceholder.typicode.com/users')
        .then(response => response.json()) // convert the response to json
        .then(data => users.value = data) // Once the data is retrieved, it's assigned to the users variable.
    })

    /**
     * Rendered on the server's side
     */
    const { data: users2 } = await useAsyncData(
        // useAsyncData fetches data on the server, and then it emerges the data on the client
        'users2', () => $fetch('https://jsonplaceholder.typicode.com/users')
    )

    /**
     * Rendered on the server's side
     */
    const { data: users3 } = await useFetch('https://jsonplaceholder.typicode.com/users')


    /**
     * Rendered on the server's side
     */
    const { data: user } = await useFetch('https://jsonplaceholder.typicode.com/users/1', {
        pick: [ // pick specifies that only specific properties should be picked from the fetched data.
            'id', // In this case, the properties being picked are 'id', 'name',
            'name',
            'email'
        ]
    })

    /**
     * Rendered on the server's side
     */
    const { data: weather } = await useFetch('/api/weather') // server/api/weather
</script>
