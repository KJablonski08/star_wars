<template>
	<div>
    <!-- SELECT FORM --> 
        <b-form-select v-model="selected" :options="options" size="sm" class="mt-3 w-50 p-3 mb-1 bg-secondary text-light" v-on:change="updateResults" ></b-form-select>
        <div class="mt-3" v-if="selected">Selected: <strong>{{ selected.toUpperCase() }}</strong></div>
        <div class="d-flex justify-content-center">
            <b-form-input list="my-list-id"  v-show="results" class="w-50" v-on:input="filterList"></b-form-input>

			<datalist id="my-list-id" v-if="selected === 'films'">
				<option v-for="(item, index) in results" :key="index">{{
					item.title
				}}</option>
			</datalist>

            <datalist id="my-list-id" v-if="selected !== 'films'">
				<option v-for="(item, index) in results" :key="index">{{
					item.name
				}}</option>
			</datalist>
        </div>
    
    <!-- ACCORDION --> 
        <div class="accordion" role="tablist" v-for="(item, index) in results" :key="index" v-show="search === item.name || search === null || search === '' || item.name.includes(search)">
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
            search: null,
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
       },
       filterList() {
			this.search = event.target.value;
		},
    },
    }
</script>

<style scoped></style>
