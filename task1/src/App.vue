<template>
  <div class="row" id="app">
    <div class="workers col-2" v-if="workersList!==null" v-for="(worker) in workersList.data">
      <img :src="worker.avatar" data-toggle="modal" :data-target="'#'+worker.id" v-on:click="openModal(worker.id)"/>
     
      <!-- Modal -->
<div class="modal fade" :id="worker.id" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
  <div class="modal-dialog" role="document">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title" id="exampleModalLabel">Worker</h5>
        <button type="button" class="close" data-dismiss="modal" aria-label="Close">
          <span aria-hidden="true">&times;</span>
        </button>
      </div>
      <div class="modal-body">
        <h3>{{worker.first_name}}</h3>
        <h3>{{worker.last_name}}</h3>
        <h3>{{worker.email}}</h3>
        
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
      </div>
    </div>
  </div>
</div>
    </div>
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";

export default {
  name: "app",
  components: {
    HelloWorld
  },
  data() {
    return {
      workersList: null,
      workersUrl: "https://reqres.in/api/users"
    };
  },
  mounted() {
    this.loadData(this.workersUrl);
  },
  methods: {
    loadData(url) {
      this.axios.get(url).then(response => {
        this.workersList = response.data;
      });
    },
    openModal(index){
      $('#'+index).modal('toggle');
    }
  }
};
</script>

<style>
</style>
