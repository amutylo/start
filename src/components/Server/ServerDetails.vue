<template>
    <div class="col-xs-12 col-sm-6">
        <h3>Server Details</h3>
        <p v-if="!selectedId">Select server first</p>
        <p v-else>Server is {{ selectedId }} status is {{ selectedStatus }} </p>
        <button @click="changeServerStatus(selectedId)">Update status of server {{ selectedId }}</button>
    </div>
</template>

<script>
    import { eventBus } from '../../main'
    export default {
        data: function (){
          return {
              selectedId: null,
              selectedStatus: null
          }
        },
        props: {
            serverStatus: {
                type: String,
                default: 'unknown'
            },
            selectedServer: {
                type: String,
                default: 'not selected'
            }
        },
        methods: {
            changeServerStatus(id) {
                this.selectedStatus = 'Updated'
                eventBus.$emit('serverStatusWasChanged', {id: id, status:'Updated'})
            }
        },
        created() {
            eventBus.$on('serverSelected', (server) => {
                this.selectedId = server.id
                this.selectedStatus = server.status
            })
        }
    }
</script>

