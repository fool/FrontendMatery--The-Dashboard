<template>
    <!-- To note grid-frame does not allow a web page to be scrollable -->
    <div class="grid-y main">
        <div class="large-5 medium-5 small-5 main_top">
            <div class="grid-container grid-x">
                <div class="cell large-1 medium-1 small-0"/>
                <div class="cell large-8 medium-8 small-12 main_top_content_left">
                    <p>Social Media Dashboard
                        <br>
                        <span class="counter">
                           Total Followers :  <ICountUp
                                :delay="delay"
                                :endVal="endVal"
                                :options="options"
                                @ready="onReady"
                        />
                          </span>
                    </p>
                </div>
                <div class="cell large-2 medium-2 small-12 main_top_content_right">
                    <p>Dark Mode <span>
                          <input type="checkbox" id="switch" class="checkbox" v-model="darkMode"/>
                         <label for="switch" class="toggle"></label>
                      </span>
                    </p>

                </div>
                <div class="cell large-1 medium-1 small-0"/>
            </div>
        </div>
        <div class="large-7 medium-7 small-7 main_bottom">
            <div class="grid-container grid-x">
                <div class="cell large-1 medium-1 small-0"/>
                <div class="cell large-10 medium-10 small-12">
                    <Summary></Summary>
                </div>
                <div class="cell large-1 medium-1 small-0"/>
            </div>

            <div class="grid-container grid-x main_bottom_overview">
                <div class="cell large-1 medium-1 small-0"/>
                <div class="cell large-10 medium-10 small-12">
                    <p>Overview - Today</p>
                </div>
                <div class="cell large-1 medium-1 small-0"/>
            </div>

            <div class="grid-container grid-x">
                <div class="cell large-1 medium-1 small-0"/>
                <div class="cell large-10 medium-10 small-12">
                    <Statistics></Statistics>
                </div>
                <div class="cell large-1 medium-1 small-0"/>
            </div>
        </div>
    </div>
</template>

<script>
    import ICountUp from 'vue-countup-v2';
    import Summary from "./components/Summary";
    import Statistics from "./components/Statistics";

    export default {
        name: "App",
        components: {
            ICountUp,
            Summary,
            Statistics
        },
        data() {
            return {
                darkMode: false,
                delay: 1000,
                endVal: 120500,
                options: {
                    useEasing: true,
                    useGrouping: true,
                    separator: ',',
                    decimal: '.',
                    prefix: '',
                    suffix: ''
                }
            }
        },
        watch :{
            darkMode :{
                handler : function()
                {
                    let htmlElement = document.documentElement;
                    if (this.darkMode) {
                        this.$store.commit('SET_APPLICATION_THEME', 'dark');
                        htmlElement.setAttribute('theme', 'dark');
                    } else {
                        this.$store.commit('SET_APPLICATION_THEME', 'light');
                        htmlElement.setAttribute('theme', 'light');
                    }
                }

            }
        },
        methods: {
            onReady: function (instance, CountUp) {
                const that = this;
                instance.update(that.endVal + 100);
            }
        }

    }
</script>

<style scoped>

</style>
