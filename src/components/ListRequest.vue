<template>
    <div class="list-request">
        <div v-if="listFilter.length">
            <Request v-for="(request, index) in listFilter" :key="index" :request="request"/>
        </div>
        <div v-if="!listFilter.length">
            <p class="not-found">We didn’t find any posts with the same topic. You’re good to go! 🙌</p>
        </div>
    </div>
</template>

<script>
import eventBus from '../event-bus'
import Request from './Request.vue'
export default {
    name: 'ListRequest',
    components: {
        Request
    },
    data() {
        return {
            listRequest: [],
            keySearch: '',
        }
    },
    mounted() {
        if(localStorage.listRequestStorage) {
            this.listRequest = JSON.parse(localStorage.listRequestStorage)
        }
    },
    watch: {
        listRequest: {
            handler(newItem) {
                localStorage.listRequestStorage = JSON.stringify(newItem)
            }, 
            deep: true
        }
    },
    computed: {
        listFilter() {
            return this.listRequest.filter((request) => {
                return request.title.toLowerCase().includes(this.keySearch.toLowerCase())
            })
        }
    },
    created() {
        eventBus.$on('addRequest', (item) => {
            this.listRequest.push(item)
        })
        eventBus.$on('searchRequest', (keyword) => {
            this.keySearch = keyword
        })
    },
   
}
</script>

<style lang="scss" scoped>
    .list-request {    
    }
    .not-found {
        text-align: center;
        margin: 10px;
    }
</style>