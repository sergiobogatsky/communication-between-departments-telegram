<template>
    <v-row
            align="start"
            justify="start"
    >
        <v-col
                v-for="department in departments"
                lg="4"
                xl="4"
                cols="12"
                sm="12"
                md="6"
        >
            <v-card
            >
                <v-card-title>{{department.name}}</v-card-title>
                <v-card-text></v-card-text>
                <v-card-actions>
                    <router-link
                            tag="v-btn"
                            text
                            :to="{name: 'show department', params: {id: department.id}}"
                    >
                        show
                    </router-link>

                </v-card-actions>
            </v-card>
        </v-col>
    </v-row>
</template>

<script>
    export default {
        data() {
            return {
                departments: []
            }
        },
        methods: {
            indexDepartments(){
                this.$http.get('/api/departments').then(response => {
                    this.departments = response.data;
                    console.log(this.departments);
                }, response => {
                    alert('Error in indexDepartments()');
                });
            }
        },
        created(){
            this.indexDepartments();
        },
    }
</script>