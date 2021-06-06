<template>
    <div type="flex">
        <p v-if="$fetchState.pending">Fetching mountains...</p>
        <p v-else-if="$fetchState.error">An error occurred :(</p>
        <div v-else>
            <h1>Nuxt Posts</h1>
            <el-button
                size="mini"
                type="success"
                @click="handleCreate(scope.$index, scope.row)">Add new Post
            </el-button>
            <el-table
                :data="posts.filter(data => !search || data.name.toLowerCase().includes(search.toLowerCase()))"
                style="width: 100%">
                <el-table-column label="Date" prop="title"></el-table-column>
                <el-table-column label="Name" prop="author"></el-table-column>
                <el-table-column align="right">
                <template slot="header">
                    <el-input
                    v-model="search"
                    size="mini"
                    placeholder="Type to search"/>
                </template>
                <template slot-scope="scope">
                    <el-button
                    size="mini"
                    @click="handleEdit(scope.$index, scope.row)">Edit</el-button>
                    <el-button
                    size="mini"
                    type="danger"
                    @click="handleDelete(scope.$index, scope.row)">Delete</el-button>
                </template>
                </el-table-column>
            </el-table>
        </div>
    </div>  
</template>

<script>
    export default {

        data() {
            return {
                posts: []
            }
        },

        async fetch() {
            this.posts = await fetch(
                'http://localhost:8000/api/posts'
            ).then(res => res.json())
        },

        methods: {
            handleEdit(index, row) {
                console.log(index, row);
            },
            handleDelete(index, row) {
                console.log(index, row);
            }
        },
    }
</script>

