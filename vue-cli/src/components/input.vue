<template>
  <div>
    <!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script src="https://unpkg.com/vue@latest"></script>
    <script src="https://unpkg.com/element-plus"></script>
    <script src="https://unpkg.com/axios@1.1.2/dist/axios.min.js"></script>
    <link rel="stylesheet" href="https://unpkg.com/element-plus/dist/index.css">
</head>

<body>
    <div id="app">
        <el-input placeholder="City or State" v-model="input" @input="trimSpace" ref="inputEle" clearable>
        </el-input>
        <ul class="already" v-if="input.trim() !== '' ">
            <li v-for="item,idx in afterSearchCity" :key="idx">
                <span class="name"><span class="hl">{{item.city}}</span>,<span class="hl">{{item.state}}</span></span>
                <span class="population" v-text="numberWithCommas(item.population)"></span>
            </li>
        </ul>
        <ul class="suggestions"  v-if="input.trim() === '' ">
            <li>Filter for a city</li>
            <li>or a state</li>
        </ul>
        <div v-if="messageNoResult">
            沒有符合的項目
        </div>
    </div>

    <script>
        const app = Vue.createApp({
            data() {
                return {
                    messageNoResult:'',
                    cities: [],
                    afterSearchCity: [],
                    input: '',
                    api: 'https://gist.githubusercontent.com/Miserlou/c5cd8364bf9b2420bb29/raw/2bf258763cdddd704f8ffd3ea9a3e81d25e2c6f6/cities.json'
                }
            },
            watch: {
                input: {
                    handler(val, oldVal) {
                        this.afterSearchCity = this.cities.filter((item, index) => {
                            const regex = new RegExp(val, 'gi');
                            return item.city.match(regex) || item.state.match(regex);
                        })
                    }
                },
                afterSearchCity:{
                    handler(val, oldVal){
                        if(val.length === 0){
                            this.messageNoResult = true;
                        }else{
                            this.messageNoResult = false;
                        }
                    }

                }
            },
            computed: {
            },
            methods: {
                trimSpace(){
                    this.input = this.input.replace(/^\s/,'');
                },
                numberWithCommas(x) {
                    return x.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ',');
                },
                async getApi() {
                    axios.get(this.api)
                        .then((response) => {
                            let dataArr = response.data;
                            this.cities = dataArr;
                        })
                        .catch((error) => { })
                },

            },
            mounted() {
                this.getApi();
            }
        });

        app.use(ElementPlus);
        app.mount("#app");
    </script>
</body>

</html>



<!-- ------------------------------------------------------------------- -->

<!-- <!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>Type Ahead 👀</title>
    <link rel="stylesheet" href="style.css">
</head>

<body>

    <form class="search-form">
        <input type="text" class="search" placeholder="City or State">
        <ul class="suggestions">
            <li>Filter for a city</li>
            <li>or a state</li>
        </ul>
    </form>
    <script>
        const endpoint = 'https://gist.githubusercontent.com/Miserlou/c5cd8364bf9b2420bb29/raw/2bf258763cdddd704f8ffd3ea9a3e81d25e2c6f6/cities.json';

        const cities = [];
        fetch(endpoint)
            .then(blob => blob.json())
            .then(data => cities.push(...data));

        function findMatches(wordToMatch, cities) {
            return cities.filter(place => {
                // here we need to figure out if the city or state matches what was searched
                const regex = new RegExp(wordToMatch, 'gi');
                return place.city.match(regex) || place.state.match(regex)
            });
        }

        function numberWithCommas(x) {
            return x.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ',');
        }

        function displayMatches() {
            const matchArray = findMatches(this.value, cities);
            const html = matchArray.map(place => {
                const regex = new RegExp(this.value, 'gi');
                const cityName = place.city.replace(regex, `<span class="hl">${this.value}</span>`);
                const stateName = place.state.replace(regex, `<span class="hl">${this.value}</span>`);
                return `
        <li>
          <span class="name">${cityName}, ${stateName}</span>
          <span class="population">${numberWithCommas(place.population)}</span>
        </li>
      `;
            }).join('');
            suggestions.innerHTML = html;
        }

        const searchInput = document.querySelector('.search');
        const suggestions = document.querySelector('.suggestions');

        searchInput.addEventListener('change', displayMatches);
        searchInput.addEventListener('keyup', displayMatches);

    </script>
</body>

</html> -->
  </div>
</template>

<script>
export default {
    props:['id'],
methods:{
replace:function(id){
this.$router.push({ path: id }) 
}

}

}
</script>

<style>

</style>