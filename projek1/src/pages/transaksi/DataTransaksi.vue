<template xmlns:v-slot="http://www.w3.org/1999/XSL/Transform">
    <div class="q-pa-md">
        <q-table
                title="Treats"
                :data="data"
                :columns="columns"
                row-key="id"
                :filter="filter"
                :loading="loading"
        >

            <template v-slot:top>

                <span class="text-h5 text-weight-light q-pa-md">
        <span class="text-blue-grey-14">Data Transaksi</span>
      </span>

                <q-space />
                <q-input borderless dense debounce="300" color="primary" v-model="filter">
                    <template v-slot:append>
                        <q-icon name="search" />
                    </template>
                </q-input>
            </template>

        </q-table>
    </div>
</template>
<script>
    export default {
        data () {
            return {
                loading: false,
                filter: '',
                rowCount: 10,
                columns: [
                    {
                        name: 'desc',
                        required: true,
                        label: 'Kode Transaksi',
                        align: 'left',
                        field: row => row.kodetrx,
                        format: val => `${val}`,
                        sortable: true
                    },
                    { name: 'kodetrx', align: 'center', label: 'Judul Buku', field: 'kodetrx', sortable: true },
                    { name: 'namapenerbit', align: 'center', label: 'Nama Penerbit', field: 'namapenerbit', sortable: true },
                    { name: 'judulbuku', label: 'Judul Buku', align: 'center', field: 'judulbuku' },
                    { name: 'hargabuku', label: 'Harga Buku', align: 'center', field: 'hargabuku' },
                    { name: 'jumbeli', label: 'Jumlah Beli', align: 'center', field: 'jumbeli' },
                    { name: 'total', label: 'Total', align: 'center', field: 'total' }
                ],
                data: [
                    {
                        kodetrx: 'Trans001',
                        namapenerbit: 'John Petrucci',
                        judulbuku: 'Pemrograman 3',
                        hargabuku: '250000',
                        jumbeli: '2',
                        total:'500000'
                    },
                    {
                        kodetrx: 'Trans002',
                        namapenerbit: 'Yngwie Malmsteen',
                        judulbuku: 'Pemrograman 3',
                        hargabuku: '250000',
                        jumbeli: '1',
                        total:'500000'
                    },
                    {
                        kodetrx: 'Trans003',
                        namapenerbit: 'Slash',
                        judulbuku: 'Prak.Pemrograman 3',
                        hargabuku: '350000',
                        jumbeli: '3',
                        total:'1050000'
                    }
                ]
            }
        },

        methods: {
            // emulate fetching data from server
            addRow () {
                this.loading = true
                setTimeout(() => {
                    const
                        index = Math.floor(Math.random() * (this.data.length + 1)),
                        row = this.original[Math.floor(Math.random() * this.original.length)]
                    if (this.data.length === 0) {
                        this.rowCount = 0
                    }
                    row.id = ++this.rowCount
                    const addRow = { ...row } // extend({}, row, { name: `${row.name} (${row.__count})` })
                    this.data = [ ...this.data.slice(0, index), addRow, ...this.data.slice(index) ]
                    this.loading = false
                }, 500)
            },

            removeRow () {
                this.loading = true
                setTimeout(() => {
                    const index = Math.floor(Math.random() * this.data.length)
                    this.data = [ ...this.data.slice(0, index), ...this.data.slice(index + 1) ]
                    this.loading = false
                }, 500)
            }
        }
    }
</script>