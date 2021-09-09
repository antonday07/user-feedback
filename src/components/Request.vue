<template>
  <div class="request">
      <div class="upvote" @click="upvote(request.isVote)">
          <svg viewBox="0 0 18 12" xmlns="http://www.w3.org/2000/svg" :class="{isVote: request.isVote}">
            <path d="M17.396 11.194c.333.445.16.806-.39.806H.994c-.548 0-.724-.36-.39-.806L8.397.806C8.73.36 9.27.36 9.604.806l7.792 10.388z" 
                fill="currentColor" fill-rule="evenodd">
            </path>
          </svg>
          <span>{{ request.vote }}</span>
      </div>    
      <div class="content">
          <h3>{{ request.title }}</h3>
          <p>{{ request.detail }}</p>
      </div>
  </div>

</template>

<script>
// import eventBus from '../event-bus'
export default {
    name: 'Request',
    props: {
        request: {
            type: Object,
            required: true
        }
    },
    data() {
        return {

        }
    },
    methods: {
        upvote(voted) {
            if(voted) {
                this.request.vote--
                this.request.isVote = !voted
                return
            }
            this.request.vote++
            this.request.isVote = !voted
        }
    }
}
</script>

<style lang="scss" scoped>
    .request {
        display: flex;
        align-items: center;
        padding: 20px;
        border-bottom: 1px solid #f0f0f0;
        
    }
    .upvote {
        display: flex;
        margin-right: 30px;
        flex-direction: column;
        align-items: center;
        cursor: pointer;

        svg {
            width: 18px;
            height: 12px;
            margin-bottom: 5px;  
            color: #4b587c;
        }
        svg.isVote {
            color: #4855FF;
            //color: #f64900;
        }
        span{

        }

    }
    .content {

        h3 {
            margin-bottom: 10px;
        }
        p {
            color: #464646;
        }
    }
</style>