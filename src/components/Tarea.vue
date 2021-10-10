<template>
  <div class="container mt-5">
      <div class="row">
          <div class="column is-8 is-offset-2">
              <input type="text" class="input is-success is-medium" placeholder="Ingresar Tarea" v-model="nombreTarea" v-on:keyup.enter="agregarTarea()">
              <br>
          </div>
          <div class="column is-6 is-offset-3">
              <div class="card p-2" v-if="tareas.length === 0">
                  <h6>No hay tareas para mostrar</h6>
              </div>
              <ul class="card p-2" v-for="(tarea, index) in tareas" v-bind:key="index">
                <li class="is-flex is-justify-content-space-between">
                    <span v-bind:class="[tarea.estado=== true ? 'icon has-text-success': '', 'cursor']" v-on:click="actualizarTarea(tarea, index)">
                        <i v-bind:class="[tarea.estado===true ? 'fas fa-check-circle': 'far fa-circle']"></i>
                        <!-- <i class="far fa-circle"></i>
                        <i class="fas fa-check-circle"></i> -->
                    </span>
                    <h5>{{tarea.nombre}}</h5> 
                    <span class="cursor icon has-text-danger" v-on:click="eliminarTarea(index)">
                        <i class="fas fa-trash-alt"></i>
                    </span>   
                </li>
              </ul>
          </div>
      </div>
  </div>
</template>

<script>
export default {
    data(){
        return{
            tareas: [],
            nombreTarea: ''
        }
    },
    methods:{
        agregarTarea(){

            const tarea= {
                nombre: this.nombreTarea,
                estado: false
            }
            this.tareas.push(tarea);
            this.nombreTarea='';
            console.log(tarea)
        },
        eliminarTarea(index){
            this.tareas.splice(index, 1);
        },
        actualizarTarea(tarea, index){
            this.tareas[index].estado = !tarea.estado;
        }
    }
}
</script>

<style scoped>
    input{
        text-align: center;
    }

    .is-medium{
        font-size: 20px;
    }

    .cursor{
        cursor: pointer;
    }
</style>