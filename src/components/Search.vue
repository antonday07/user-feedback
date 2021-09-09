<template>
  <div class="search">
      <div class="search__input">
        <svg class="svg-icon search-icon" aria-labelledby="title desc" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 19.9 19.7">
            <title id="title">Search Icon</title>
            <desc id="desc">A magnifying glass icon.</desc><g class="search-path" fill="none" stroke="#848F91">
                <path stroke-linecap="square" d="M18.5 18.3l-5.4-5.4"/><circle cx="8" cy="8" r="7"/></g>
        </svg>
          <input type="text" v-model="search" placeholder="Search..." @keyup="searchList">
      </div>
      <div class="search__filter">
          <div class="dropdown-menu">
              <button type="button" @click="toggleDropdown(isOpenDropdown)">Show all</button>
              <div v-if="isOpenDropdown" class="dropdown-filter">
                  <div class="custom-checkbox">
                      <input class="custom-checkbox-input" type="checkbox" id="planned">
                      <label for="planned">Planned</label>
                  </div>
                 <div class="custom-checkbox">
                      <input class="custom-checkbox-input" type="checkbox" id="inprogress">
                      <label for="inprogress">In progress</label>
                  </div>
                    <div class="custom-checkbox">
                      <input class="custom-checkbox-input" type="checkbox" id="live">
                      <label for="live">Live</label>
                  </div>
              </div>
          </div>
      </div>
  </div>
</template>

<script>
import eventBus from '../event-bus'
export default {
    name: 'Search',
    data() {
        return {
            search: '',
            timer: null,
            isOpenDropdown: false,
        }
    },
    methods: {
        searchList()  {
            if (this.timer) {
                clearTimeout(this.timer)
                this.timer = null
            }
            this.timer = setTimeout(() => {
                eventBus.$emit('searchRequest', this.search)
            }, 800)
        },
        toggleDropdown(status) {
            this.isOpenDropdown = !status
        }
    }
}
</script>

<style lang="scss" scoped>
    .search {
        padding: 20px 0;
        display: flex;
        align-items: center;
        justify-content: space-between;
        border-bottom: 1px solid #f0f0f0;

        &__input {
            display: flex;
            align-items: center;
            position: relative;

            input {
                outline: none;
                border: 0;
                border-radius: 11px;
                background-color: #fafafa;
                padding: 15px 30px;
            }
            svg {
                position: absolute;
                top: 34%;
                left: 7px;
            }
        }

        &__filter {
            display: flex;
         

            .dropdown-menu {
                margin-right: 10px;
                position: relative;

                button {
                    font-family: 'Rubik', sans-serif;
                    font-size: 15px;
                    outline: none;
                    border: 0;
                    padding: 10px 20px;
                    border-radius: 11px;
                    background-color: #fff;
                    cursor: pointer;
                    transition: background .2s;

                    &::after {
                        display: inline-block;
                        width: 0;
                        height: 0;
                        margin-left: 0.255em;
                        vertical-align: 0.255em;
                        content: "";
                        border-top: 0.3em solid;
                        border-right: 0.3em solid transparent;
                        border-bottom: 0;
                        border-left: 0.3em solid transparent;
                    }

                    &:hover {
                        background-color: #fafafa;
                    }
                }

                .dropdown-filter {
                    padding: 0;
                    box-shadow: 0 0.125rem 0.25rem rgb(0 0 0 / 8%) !important;
                    overflow: hidden;
                    border: none;
                    border-radius: 10px;
                    background-color: #fff;
                    position: absolute;
                    left: -38px;
                    top: 40px;
                    z-index: 2000;
                    .custom-checkbox{
                        padding: 10px 25px;
                        cursor: pointer;

                        &:hover {
                            background-color: #fafafa;
                        }
      

                        .custom-checkbox-input {
                            opacity: 0;
                            position: absolute;
                            z-index: -1;
                        }
                        .custom-checkbox-input:checked ~ label::after {
                               background-color: #4855ff;
                        }
                        label {
                            padding: 0 10px;
                            position: relative;
                            font-weight: 400;
                            font-size: 15px;
                            color: #212529; 
                            display: block;
                            cursor: pointer;

                            &::before {
                                position: absolute;
                                left: -12px;
                                top: 0;
                                content: "";
                                width: 15px;
                                height: 15px;
                                border-radius: 5px;
                                background-color: #dee2e6;
                            }
                            &::after {
                                position: absolute;
                                content: "";
                                top: 2px;
                                left: -10px;
                                display: block;
                                width: 10px;
                                height: 10px;
                                border-radius: 12px;
                            }
                        }
                    }
                }
            }
        }

    }


    .svg-icon.search-icon {
        display: inline-block;
        width: 17px;
        height: 17px;
        stroke-width: 2px;
        /* On hover: blue strokes */
        &:focus,
        &:hover {
            .search-path {
                stroke: #299ecc;
            }
        }
     
    }
</style>
