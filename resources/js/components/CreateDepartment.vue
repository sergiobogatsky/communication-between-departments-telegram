<template>
    <form
            method="post"
    >
        <v-text-field
                v-model="name"
                label="name"
                required
        ></v-text-field>

        <v-btn class="mr-4" @click="submit">create</v-btn>
        <v-btn @click="clear">clear</v-btn>
    </form>
</template>

<script>
    export default {
        props: {
            id: String,
            name: String
        },
        data() {
            return {
                department: Object,
            }
        },
        methods: {

            clear() {
                this.name = '';
            },

            submit() {
                this.errors = {};
                this.$http.post('/api/departments/store'
                    , {
                        name: this.name
                    }).then(response => {
                    this.$router.push('/departments/show/' + response.data.id);
                }).catch(error => {
                    if (error.response.status === 422) {
                        this.errors = error.response.data.errors || {};
                    }
                });
            },
        }
    }
</script>

<style scoped>

</style>