<template>
  <div class="card shadow mt-3">
    <div class="card-body">
      <h5 class="card-title">Add pegawai</h5>
      <form class="row g-3" @submit.prevent="store">
        <div class="col-md-6">
          <label for="inputEmail4" class="form-label">Nama</label>
          <input
            type="text"
            class="form-control"
            id="inputEmail4"
            v-model="pegawai.nama"
          />
          <div class="alert alert-warning" v-if="validation.nama">
            {{ validation.nama[0] }}
          </div>
        </div>
        <div class="col-md-6">
          <label for="inputPassword4" class="form-label">No Telepon</label>
          <input
            type="number"
            class="form-control"
            id="inputPassword4"
            v-model="pegawai.telp"
          />
          <div class="alert alert-warning" v-if="validation.telp">
            {{ validation.telp[0] }}
          </div>
        </div>
        <div class="col-6">
          <label for="inputAddress" class="form-label">nik</label>
          <input
            type="text"
            class="form-control"
            id="inputAddress"
            placeholder="Masukan nik"
            v-model="pegawai.nik"
          />
          <div class="alert alert-warning" v-if="validation.nik">
            {{ validation.nik[0] }}
          </div>
        </div>

        <div class="col-6">
          <label for="inputAddress" class="form-label">Shift</label>
        <select class="form-select" aria-label="Default select example" v-model="pegawai.shift_id">
          
          <option v-for="shift in shifts" :key="shift.id" :value="shift.id">{{ shift.name}}</option>

        </select>
        </div>

        <div class="col-12">
          <button type="submit" class="btn btn-light">Submit</button>
        </div>
      </form>
    </div>
  </div>
</template>
<script>
import { reactive, ref, onMounted } from "vue";
import { useRouter } from "vue-router";
import axios from "axios";
export default {
  setup() {
    const pegawai = reactive({
      nama: "",
      telp: "",
      nik: "",
      shift_id: ""
    });

    let shifts = ref([]);
    
    const validation = ref([]);

    const router = useRouter();


    onMounted(() =>{
      axios
        .get("http://127.0.0.1:8000/api/shifts")
        .then((response) => {
          shifts.value = response.data.data;
          console.log(response);
        })
        .catch((error) => {
          console.log(error);
        });
    });

    function store() {
      let nama = pegawai.nama;
      let telp = pegawai.telp;
      let nik = pegawai.nik;
      let shift_id = pegawai.shift_id;

      axios
        .post("http://127.0.0.1:8000/api/pegawais/", {
          nama: nama,
          telp: telp,
          nik: nik,
          shift_id: shift_id
        })
        .then(() => {
          router.push({
            name: "Home",
          });
        })
        .catch((error) => {
          validation.value = error.response.data;
        });
    }
    return {
      pegawai,
      store,
      validation,
      router,
      shifts,
    };
  },
};
</script>