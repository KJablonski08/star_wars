<template>
	<div>
    <!-- SELECT FORM --> 
        <b-form-select v-model="selected" :options="options" size="sm" class="mt-3 w-50 p-3 mb-1 bg-secondary text-light" v-on:change="updateResults" ></b-form-select>
        <div class="mt-3">Selected: <strong>{{ selected }}</strong></div>
    <!-- ACCORDION --> 
        <div class="accordion" role="tablist" v-for="(item, index) in results" :key="index">
            <b-card no-body class="mb-1">
                <b-card-header header-tag="header" class="p-1" role="tab">
                    <b-button block v-b-toggle="'collapse' + index" variant="dark" v-if="selected === 'films'">{{item.title}}</b-button>
                </b-card-header>
                <b-card-header header-tag="header" class="p-1" role="tab">
                    <b-button block v-b-toggle="'collapse' + index" variant="dark" v-if="selected !== 'films'">{{item.name}}</b-button>
                </b-card-header>
                <b-collapse :id="'collapse' + index" accordion="my-accordion" role="tabpanel">
                    <b-card-body>
                        <b-card-text v-for="(key, value) in item" :key="value"><strong>{{value.toUpperCase()}}</strong> : {{key}}</b-card-text>
                    </b-card-body>
                </b-collapse>
            </b-card>
        </div>
	</div>
</template>

<script>
    import axios from 'axios';
    export default {
	props: {
		endPoint: {
			type: Object,
		},
	},
    data() {
		return {
			results: null,
            selected: null,
            options: [
                { value: null, text: 'Please select an option' },
                { value: 'films', text: 'films' },
                { value: 'planets', text: 'planets' },
                { value: 'starships', text: 'starships' },
                { value: 'vehicles', text: 'vehicles' },
                { value: 'people', text: 'people'},
                {value: 'species', text: 'species'}
            ],
        }
	},
    methods: {
       updateResults() {
           axios
			.get("http://swapi.dev/api/" + this.selected + "/")
			.then((response) => (this.results = response.data.results))
       } 
    },
    }
</script>

<style scoped></style>
