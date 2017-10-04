<template>
    <div class="col-xs-12 col-sm-6">
        <ul class="list-group">
            <li
                    class="list-group-item"
                    v-for="server in servers"
                    >
                <app-server :id="server.id" :status="server.status"></app-server>
            </li>
        </ul>
    </div>
</template>

<script>
    import { eventBus } from '../../main'
    import Server from './Server.vue';
    export default {
        data: function () {
            return {
                servers:[
                    { id: 1, status: 'Normal'},
                    { id: 2, status: 'Critical'},
                    { id: 3, status: 'Unknown'},
                    { id: 4, status: 'Updating'},
                    { id: 5, status: 'Normal'}
                ]
            }
        },
        methods: {
            selectServer(event) {
                console.log(event)
            }
        },
        components: {
            appServer: Server,
        },
        created() {
            eventBus.$on('serverStatusWasChanged', (server) => {
                var serverFound = this.servers.forEach(function(item, i , servers){
                    if (item.id === server.id) {
                        item.status = server.status;
                    }
                });
            })
        }
    }
</script>

