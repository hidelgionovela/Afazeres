<template>
  <q-page class=" bg-grey-3 column">
    <!-- <div class="row q-pa-sm bg-primary"> Criar um afazer </div> -->
    <q-list 
    class="bg-white" bordered
    separator borderd>
     
      <q-item
      v-for="(task, index) in tasks" 
      :key="task.title"
      @click="task.done = !task.done"
      :class="{'done bg-yellow-2' : task.done}"
      clickable
      v-ripple>
        <q-item-section avatar>
          <q-checkbox
           v-model="task.done"
           class="no-pointer-events" 
            color="primary" />
        </q-item-section>
        <q-item-section>
          <q-item-label>{{ task.title }}</q-item-label>
        </q-item-section>
          
        <q-item-section 
          v-if ="task.done"
          side>
          <q-btn @click.stop="deleteTask(index)" flat round dense color="primary" icon="delete" />
        </q-item-section>
      </q-item>

    </q-list>
  </q-page>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  name: "IndexPage",

    data(){
    return{
      tasks:[
        {
          title: 'Estuadar PHP',
          done: true
        },
        {
          title: 'Estuadar Fisica',
          done: false
        },
        {
          title: 'Estudar Matematica',
          done: false
        },
        
      ]
    }
    
  },
  methods : { 
      deleteTask(index) {
      this.$q.dialog({
        title: 'Confirm',
        message: 'Realmente Deseja apagar!',
        cancel: true,
        persistent: true
      }).onOk(() => {
        this.tasks.splice(index, 1)
        this.$q.notify('Afazer apagado')
      })

      }
    }
});


</script>

<style lang="scss">
.done{
  .q-intem__label{
    text-decoration: line-through;
    color: brown;
  }
}

</style>
