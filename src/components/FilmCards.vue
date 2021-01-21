<template>
	<div>

    <!-- DARK -->

    <div v-show="!this.mode">

    <!-- SELECT FORM --> 

        <h4 class="mt-3 dark">Welcome! Select the Star Wars data that you'd like to know more about...</h4>
        <b-form-select v-model="selected" :options="options" size="sm" class="mt-3 w-50 p-3 mb-1 bg-dark text-light" v-on:change="updateResults">
        </b-form-select>
        <div class="mt-3 mb-3" v-if="selected">Selected: <strong>{{ selected.toUpperCase() }}</strong></div>

        <!-- DATALIST - FILTER -->

        <div class="d-flex justify-content-center">
            <b-form-input list="my-list-id"  v-show="results && selected !== 'films'" class="w-50 mb-3 bg-dark" v-on:input="filterList" placeholder="Filter here..."></b-form-input>

            <!-- IF FILMS (api does not have item.name for films) -->

			<datalist id="my-list-id" v-if="selected === 'films'">
				<option v-for="(item, index) in results" :key="index">{{
					item.title
				}}</option>
			</datalist>

            <!-- ALL OTHER ENDPOINTS USE item.name -->

            <datalist id="my-list-id" v-if="selected !== 'films'">
				<option v-for="(item, index) in results" :key="index">{{
					item.name
				}}</option>
			</datalist>
        </div>
    
    <!-- ACCORDION --> 

        <div class="accordion" role="tablist" v-for="(item, index) in results" :key="index" v-show="search === item.name || search === null || search === '' || item.name.includes(search)">
            <b-card no-body class="mb-1">

                 <!-- Header with title for films (no item.name in films endpoint) --> 

                <b-card-header header-tag="header" class="p-1" role="tab">
                    <b-button block v-b-toggle="'collapse' + index" variant="dark" v-if="selected === 'films'">{{item.title}}</b-button>
                </b-card-header>

                <!-- Header with name for all other endpoints (no item.name in films endpoint) -->

                <b-card-header header-tag="header" class="p-1" role="tab">
                    <b-button block v-b-toggle="'collapse' + index" variant="dark" v-if="selected !== 'films'">{{item.name}}</b-button>
                </b-card-header>
                <b-collapse :id="'collapse' + index" accordion="my-accordion" role="tabpanel">
                    <b-card-body>
                        <b-card-text v-for="(key, value) in item" :key="value">

                            <!-- removed created, edited, and release_date keys-->

                            <div v-if="value !== 'created' && value !== 'edited' && value !== 'release_date'">   
                                <strong>{{value.toUpperCase()}}</strong> : {{key}}
                            </div>

                            <!-- showing only release_date on films - reformatted using moment-->

                            <div v-if="value === 'release_date'">   
                                <strong>{{value.toUpperCase()}}</strong> : {{moment(new Date(key)).format('MMMM Do YYYY')}}
                            </div>
                        </b-card-text>
                    </b-card-body>
                </b-collapse>
            </b-card>
        </div>
    </div>

    <!-- LIGHT -->

    <div v-show="this.mode">

        <!-- SELECT FORM --> 

        <h4 class="mt-3 dark">Welcome, Select the Star Wars data would you like to know more about...</h4>
        <b-form-select v-model="selected" :options="options" size="sm" class="mt-3 w-50 p-3 mb-1 bg-light text-dark" v-on:change="updateResults">
        </b-form-select>
        <div class="mt-3 mb-3" v-if="selected">Selected: <strong>{{ selected.toUpperCase() }}</strong></div>

        <!-- DATALIST - FILTER -->

        <div class="d-flex justify-content-center">
            <b-form-input list="my-list-id"  v-show="results && selected !== 'films'" class="w-50 mb-3 bg-light" v-on:input="filterList" placeholder="Filter here..."></b-form-input>

             <!-- IF FILMS (api does not have item.name for films) -->

			<datalist id="my-list-id" v-if="selected === 'films'">
				<option v-for="(item, index) in results" :key="index" class="bg-light">{{
					item.title
				}}</option>
			</datalist>

            <!-- Header with name for all other endpoints (no item.name in films endpoint) -->

            <datalist id="my-list-id" v-if="selected !== 'films'">
				<option v-for="(item, index) in results" :key="index">{{
					item.name
				}}</option>
			</datalist>
        </div>
    
    <!-- ACCORDION --> 

        <div class="accordion" role="tablist" v-for="(item, index) in results" :key="index" v-show="search === item.name || search === null || search === '' || item.name.includes(search)">
            <b-card no-body class="mb-1">

                 <!-- Header with title for films (no item.name in films endpoint) --> 

                <b-card-header header-tag="header" class="p-1" role="tab">
                    <b-button block v-b-toggle="'collapse' + index" variant="light" v-if="selected === 'films'">{{item.title}}</b-button>
                </b-card-header>

                <!-- Header with name for all other endpoints (no item.name in films endpoint) -->

                <b-card-header header-tag="header" class="p-1" role="tab">
                    <b-button block v-b-toggle="'collapse' + index" variant="light" v-if="selected !== 'films'">{{item.name}}</b-button>
                </b-card-header>

                <b-collapse :id="'collapse' + index" accordion="my-accordion" role="tabpanel">

                    <b-card-body>
                        <b-card-text v-for="(key, value) in item" :key="value">

                            <!-- removed created, edited, and release_date keys-->

                            <div v-if="value !== 'created' && value !== 'edited' && value !== 'release_date'">   
                                <strong>{{value.toUpperCase()}}</strong> : {{key}}
                            </div>

                            <!-- showing only release_date on films - reformatted using moment-->

                            <div v-if="value === 'release_date'">   
                                <strong>{{value.toUpperCase()}}</strong> : {{moment(new Date(key)).format('MMMM Do YYYY')}}
                            </div>
                        </b-card-text>
                    </b-card-body>

                </b-collapse>
            </b-card>
        </div>
    </div>

	</div>
</template>

<script>
    import moment from 'moment';
    import axios from 'axios';
    export default {
	props: {
		mode: {
			type: Boolean,
		},
	},
    data() {
		return {
			results: null,
            count: null,
            selected: null,
            search: null,
            options: [
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
			.get("https://swapi.dev/api/" + this.selected + "/")
			.then((response) => (this.results = response.data.results))
       },
       filterList() {
			this.search = event.target.value;
		},
        moment: function () {
            return moment();
  }
    },
    }
</script>
<style scoped></style>
