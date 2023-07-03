<template>
    <div class="container mt-5">

        <div class="row mb-5">
            <div class="">Выберите период</div>
            <div class="col-md-4">
                <div class="form-group">
                    <input type="date" class="form-control" v-model="start_date" />
                </div>
            </div>
            <div class="col-md-4">
                <div class="form-group">
                    <input type="date" class="form-control" v-model="end_date" />
                </div>  
            </div>
        </div>


        <h3>Транзакции</h3>


        <table class="table table-striped table-hover mt-5">
            <thead>
                <tr>
                    <th scope="col">#</th>
                    <th scope="col">Работник</th>
                    <th scope="col">Сумма в долларах (Если списано)</th>
                    <th scope="col">Статус</th>
                </tr>
            </thead>
            <tbody v-if="transactions">
                <tr v-for="transaction in transactions" :key="transaction.id">
                    <th scope="row">{{ transaction.id }}</th>
                    <td>{{ transaction.referal }}</td>
                    <td v-if="transaction.status === 'pending'">
                        <input type="text" class="form-control form-control-sm" placeholder="Сумма в долларах" v-model="transaction.amount" @change="updateAmount(transaction.uuid)" />
                    </td>
                    <td v-else>{{ transaction.amount }}</td>
                    <td class="fw-bold">{{ getStatus(transaction.status) }}</td>
                    <td v-if="transaction.status === 'pending'">
                        <button class="btn btn-sm btn-success" @click="setStatus('approved', transaction.uuid)">Списано</button>
                        <button class="btn btn-sm btn-danger" @click="setStatus('declined', transaction.uuid)">Не удачно</button>
                    </td>
                </tr>
            </tbody>
        </table>



        <h3 class="mt-5">Статистика по работникам</h3>
        <div>Общая сумма: {{ earn.totalEarn }} USDT</div>
        <table class="table table-striped table-hover mt-5">
            <thead>
                <tr>
                    <th scope="col">Работник</th>
                    <th scope="col">Сумма в долларах</th>
                </tr>
            </thead>
            <tbody v-if="transactions">
                <tr v-for="transaction in earn.transactions" :key="transaction.id">
                    <td>{{ transaction.referal }}</td>
                    <td>{{ transaction.totalAmount }}</td>
                </tr>
            </tbody>
        </table>


    </div>
</template>
<script>
export default {
    layout: 'statistics',
    head() {
        return {
            title: 'Statistics',
            meta: [
                { hid: 'description', name: 'description', content: 'Statistics' }
            ],
            link: [
                { rel: 'stylesheet', href: 'https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css' }
            ]
        }
    },

    data() {
        return {
            transactions: [],
            earn: [],
            start_date: this.$route.query.start_date || '',
            end_date: this.$route.query.end_date || ''
        }
    },

    watch: {
        start_date() {
            this.$router.push({ query: { start_date: this.start_date, end_date: this.end_date } })
            this.fetchStatistics();
            this.fetchEarnStatistics();
        },
        end_date() {
            this.$router.push({ query: { start_date: this.start_date, end_date: this.end_date } })
            this.fetchStatistics();
            this.fetchEarnStatistics();
        }
    },

    async mounted() {
        await this.fetchStatistics();
        await this.fetchEarnStatistics();
    },

    methods: {
        async fetchEarnStatistics() {
            try {
                let start_date = this.$route.query.start_date
                let end_date = this.$route.query.end_date
                const { data: res } = await this.$axios.get('/public/get-earn-statistics', {
                    params: {
                        start_date,
                        end_date
                    }
                });
                if(res.success) {
                    this.earn = res.data;
                }
            } catch (error) {
                console.log(error);
            }
        },

        async fetchStatistics() {
            try {
                let start_date = this.$route.query.start_date
                let end_date = this.$route.query.end_date
                const { data: res } = await this.$axios.get('/public/get-statistics', {
                    params: {
                        start_date,
                        end_date
                    }
                });
                if(res.success) {
                    this.transactions = res.data;
                }
            } catch (error) {
                console.log(error);
            }
        },

        async setStatus(status, uuid) {
            const { data: res } = await this.$axios.post('/public/set-status', {
                status,
                uuid
            });
            if(res.success) {
                await this.fetchStatistics();
            }
        },


        async updateAmount(uuid) {
            let transaction = this.transactions.find(transaction => transaction.uuid === uuid);
            const { data: res } = await this.$axios.post('/public/update-amount', {
                amount: transaction.amount,
                uuid
            });
            if(res.success) {
                
            }
        },

        getStatus(status) {
            switch(status) {
                case 'pending':
                    return 'В ожидании';
                case 'approved':
                    return 'Списано';
                case 'declined':
                    return 'Не удачно';
                default:
            }
        }


    }
}
</script>