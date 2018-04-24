<template>
  <v-container fluid>
    <v-slide-y-transition mode="out-in">
      <v-layout column align-center>
        <div>
          <v-btn @click="realizaPeticion" color="success">Petición GetJson</v-btn>
          <v-btn color="error">Error</v-btn>
          <v-btn color="warning">Warning</v-btn>
          <v-btn color="info">Info</v-btn>
          <v-data-table
            :headers="cabeceras"
            :items="partidos"
            hide-actions
            class="elevation-1"
          >
            <template slot="items" slot-scope="props">
              <td>{{ props.item.nombre }}</td>
              <td class="text-xs-right">{{ props.item.dipu }}</td>
              <td class="text-xs-right"><img width="100px" height="50px" :src=" preUrl + props.item.imagen"/></td>
            </template>
          </v-data-table>
        </div>
        <v-form v-model="valid" ref="form" lazy-validation>
          <v-text-field
            label="Name"
            v-model="name"
            :rules="nameRules"
            :counter="10"
            required
          ></v-text-field>
          <v-text-field
            label="E-mail"
            v-model="email"
            :rules="emailRules"
            required
          ></v-text-field>
          <v-select
            label="Item"
            v-model="select"
            :items="items"
            :rules="[v => !!v || 'Item is required']"
            required
          ></v-select>
          <v-checkbox
            label="Do you agree?"
            v-model="checkbox"
            :rules="[v => !!v || 'You must agree to continue!']"
            required
          ></v-checkbox>

          <v-btn
            @click="submit"
            :disabled="!valid"
          >
            submit
          </v-btn>
          <v-btn @click="clear">clear</v-btn>
        </v-form>
      </v-layout>
    </v-slide-y-transition>
    <v-data-table
      :headers="headers"
      :items="listado"
      hide-actions
      class="elevation-1"
    >
      <template slot="items" slot-scope="props">
        <td>{{ props.item.name }}</td>
        <td class="text-xs-right">{{ props.item.calories }}</td>
        <td class="text-xs-right">{{ props.item.fat }}</td>
        <td class="text-xs-right">{{ props.item.carbs }}</td>
        <td class="text-xs-right">{{ props.item.protein }}</td>
        <td class="text-xs-right">{{ props.item.iron }}</td>
      </template>
    </v-data-table>

  </v-container>
</template>
<script>
  import axios from 'axios'
  export default {
    data: () => ({
      valid: true,
      name: '',
      nameRules: [
        v => !!v || 'Name is required',
        v => (v && v.length <= 10) || 'Name must be less than 10 characters'
      ],
      email: '',
      emailRules: [
        v => !!v || 'E-mail is required',
        v => /^\w+([.-]?\w+)*@\w+([.-]?\w+)*(\.\w{2,3})+$/.test(v) || 'E-mail must be valid'
      ],
      select: null,
      items: [
        'Item 1',
        'Item 2',
        'Item 3',
        'Item 4'
      ],
      checkbox: false,
      headers: [
        {
          text: 'Dessert (100g serving)',
          align: 'left',
          sortable: false,
          value: 'name'
        },
        { text: 'Calories', value: 'calories' },
        { text: 'Fat (g)', value: 'fat' },
        { text: 'Carbs (g)', value: 'carbs' },
        { text: 'Protein (g)', value: 'protein' },
        { text: 'Iron (%)', value: 'iron' }
      ],
      listado: [
        {
          value: false,
          name: 'Frozen Yogurt',
          calories: 159,
          fat: 6.0,
          carbs: 24,
          protein: 4.0,
          iron: '1%'
        },
        {
          value: false,
          name: 'Ice cream sandwich',
          calories: 237,
          fat: 9.0,
          carbs: 37,
          protein: 4.3,
          iron: '1%'
        },
        {
          value: false,
          name: 'Eclair',
          calories: 262,
          fat: 16.0,
          carbs: 23,
          protein: 6.0,
          iron: '7%'
        },
        {
          value: false,
          name: 'Cupcake',
          calories: 305,
          fat: 3.7,
          carbs: 67,
          protein: 4.3,
          iron: '8%'
        },
        {
          value: false,
          name: 'Gingerbread',
          calories: 356,
          fat: 16.0,
          carbs: 49,
          protein: 3.9,
          iron: '16%'
        },
        {
          value: false,
          name: 'Jelly bean',
          calories: 375,
          fat: 0.0,
          carbs: 94,
          protein: 0.0,
          iron: '0%'
        },
        {
          value: false,
          name: 'Lollipop',
          calories: 392,
          fat: 0.2,
          carbs: 98,
          protein: 0,
          iron: '2%'
        },
        {
          value: false,
          name: 'Honeycomb',
          calories: 408,
          fat: 3.2,
          carbs: 87,
          protein: 6.5,
          iron: '45%'
        },
        {
          value: false,
          name: 'Donut',
          calories: 452,
          fat: 25.0,
          carbs: 51,
          protein: 4.9,
          iron: '22%'
        },
        {
          value: false,
          name: 'KitKat',
          calories: 518,
          fat: 26.0,
          carbs: 65,
          protein: 7,
          iron: '6%'
        }
      ],
      cabeceras: [
        { text: 'Partido', value: 'nombre' },
        { text: 'Número de Diputados', value: 'dipu' },
        { text: 'Imagen', value: 'imagen' }
      ],
      partidos: [

      ],
      preUrl: 'http://cursosdedesarrollo.com/pactometro/img/'
    }),

    methods: {
      realizaPeticion () {
        axios.get('http://cursosdedesarrollo.com/pactometro/resultados.json')
          .then((response) => {
            this.partidos = response.data
            console.log(this.partidos)
          }, (error) => {
            console.log(error)
          }
        )
      },
      submit () {
        if (this.$refs.form.validate()) {
          // Native form submission is not yet supported
          /*
          axios.post('/api/submit', {
            name: this.name,
            email: this.email,
            select: this.select,
            checkbox: this.checkbox
          })
          */
        }
      },
      clear () {
        this.$refs.form.reset()
      }
    }
  }
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
