<template>
    <div class="hello">
		<input type="text" v-model="input.url" placeholder="URL" />
		<label for="method">Method</label>
		<select id="method" v-model="input.method">
			<option value="GET">GET</option>
			<option value="POST">POST</option>
			<option value="PUT">PUT</option>
			<option value="DELETE">DELETE</option>
		</select>
		<br />
		<label for="data">Data</label>
		<br />
        <input type="textarea" v-model="input.data"/>
        <button  v-on:click="sendData()">Send</button>
        <br />
        <br />
        <textarea>{{ response }}</textarea>
    </div>
</template>

<script>
    import axios from "axios";

    export default {
        name: 'HelloWorld',
        data () {
            return {
                ip: "",
                input: {
					url: "",
                    method: "",
                    data: ""
                },
                response: ""
            }
        },
        mounted() { },
        methods: {
            sendData() {
				console.log(this.method)
                axios({ method: this.input.method, url: this.input.url, data: this.input.data, "headers": { "content-type": "application/json" } }).then(result => {
                    this.response = result.data;
                }, error => {
                    console.error(error);
                });
            }
        }
    }
</script>

<style scoped>
    h1, h2 {
        font-weight: normal;
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

    textarea {
        width: 600px;
        height: 200px;
    }
</style>
