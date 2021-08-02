<template>
  <div class="home">

    <hr class="my-3" />
    <router-link class="btn btn-warning" to="/createpegawais"
      >Tambah Pegawai</router-link
    >


  <Main :pegawais="pegawais"/>
    
    <table class="table table-success table-stripe">
      <thead>
        <tr>
          <th scope="col">Nama</th>
          <th scope="col">No Telp</th>
          <th scope="col">NIK</th>
        </tr>
      </thead>

      <tbody>
        <tr v-for="(pegawais, index) in pegawais" :key="index">
          <td>{{ pegawais.nama }}</td>
          <td>{{ pegawais.telp }}</td>
          <td>{{ pegawais.nik }}</td>
          <td>
            <router-link class="btn btn-light" :to="{name:'Editpegawais', params:{id:pegawais.id}}"
              >Edit</router-link
            >
            <button @click.prevent="pegawaiDelete(pegawai.id)" class="btn btn-secondary">Delete</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from "axios";
// @ is an alias to /src
import Main from "@/components/Main.vue";
import { onMounted, ref } from "vue";

export default {
  name: "Home",
  components: {
    Main,
  },

  setup() {
    let pegawais = ref([])

    onMounted(() => {
      axios
        .get('http://127.0.0.1:8000/api/pegawais')
        .then(response => {
          pegawais.value = response.data.data
        })
        .catch(error => {
          console.log(error)
        })
    })

    function pegawaiDelete(id){
      axios.delete(`http://127.0.0.1:8000/api/pegawais/${id}`)
      .then(()=>{
        let z = this.pegawai.map(pegawais => pegawais.id).indexOf(id);
        this.pegawais.splice(z, 1)
      }).catch(error => {
        console.log(error)
      })
    }

    return {
      pegawais,
      pegawaiDelete
    }
  }
};
</script>
