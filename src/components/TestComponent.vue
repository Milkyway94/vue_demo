<template>
    <div class="jumbotron">
        <h1>{{msg}}</h1>

            <input
                    id="new"
                    v-model="name"
                    type="text"
                    name="new"
            >
            <button @click="addNew()">
                Thêm mới
            </button>

        <ul>
            <li class="newItem" v-for="item in news" :key="item">
                {{item.lead}}
            </li>
        </ul>
    </div>
</template>

<script>
    export default {
        name: 'Test',
        data() {
            return {
                msg: "Test",
                news: [],
                name: ""
            }
        },
        mounted() {
            let self = this;
            fetch("https://api.baonoivn.vn/api/v1/users/5aff840afe7d3752d5a018dd/categories/13/articles")
                .then(res => res.json())
                .then(data => {
                    //alert(data.results);
                    self.msg = data.message
                    self.news = data.results
                })
        },
        methods: {
            addNew() {
                this.news.push({lead: this.name})
            }
        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    h3 {
        margin: 40px 0 0;
    }

    ul {
        list-style-type: none;
        padding: 0;
    }

    li {
        display: inline-block;
        margin: 0 10px;
    }

    a {
        color: #42b983;
    }
    newItem{
        width: 100%;

    }
</style>
