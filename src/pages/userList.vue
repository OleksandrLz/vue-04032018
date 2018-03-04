<template>
    <div>
        <h2>Список пользователей</h2>

        <div v-if="!users.length" class="alert alert-warning">
            Загрузка...
        </div>
        <user-table v-else :users="users"></user-table>
    </div>
</template>

<script>
    import axios from 'axios'
    import UserTable from '@/components/UserTable.vue'
    export default {
        name: 'UsersListPage',
        components: {
            UserTable,
        },
        data: function () {
            return {
                // Список пользователей
                users: []
            };
        },
        methods: {
            loadData: function() {
                var self = this;
                axios.get('http://localhost:3004/users/')
                    .then(function(response) {
                        self.users = response.data;
                    })
            }
        },
        mounted: function () {
            this.loadData();
        }
    }

</script>