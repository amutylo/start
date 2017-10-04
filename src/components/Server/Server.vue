<template>
    <div class="" @click="selectServer(id, status)">
        <p>Server # {{ id }} and status is {{ status }}</p>
    </div>
</template>

<script>
    import { eventBus } from '../../main'
    export default {
        props: ['id', 'status', 'selectedServer'],
        methods: {
            selectServer(id, status) {
                eventBus.$emit('serverSelected', {id:id, status:status})
            }
        }
    }
</script>
