<template>
  <div class="form-request">
      <h3 class="form-request__title">
          Feature request
      </h3>
      <p class="form-request__text">
          Help us improve our product 💪
      </p>
      <form 
        @submit.prevent="handleRequest"
        action=""
        >
          <div class="input-group">
              <label for="title">Title</label>
              <input type="text" id="title" v-model="title" placeholder="Short, descriptive title">
          </div>
           <div class="input-group">
              <label for="detail">Details</label>
              <textarea id="detail" cols="30" rows="10" v-model="detail" placeholder="All the additional details here..."></textarea>
          </div>
          <input type="submit" :disabled="isDisable" value="Submit" class="btn">
      </form>
  </div>
</template>

<script>
    import eventBus from '../event-bus'
    import generateID from '../utils/uniqueID'
    export default {
        name: 'FormRequest',
        data() {
            return {
                title: '',
                detail: '',
                vote: 0,
            }
        },
        computed : {
            isDisable() {
                return this.title.length === 0 || this.detail.length === 0
            }
        },
        methods: {
            handleRequest() {

                eventBus.$emit('addRequest', {
                    id: generateID(),
                    title: this.title,
                    detail: this.detail,
                    vote: this.vote,
                    isVote: false
                })
                localStorage.listRequestStorage = JSON.stringify([])
                this.title = ''
                this.detail = ''
            }
        }
    }
</script>

<style lang="scss" scoped>
    .form-request {
        flex: 0 0 32%;
        padding: 20px;
        border-radius: 7px;
        background-color: #fafafa;

        &__title {
            margin-bottom: 7px;
        }
        &__text {
            margin-bottom: 15px;
        }
    }
    form {
     
    }

    .input-group {
        background-color: #fff; 
        margin-bottom: 15px;
        padding: 10px;
        display: flex;
        flex-direction: column;
        border: 1px solid #eee;
        border-radius: 8px;

        label {
            font-weight: 400;
            font-size: 16px;
            margin-bottom: 10px;
        }
        input {
            outline: none;
            border: 0;
           
        }
        textarea {
            border: 0;
            outline: none;
        }
    }
    input.btn {
        float: right;
        font-weight: 400;
        text-transform: uppercase;
        color: #fff;
        background-color: #4855FF;
        border-radius: 12px;
        border: 0;
        outline: none;
        padding: 12px 18px;
        cursor: pointer;
        transition: opacity .2s ;
    }
    input.btn:hover {
        opacity: .8;
    }
    input:disabled {    
        opacity: .5;
        cursor: default;
        pointer-events: none;
    }

</style>