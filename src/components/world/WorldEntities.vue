<template>
    <div>
        <b-card class="text-center m-3">
            <strong>Total Entities:</strong> {{entities.length}}
        </b-card>

        <b-pagination
                v-model="currentPage"
                :total-rows="entities.length"
                :per-page="rowsShown"
                align="center"
                limit="10"
        ></b-pagination>

        <b-table :items="entities" :fields="fields" striped :per-page="rowsShown" :current-page="currentPage"></b-table>
    </div>
</template>

<script>
    export default {
        name: 'WorldEntities',
        data()
        {
            return {
                rowsShown: 50,
                currentPage: 1,
                fields: [
                    {
                        label: 'Type',
                        key: 'type',
                        sortable: true
                    },
                    {
                        label: 'Display Name',
                        key: 'display_name',
                        sortable: true
                    },
                    {
                        label: 'Custom Name',
                        key: 'custom_name',
                        sortable: true
                    },
                    {
                        label: 'Alive',
                        key: 'alive'
                    },
                    {
                        label: 'UUID',
                        key: 'uuid'
                    },
                    {
                        label: 'X',
                        key: 'x'
                    },
                    {
                        label: 'Y',
                        key: 'y'
                    },
                    {
                        label: 'Z',
                        key: 'z'
                    }
                ]
            }
        },
        computed: {
            level()
            {
                return this.$store.state.levels[this.$route.params.world];
            },
            entities()
            {
                return this.level.entities.map((v) =>
                {
                    v.x = Number(v.x).toFixed(1);
                    v.y = Number(v.y).toFixed(1);
                    v.z = Number(v.z).toFixed(1);
                    return v;
                });
            }
        }
    };
</script>

<style scoped>

</style>
