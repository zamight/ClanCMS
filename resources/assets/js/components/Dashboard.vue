<template>
<div>
    <!-- Content Header (Page header) -->
    <section class="content-header">
        <h1>
            Dashboard
            <small>Daily digest of statistical data.</small>
        </h1>
        <ol class="breadcrumb">
            <li><a href="#"><i class="fa fa-dashboard"></i> Dashboard</a></li>
            <li class="active">Widgets</li>
        </ol>
    </section>

    <!-- Main content -->
    <div v-if="$gate.isAdminOrAuthor()">
        <section class="content">
            <div class="row">
                <div class="col-lg-4 col-6">
                    <SmallBoxMoreInfo
                        v-bind:header='widgetInfo.user_count'
                        body='Users Count' url='/users'
                        icon='ion ion-ios-people'
                        color='bg-green'>
                    </SmallBoxMoreInfo>
                </div>
                <!-- ./col -->
                <div class="col-lg-4 col-6">
                    <SmallBoxMoreInfo
                        v-bind:header='widgetInfo.category_count'
                        body='Category Count' url='/category'
                        icon='ion ion-locked'
                        color='bg-aqua'>
                    </SmallBoxMoreInfo>
                </div>
                <!-- ./col -->
                <div class="col-lg-4 col-6">
                    <SmallBoxMoreInfo
                        v-bind:header='widgetInfo.forum_count'
                        body='Forum Count' url='/category'
                        icon='ion ion-pie-graph'
                        color='bg-yellow'>
                    </SmallBoxMoreInfo>
                </div>

                </div>
                <div class="row">
                    <!-- ./col -->
                    <div class="col-lg-4 col-6">
                        <SmallBoxMoreInfo
                            v-bind:header='widgetInfo.thread_count'
                            body='Thread Count' url='/category'
                            icon='ion ion-chatbubble-working'
                            color='bg-purple'>
                        </SmallBoxMoreInfo>
                    </div>
                    <!-- ./col -->
                    <div class="col-lg-4 col-6">
                        <SmallBoxMoreInfo
                            v-bind:header='widgetInfo.post_count'
                            body='Post Count' url='/category'
                            icon='ion ion-arrow-graph-up-right'
                            color='bg-teal'>
                        </SmallBoxMoreInfo>
                    </div>
                    <!-- ./col -->
            </div>
        </section>
    </div>

    <div v-if="!$gate.isAdminOrAuthor()">
        <not-found></not-found>
    </div>
</div>
</template>

<script>
import SmallBoxMoreInfo from './Widgets/SmallBoxMoreInfo.vue'
export default {
    data() {
        return {
            widgetInfo: ''
        }
    },
    components: {
        SmallBoxMoreInfo
    },
    mounted() {
        console.log('Component mounted.')
        this.loadSetting();
    },
    methods: {
        loadSetting() {
            axios.get(this.$site_url_address + 'api/dashboard').then(response => {
                this.widgetInfo = response.data;
                console.log(this.widgetInfo);
                console.log(this.widgetInfo.userCount);
            });
        },
        created() {
            this.loadSetting();
            //setInterval(() => this.loadSetting(), 3000);
        }
    }
}
</script>
