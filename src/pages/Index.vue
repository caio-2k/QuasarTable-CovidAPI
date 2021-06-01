<template>
  <q-page>
    <!-- Componente de tabela do Quasar: -->
    <!-- Columns: é onde iremos configurar as colunas da tabela
    Data: é onde vem os dados para serem exibidos na tabela -->
    <div class="row">
    <q-table
      title="COVID API"
      :data="data"
      :columns="columns"
      row-key="uid"
      class="col"
      separator="cell"
    />
    </div>
  </q-page>
</template>

<script>
export default {
  name: 'PageIndex',

  data () {
    return {
      // Colunas
      columns: [
        // Coluna 1
        {
          name: 'uf',
          label: 'UF',
          field: 'uf',
          align: 'left',
          sortable: true
        },
        // Coluna 2
        {
          // Nome
          name: 'cases',
          label: 'Casos Confirmados',
          field: 'cases',
          align: 'left',
          sortable: true
        },
        // Coluna 3
        {
          // Nome
          name: 'deaths',
          label: 'Mortes',
          field: 'deaths',
          align: 'left',
          sortable: true
        }
      ],
      data: []
    }
  },
  mounted () {
    this.getPosts()
  },

  methods: {
    getPosts () {
      this.$axios.get('https://covid19-brazil-api.vercel.app/api/report/v1')
        .then((res) => {
          this.data = res.data.data
          console.log(res.data)
        })
        .catch((err) => {
          console.log(err)
        })
    }
  }
}
</script>
