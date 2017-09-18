<template>
    <div class="main wrap clearfix">
        <div class="main-left">
            <div class="card card-answer">
                <div class="answer-content">
                    <div class="article-content">
                        <h3 class="about-title">关于团队</h3>
                        <div class="flex-item">
                            <div class="flex-label">团队：</div>
                            <div class="flex-content">新餐饮前端组</div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <div class="main-right">
            <trending :trending="trending"></trending>
        </div>
    </div>
</template>
<script lang="babel">
import { mapGetters } from 'vuex'
import metaMixin from '~mixins'
import trending from '../components/aside-trending.vue'

const fetchInitialData = async store => {
    await store.dispatch('frontend/article/getTrending')
}

export default {
    name: 'frontend-index',
    prefetch: fetchInitialData,
    mixins: [metaMixin],
    components: {
        trending
    },
    computed: {
        ...mapGetters({
            trending: 'frontend/article/getTrending'
        })
    },
    mounted() {
        if (this.trending.length <= 0) {
            fetchInitialData(this.$store)
        } else {
            this.$store.dispatch('global/gProgress', 100)
        }
    },
    metaInfo () {
        return {
            title: 'xcyfed',
            meta: [{ vmid: 'description', name: 'description', content: 'xcyfed' }]
        }
    }
}
</script>
