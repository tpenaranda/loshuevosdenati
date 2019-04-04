<template>
    <div class="col-md-12">
        <md-table v-model="orders" md-sort="id" md-sort-order="asc" md-card>
          <md-table-toolbar><h1 class="md-title">Pedidos</h1></md-table-toolbar>
          <md-table-row slot="md-table-row" slot-scope="{ item }">
            <md-table-cell md-label="#" md-sort-by="id" md-numeric>{{ item.id }}</md-table-cell>
            <md-table-cell md-label="Fecha">{{ item.created_at | formatCreatedAt }}</md-table-cell>
            <md-table-cell md-label="Nombre">{{ item.user.name }}</md-table-cell>
            <md-table-cell md-label="Teléfono">{{ item.user.phone }}</md-table-cell>
            <md-table-cell md-label="Huevos">{{ item.skus | formatSkus }}</md-table-cell>
          </md-table-row>
        </md-table>
    </div>

</template>

<script>
    import moment from 'moment-timezone'
    import { validationMixin } from 'vuelidate'
    import {
        between,
        integer,
        maxLength,
        minLength,
        minValue,
        required
    } from 'vuelidate/lib/validators'

    export default {
        name: 'MainComponent',
        mixins: [
            validationMixin
        ],
        components: {
        },
        filters: {
            formatCreatedAt (value) {
                let output = moment.tz(value, 'UTC').tz(moment.tz.guess()).locale('es').calendar()

                return output.substr(0,1).toUpperCase() + output.substr(1);
            },
            formatSkus (skus) {
                return skus.map((sku) => `${sku.name} (${sku.data['text']}) [${sku.data['flavor']}]`).join(" - ")
            }
        },
        data: () => ({
            orders: [],
            errorLoadingOrders: false,
            loadingOrders: null,
        }),
        computed: {
        },
        mounted () {
            this.getOrders()
        },
        methods: {
            getOrders() {
                this.loadingOrders = true
                this.axios.get('/api/orders').then((response) => {
                    this.orders = response.data
                }).catch((error) => {
                    this.errorDialogOrders = true
                }).finally((response) => {
                    this.loadingOrders = false
                })
            },
        }
    }
</script>

<style lang="scss" scoped>
</style>