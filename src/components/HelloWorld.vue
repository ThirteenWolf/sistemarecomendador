<template>
  <v-container>
    <v-toolbar app>
      <v-toolbar-title class="headline text-uppercase">
        <span>Recomendador de mascotas</span>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn
        color="primary"
        dark
        @click="dialog = true"
      >
        <span class="mr-2">Obtener Recomendación</span>
      </v-btn>
    </v-toolbar>

    <v-dialog v-model="dialog" max-width="600px">
      <v-card>
        <v-card-title>
          <span class="headline">Obten tu recomendación</span>
        </v-card-title>
        <v-card-text>
          <v-form ref="form" v-model="valid" lazy-validation>
            <v-text-field
              v-model="nombre"
              :rules="reglasNombre"
              label="Nombre"
              required
              row
            ></v-text-field>
            <v-radio-group 
              v-model="vivienda" 
              :rules="reglasVivienda" 
              required
              row
            >
              <div slot="label">¿Qué tipo de vivienda habitas?</div>
              <v-radio value=1>
                <div slot="label">Casa</div>
              </v-radio>
              <v-radio value=0>
                <div slot="label">Departamento</div>
              </v-radio>
            </v-radio-group>
            <v-radio-group 
              v-model="patio"
              :rules="reglasPatio" 
              required
              row
            >
              <div slot="label">¿El lugar donde vives cuenta con patio?</div>
              <v-radio value=2>
                <div slot="label">Si</div>
              </v-radio>
              <v-radio value=0>
                <div slot="label">No</div>
              </v-radio>
            </v-radio-group>
            <v-radio-group 
              v-model="ocupacion"
              :rules="reglasOcupacion" 
              required
              row
            >
              <div slot="label">¿A qué se dedica?</div>
              <v-radio value=3>
                <div slot="label">Trabajador</div>
              </v-radio>
              <v-radio value=0>
                <div slot="label">Estudiante</div>
              </v-radio>
            </v-radio-group>
            <v-radio-group 
              v-model="genero"
              :rules="reglasGenero" 
              required
              row
            >
              <div slot="label">Género</div>
              <v-radio value=4>
                <div slot="label">Hombre</div>
              </v-radio>
              <v-radio value=0>
                <div slot="label">Mujer</div>
              </v-radio>
            </v-radio-group>
            <v-radio-group 
              v-model="activFisica"
              :rules="reglasActivFisica" 
              required
              row
            >
              <div slot="label">¿Practica alguna actividad física?</div>
              <v-radio value=5>
                <div slot="label">Si</div>
              </v-radio>
              <v-radio value=0>
                <div slot="label">No</div>
              </v-radio>
            </v-radio-group>
            <v-radio-group 
              v-model="compra"
              :rules="reglasCompra" 
              required
              row
            >
              <div slot="label">¿Piensa que la compra de animales es una mala práctica?</div>
              <v-radio value=6>
                <div slot="label">Si</div>
              </v-radio>
              <v-radio value=0>
                <div slot="label">No</div>
              </v-radio>
            </v-radio-group>
          </v-form>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn
            color="blue darken-1"
            flat
            :disabled="!valid"
            @click="submit"
          >
            Obtener Recomendación
          </v-btn>
          <v-btn @click="clear">Limpiar</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>

    <v-layout
      text-xs-center
      align-center
      wrap
    >
      <v-flex xs12>
        <v-toolbar class="elevation-1">
          <v-toolbar-title>Datos de entrenamiento</v-toolbar-title>
        </v-toolbar>
        <v-data-table
          :headers="headers1"
          :items="x"
          class="elevation-1"
        >

        <template slot="items" slot-scope="props">
          <td>{{props.item[0]}}</td>
          <td>
            <span v-if="props.item[3] == 0">
              Departamento
            </span>
            <span v-else>
              Casa
            </span>
          </td>
          <td>
            <span v-if="props.item[4] == 0">
              No
            </span>
            <span v-else>
              Sí
            </span>
          </td>
          <td>
            <span v-if="props.item[5] == 0">
              Estudiante
            </span>
            <span v-else>
              Trabaja
            </span>
          </td>
          <td>
            <span v-if="props.item[6] == 0">
              Mujer
            </span>
            <span v-else>
              Hombre
            </span>
          </td>
          <td>
            <span v-if="props.item[7] == 0">
              No
            </span>
            <span v-else>
              Sí
            </span>
          </td>
          <td>
            <span v-if="props.item[8] == 0">
              No
            </span>
            <span v-else>
              Sí
            </span>
          </td>
          <td>{{props.item[2]}}</td>
        </template>

        </v-data-table>
      </v-flex>

      <v-flex xs12 class="mt-3">
        <v-toolbar class="elevation-1">
          <v-toolbar-title>Datos de prueba</v-toolbar-title>
        </v-toolbar>

        <v-data-table
          :headers="headers2"
          :items="recomendaciones"
          class="elevation-1"
        >

        <template slot="items" slot-scope="props">
          <td>{{props.item[0]}}</td>
          <td>
            <span v-if="props.item[1] == 0">
              Departamento
            </span>
            <span v-else>
              Casa
            </span>
          </td>
          <td>
            <span v-if="props.item[2] == 0">
              No
            </span>
            <span v-else>
              Sí
            </span>
          </td>
          <td>
            <span v-if="props.item[3] == 0">
              Estudiante
            </span>
            <span v-else>
              Trabaja
            </span>
          </td>
          <td>
            <span v-if="props.item[4] == 0">
              Mujer
            </span>
            <span v-else>
              Hombre
            </span>
          </td>
          <td>
            <span v-if="props.item[5] == 0">
              No
            </span>
            <span v-else>
              Sí
            </span>
          </td>
          <td>
            <span v-if="props.item[6] == 0">
              No
            </span>
            <span v-else>
              Sí
            </span>
          </td>
          <td>{{props.item[7]}}</td>
          <td>{{props.item[8]}}</td>
        </template>

        </v-data-table>
      </v-flex>

      <v-dialog
        v-model="dialog2"
        max-width="290"
      >
        <v-card>
          <v-card-title class="headline">Tu recomendación</v-card-title>
          <v-card-text>{{recomen}}</v-card-text>
          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn
              color="primary"
              dark
              @click="dialog2 = false"
            >
              Ok
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
    </v-layout>
  </v-container>
</template>

<script>
  export default {
    mounted() {
      this.Recomendacion()
    },
    data: () => ({
      valid: true,
      nombre: '',
      reglasNombre: [
        v => !!v || 'Tu nombre es requerido'
      ],
      vivienda: '',
      reglasVivienda: [
        v => !!v || 'Campo requerido'
      ],
      patio: '',
      reglasPatio: [
        v => !!v || 'Campo requerido'
      ],
      ocupacion: '',
      reglasOcupacion: [
        v => !!v || 'Campo requerido'
      ],
      genero: '',
      reglasGenero: [
        v => !!v || 'Campo requerido'
      ],
      activFisica: '',
      reglasActivFisica: [
        v => !!v || 'Campo requerido'
      ],
      compra: '',
      reglasCompra: [
        v => !!v || 'Campo requerido'
      ],
      headers1: [
        {sortable: false, text: 'Nombre', value: 'nombre'},
        {sortable: false, text: "Tipo de Vivienda", value: 'vivienda'},
        {sortable: false, text: "¿Tiene patio?", value: 'patio'},
        {sortable: false, text: "¿Estudia o trabaja?", value: 'ocupacion'},
        {sortable: false, text: "Género", value: 'genero'},
        {sortable: false, text: "¿Practica alguna actividad física?", value: 'activfisica'},
        {sortable: false, text: "¿Piensa que la compra de animales es una mala práctica?", value: 'compraanimales'},
        {sortable: false, text: "Mascota", value: 'mascota'}
      ],
      headers2: [
        {sortable: false, text: 'Nombre', value: 'nombre'},
        {sortable: false, text: "Tipo de Vivienda", value: 'vivienda'},
        {sortable: false, text: "¿Tiene patio?", value: 'patio'},
        {sortable: false, text: "¿Estudia o trabaja?", value: 'ocupacion'},
        {sortable: false, text: "Género", value: 'genero'},
        {sortable: false, text: "¿Practica alguna actividad física?", value: 'activfisica'},
        {sortable: false, text: "¿Piensa que la compra de animales es una mala práctica?", value: 'compraanimales'},
        {sortable: false, text: "Recomendación", value: 'recomendacion'},
        {sortable: false, text: "Correlación", value: 'correlacion'}
      ],
      x: [["Alfredo Lopez",1,"Perro",1,2,3,4,5,6],
        ["Ruben Rosales",1,"Perro",1,2,3,4,0,6],
        ["Gabriel Gamez",1,"Perro",1,2,3,4,0,0],
        ["Juliana Flores",1,"Perro",1,2,0,0,0,0],
        ["Ivan Aguilar",1,"Perro",1,2,0,4,0,0],
        ["Alejandro Lopez",1,"Perro",1,2,3,4,5,0],
        ["Erick Cabanillas",1,"Gato",1,2,0,4,0,0],
        ["Jessica Cueva",1,"Pez",1,2,0,0,0,1],
        ["Andres Silvaran",1,"Gato",1,2,0,4,5,0],
        ["Cristian Patino",1,"Tortuga",1,2,0,4,5,0],
        ["Fernando Martinez",1,"Conejo",1,2,0,4,5,0],
        ["Diana Hurtado",1,"Gato",1,2,3,0,4,5],
        ["Raul Martinez",1,"Gato",1,2,0,4,0,0],
        ["Angelica Diaz",1,"Pez",1,2,3,0,0,0],
        ["Juan Manuel",1,"Pez",1,2,0,4,5,0],
        ["Aldair Villegas",1,"Conejo",1,2,3,4,5,0],
        ["Aldair Villeg",1,"Pez",1,2,3,0,0,0],
        ["Moises Vaquera",1,"Gato",1,2,3,0,0,0],
        ["Coraima Ramos",1,"Pajaro",1,2,0,0,5,0],
        ["Jose Chaidez",1,"Pajaro",1,2,0,4,0,0],
        ["Claudio Beltran",1,"Pajaro",1,2,0,4,5,0],
        ["Ricardo Zamudio",1,"Gato",1,2,3,0,0,0],
        ["Javier Duarte",1,"Pajaro",0,0,3,4,5,6],
        ["Enrique",1,"Tortuga",0,0,3,0,5,0],
        ["Andres Manuel",1,"Pez",0,0,0,4,0,0],
        ["Ricardo Lopez",1,"Perro",1,0,0,4,5,0],
        ["Javier",1,"Gato",0,0,0,4,5,6],
        ["Monica Trujillo",1,"Serpiente",0,0,0,4,0,0],
        ["Frida Fajardo",1,"Serpiente",0,0,0,4,5,6],
        ["Susana Tequida",1,"Pez",1,2,0,4,0,6],
        ["Santa Monica",1,"Perro",0,0,0,4,5,6],
        ["Maritza Sanches",1,"Gato",1,2,0,4,5,6],
        ["Francisco Sauceda",1,"Perro",1,2,3,4,0,6],
        ["Francisco Hernandez",1,"Tortuga",1,2,3,4,0,0],
        ["Daniela Medina",1,"Pez",1,2,0,0,5,6],
        ["Gerardo Villalobos",1,"Tortuga",1,2,3,4,5,0],
        ["Wulfrano",1,"Perro",1,2,3,0,0,0],
        ["Pedro",1,"Serpiente",0,0,3,0,5,6],
        ["Georgina Becerra",1,"Pajaro",0,0,0,4,5,6],
        ["Hanxel Alexis",1,"Conejo",0,0,3,4,5,6],
        ["Dennise Alexis",1,"Conejo",1,2,0,0,5,6],
        ["Jessica Noemi",1,"Conejo",1,2,0,4,5,6],
        ["Alejandra Mercado",1,"Perro",1,2,0,4,0,6],
        ["Ofsset",1,"Serpiente",1,2,3,4,5,0],
        ["Quavo",1,"Serpiente",1,2,3,4,0,0],
        ["Monica Sanchez",1,"Conejo",1,2,0,4,5,6],
        ["Jaime Bernal",1,"Pajaro",1,2,3,4,5,0],
        ["Luis Miguel",1,"Tortuga",1,2,3,0,0,0],
        ["Luis Enrique",1,"Tortuga",1,2,3,4,0,0],
        ["Maria Sanchez",1,"Conejo",0,0,0,4,5,6]],
      y: [["Julio Villalobos",1,2,0,4,5,0],
        ["Janeth Villalobos",1,1,0,0,0,1],
        ["Ricardo Chavez",1,2,3,4,5,0],
        ["Daniel Medina",0,0,0,4,5,0],
        ["Erick Olalde",1,2,0,4,5,0],
        ["Alexis Medina",1,2,3,0,5,0],
        ["Santa Ana",0,0,0,4,0,6],
        ["Janeth Garcia",0,0,0,4,5,0],
        ["Vianey",1,0,0,4,5,6],
        ["Jorge",1,0,3,4,5,0],
        ["Sergio Mayer",1,2,3,0,5,6],
        ["Gonzalo Navarrete",1,2,3,4,5,6],
        ["Sacarias",1,2,3,4,0,6],
        ["Homero",1,2,3,4,0,0],
        ["Erick Medina",1,0,3,0,5,0],
        ["Claudia Zapata",1,0,0,0,5,6],
        ["Daniel Zaragoza",1,2,3,0,5,6],
        ["Vanessa Secilla",1,0,0,4,5,6],
        ["Jeovanny Heredia",1,2,3,0,5,0],
        ["Dianna Vanesa",1,2,0,4,5,6],
        ["Cosmito", 1, 0, 3, 0, 5, 0]],
      recomendaciones: [],
      dialog: false,
      dialog2: false,
      recomen: ''
    }),
    methods: {
      MeanX: function (z) {
        let suma = 0.0;
        let variable1 = 0;
        let variable2 = 3;
        while (variable1 < 6) {
          suma = suma + this.x[z][variable2];
          variable1++;
          variable2++;
        }
        return suma/6.0;
      },
      StandardDeviationX: function(z) {
        let sumav = 0.0;
        let variable1 = 0;
        let variable2 = 3;

        while (variable1 < 6) {
          sumav = sumav + ((this.x[z][variable2] - this.MeanX(z))**2);
          variable1++;
          variable2++;
        }
        return Math.sqrt(sumav/6.0);
      },
      MeanY: function (w) {
        let suma = 0.0;
        let variable1 = 0;
        let variable2 = 1;
        while (variable1 < 6) {
          suma = suma + this.y[w][variable2];
          variable1++;
          variable2++;
        }
        return suma/6.0;
      },
      StandardDeviationY: function(w) {
        let sumav = 0.0;
        let variable1 = 0;
        let variable2 = 1;

        while (variable1 < 6) {
          sumav = sumav + ((this.y[w][variable2] - this.MeanY(w))**2);
          variable1++;
          variable2++;
        }
        return Math.sqrt(sumav/6.0);
      },
      Pearson: function(z,w){
        let scoreX = [];
        let scoreY = [];

        let variable1 = 0;
        let variableX = 3;
        let variableY = 1;

        while (variable1 < 6) {
          scoreX.push((this.x[z][variableX] - this.MeanX(z)) / this.StandardDeviationX(z));
          scoreY.push((this.y[w][variableY] - this.MeanY(w)) / this.StandardDeviationY(w));
          variable1++;
          variableX++;
          variableY++;
        }

        let both = 0;
        let sumaboth = 0.0;
        let varboth = 0;

        while (both < 6) {
          sumaboth = sumaboth + (scoreX[varboth] * scoreY[varboth]) / 6.0;
          both++;
          varboth++;
        }
        return sumaboth;
      },
      Recomendacion: function(){
        this.recomendaciones = []
        let w = 0;
        while (w < this.y.length) {
          let z = 0;
          while (z < 50) {
            let corr = this.Pearson(z, w);
            if(corr > 0.9 && corr < 0.99){
              let recomendacion = this.y[w]
              recomendacion[7] = this.x[z][2]
              recomendacion[8] = corr
              this.recomendaciones.push(recomendacion);
              z = 51;
            }
            if(corr > 0.80 && corr < 0.90){
              let recomendacion = this.y[w]
              recomendacion[7] = this.x[z][2]
              recomendacion[8] = corr
              this.recomendaciones.push(recomendacion);
              z = 51;
            }
            else{
              z++;
            }
          }
          w++;
        }
      },
      submit(){
        if(this.$refs.form.validate()) {
          let recomendacion = []
          recomendacion[0] = this.nombre
          recomendacion[1] = parseInt(this.vivienda)
          recomendacion[2] = parseInt(this.patio)
          recomendacion[3] = parseInt(this.ocupacion)
          recomendacion[4] = parseInt(this.genero)
          recomendacion[5] = parseInt(this.activFisica)
          recomendacion[6] = parseInt(this.compra)
          this.y.push(recomendacion)

          this.Recomendacion()

          let ultima = this.recomendaciones[this.recomendaciones.length - 1]

          this.recomen = `${ultima[0]} te recomendamos: ${ultima[7]}`

          this.dialog = false

          this.dialog2 = true

          this.clear()
        }
      },
      clear() {
        this.$refs.form.reset()
      }
    }
  }
</script>

<style>

</style>
