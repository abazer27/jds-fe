<template>
  <div class="container">
    <form
      @submit.prevent="dataBantuan"
      class="w-full max-w-max overflow-hidden text-center bg-gray-200"
    >
      <div class="flex flex-wrap px-3 mb-6">
        <div class="full">
          <label class="label" for="nama"> Nama </label>
          <input
            class="box-form"
            type="text"
            v-model="data.nama"
            placeholder="Required"
            required
          />
        </div>
      </div>
      <div class="flex flex-wrap px-3 mb-6">
        <div class="full">
          <label class="label" for="nik">NIK</label>
          <input
            class="box-form"
            type="number"
            v-model="data.nik"
            placeholder="Required"
            required
          />
        </div>
      </div>
      <div class="flex flex-wrap px-3 mb-6">
        <div class="full">
          <label class="label" for="kk">Nomor Kartu Keluarga</label>
          <input
            class="box-form"
            type="number"
            v-model="data.kk"
            placeholder="Required"
            required
          />
        </div>
      </div>
      <div class="flex flex-wrap px-3 mb-6">
        <label class="label mr-5" for="ktp">Foto KTP</label>
        <input
          type="file"
          ref="ktp"
          @change="previewKtp"
          accept="image/png, image/jpg, image/jpeg, image/bmp"
          required
        />
      </div>
      <div class="flex flex-wrap px-3 mb-6">
        <label class="label mr-5" for="fkk">Foto Kartu Keluarga</label>
        <input
          type="file"
          ref="fkk"
          @change="previewFkk"
          placeholder="Required"
          accept="image/png, image/jpg, image/jpeg, image/bmp"
          required
        />
      </div>
      <div class="flex flex-wrap px-3 mb-6">
        <label class="label" for="umur">Umur</label>
        <input
          class="box-form"
          type="number"
          min="25"
          v-model="data.umur"
          placeholder="Required"
          required
        />
      </div>
      <div class="flex flex-wrap px-3 mb-6">
        <p class="label">Jenis Kelamin</p>
        <div class="flex flex-wrap mb-2">
          <div class="half px-3">
            <label class="label" for="jk">Laki - laki</label>
            <input
              type="radio"
              name="jk"
              value="Laki-laki"
              v-model="data.jk"
              required
            />
          </div>
          <div class="half px-3">
            <label class="label" for="jk">Perempuan</label>
            <input type="radio" name="jk" value="Perempuan" v-model="data.jk" />
          </div>
        </div>
      </div>
      <div class="flex flex-wrap px-3 mb-6">
        <label class="label" for="provinsi">Provinsi</label>
        <select
          class="box-form"
          v-model="data.provinsi"
          @change="onChangeProv"
          required
        >
          <option
            v-for="list in provinsiData"
            :key="list.id"
            :id="list.id"
            :value="list.name"
          >
            {{ list.name }}
          </option>
        </select>
      </div>
      <div class="flex flex-wrap px-3 mb-6">
        <label class="label" for="kab">Kab/Kota</label>
        <select
          class="box-form"
          v-model="data.kab"
          @change="onChangeKab"
          required
        >
          <option
            v-for="list in kabData"
            :key="list.id"
            :id="list.id"
            :value="list.name"
          >
            {{ list.name }}
          </option>
        </select>
      </div>
      <div class="flex flex-wrap px-3 mb-6">
        <label class="label" for="kec">Kecamatan</label>
        <select
          class="box-form"
          v-model="data.kec"
          @change="onChangeKec"
          required
        >
          <option
            v-for="list in kecData"
            :key="list.id"
            :id="list.id"
            :value="list.name"
          >
            {{ list.name }}
          </option>
        </select>
      </div>
      <div class="flex flex-wrap px-3 mb-6">
        <label class="label" for="kel">Kelurahan</label>
        <select class="box-form" v-model="data.kel" required>
          <option v-for="list in kelData" :key="list.id" :value="list.name">
            {{ list.name }}
          </option>
        </select>
      </div>
      <div class="flex flex-wrap px-3 mb-6">
        <label class="label" for="">Alamat</label>
        <textarea
          name=""
          id=""
          class="box-form"
          maxlength="255"
          placeholder="Required"
          v-model="data.alamat"
          required
        ></textarea>
      </div>
      <div class="flex justify-between mb-2 mx-3">
        <div class="half">
          <label class="label" for="RT">RT</label>
          <input
            class="
              w-24
              bg-gray-100
              text-gray-700
              border border-gray-200
              rounded
              text-sm
              py-3
              px-4
              mb-3
            "
            v-model="data.rt"
            type="text"
            placeholder="Required"
            required
          />
        </div>
        <div class="half">
          <label class="label" for="RW">RW</label>
          <input
            class="
              w-24
              bg-gray-100
              text-gray-700
              border border-gray-200
              rounded
              text-sm
              py-3
              px-4
              mb-3
            "
            v-model="data.rw"
            type="text"
            placeholder="Required"
            required
          />
        </div>
      </div>
      <div class="flex flex-wrap px-3 mb-6">
        <label class="label" for="">Penghasilan Sebelum</label>
        <input
          class="box-form"
          type="number"
          placeholder="Required"
          v-model="data.salaryBefore"
          required
        />
      </div>
      <div class="flex flex-wrap px-3 mb-6">
        <label class="label" for="">Penghasilan Setelah Pandemi</label>
        <input
          class="box-form"
          type="number"
          placeholder="Required"
          v-model="data.salaryAfter"
          required
        />
      </div>
      <div class="flex flex-wrap px-3 mb-6 text-xs">
        <label class="label" for="">Alasan membutuhkan bantuan</label>
        <select class="box-form" v-model="data.reason" required>
          <option v-for="data in reasonData" :key="data" :value="data">
            {{ data }}
          </option>
        </select>
        <input
          type="text"
          class="box-form"
          v-if="data.reason === other"
          v-model="data.reasons"
          required
        />
      </div>
      <div class="flex flex-wrap px-3 mb-6">
        <input type="checkbox" id="checkbox" v-model="data.ttd" required />
        <label class="label" for="checkbox"
          >Saya menyatakan bahwa data yang diisikan adalah benar dan siap
          mempertanggungjawabkan apabila ditemukan ketidaksesuaian dalam data
          tersebut.</label
        >
      </div>
      <button type="sumbit" @click="openModal" class=" border-2 bg-white rounded p-3 mb-3">Submit</button>
    </form>
    <div v-if="modalData">
      <h1>Hallo</h1>
      <transition name="modal">
        <div class="modal-mask">
          <div class="overflow-auto">
            <div class="modal-header">
              <button
                @click="modalData = false"
                class="
                  right-0
                  top-0
                  absolute
                  border-2
                  rounded
                  px-2
                  py-2
                  m-1
                  bg-black
                "
              >
                Close
              </button>
              <h3 class="text-xl text-center">Data Bantuan</h3>
            </div>
            <div class="modal-body flex flex-row">
              <div class="flex flex-col half">
                <div>
                  <label class="white text-xs" for="nama">Nama</label>
                  <h4>{{ this.data.nama }}</h4>
                </div>
                <div>
                  <label class="white text-xs" for="nama">NIK</label>
                  <h4>{{ this.data.nik }}</h4>
                </div>
                <div>
                  <label class="white text-xs" for="nama">Nomor KK</label>
                  <h4>{{ this.data.kk }}</h4>
                </div>
                <div>
                  <label class="white text-xs" for="nama">Foto KTP</label>
                  <h4>img file</h4>
                </div>
                <div>
                  <label class="white text-xs" for="nama">Foto KK</label>
                  <h4>img file</h4>
                </div>
                <div>
                  <label class="white text-xs" for="nama">Umur</label>
                  <h4>{{ this.data.umur }}</h4>
                  <label class="white text-xs" for="nama">Jenis Kelamin</label>
                  <h4>{{ this.data.jk }}</h4>
                </div>
                <div>
                  <label class="white text-xs" for="nama">Provinsi</label>
                  <h4>{{ this.data.provinsi }}</h4>
                </div>
                <div>
                  <label class="white text-xs" for="nama">Kabupaten / Kota</label>
                  <h4>{{ this.data.kab }}</h4>
                </div>
                <div>
                  <label class="white text-xs" for="nama">Kecamatan</label>
                  <h4>{{ this.data.kec }}</h4>
                </div>
                <div>
                  <label class="white text-xs" for="nama">Kelurahan</label>
                  <h4>{{ this.data.kel }}</h4>
                </div>
                <div>
                  <label class="white text-xs" for="nama">Alamat</label>
                  <h4>{{ this.data.alamat }}</h4>
                </div>
              </div>
              <div class="flex flex-col half">
                <div>
                  <label class="white text-xs" for="nama">RT</label>
                  <h4>{{ this.data.rt }}</h4>
                  <label class="white text-xs" for="nama">RW</label>
                  <h4>{{ this.data.rw }}</h4>
                </div>
                <div>
                  <label class="white text-xs" for="nama"
                    >Penghasilan Sebelum Covid-19</label
                  >
                  <h4>{{ this.data.salaryBefore }}</h4>
                  <label class="white text-xs" for="nama"
                    >Penghasilan Setelah Covid-19</label
                  >
                  <h4>{{ this.data.salaryAfter }}</h4>
                </div>
                <div>
                  <label class="white text-xs" for="nama"
                    >Alasan membutuhkan bantuan</label
                  >
                  <h4>{{ this.data.reason }}. {{ this.data.reasons }}</h4>
                </div>
              </div>
            </div>
          </div>
        </div>
      </transition>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "formdata",
  data() {
    return {
      data: {
        nama: "",
        nik: null,
        kk: null,
        ktp: "",
        fkk: "",
        umur: null,
        jk: "",
        provinsi: "",
        kab: "",
        kec: "",
        kel: "",
        alamat: "",
        rt: null,
        rw: null,
        salaryBefore: null,
        salaryAfter: null,
        reason: "",
        reasons: "",
        ttd: "",
      },
      provinsiData: [],
      province_id: "",
      kabData: [],
      regency_id: "",
      kecData: [],
      district_id: "",
      kelData: [],
      villages: null,
      other: "Lainnya",
      reasonData: [
        "Kehilangan pekerjaan",
        "Kepala keluarga terdampak atau korban Covid-19",
        "Tergolong fakir/miskin semenjak sebelum Covid-19",
        "Lainnya",
      ],
      modalData: false,
    };
  },
  mounted() {
    axios
      .get(`https://www.emsifa.com/api-wilayah-indonesia/api/provinces.json`)
      .then((response) => (this.provinsiData = response.data));
  },
  methods: {
    previewKtp(e) {
      if (e.target.files[0].size > 2000000) {
        alert("FILE IS TO BIG (Max 2mb)");
        this.value = null;
      } else {
        const ktp = e.target.files[0];
        console.log(ktp);
        const reader = new FileReader();
        reader.readAsDataURL(ktp);
        reader.onloadend = (e) => {
          this.previewKtp = e.target.result;
          console.log(this.previewKtp);
        };
      }
    },
    previewFkk(e) {
      if (e.target.files[0].size > 2000000) {
        alert("FILE IS TO BIG (Max 2mb)");
        this.value = null;
      } else {
        const fkk = e.target.files[0];
        const reader = new FileReader();
        reader.readAsDataURL(fkk);
        reader.onload = (e) => {
          this.previewFkk = e.target.result;
          console.log(this.previewFkk);
        };
      }
    },
    onChangeProv: function (e) {
      const id = e.target.options[e.target.options.selectedIndex].id;
      this.province_id = id;
      axios
        .get(
          `https://www.emsifa.com/api-wilayah-indonesia/api/regencies/${this.province_id}.json`
        )
        .then((response) => (this.kabData = response.data));
    },
    onChangeKab: function (e) {
      const id = e.target.options[e.target.options.selectedIndex].id;
      this.regency_id = id;
      axios
        .get(
          `https://www.emsifa.com/api-wilayah-indonesia/api/districts/${this.regency_id}.json`
        )
        .then((response) => (this.kecData = response.data));
    },
    onChangeKec: function (e) {
      const id = e.target.options[e.target.options.selectedIndex].id;
      this.district_id = id;
      axios
        .get(
          `https://www.emsifa.com/api-wilayah-indonesia/api/villages/${this.district_id}.json`
        )
        .then((response) => (this.kelData = response.data));
    },
    openModal() {
      if (this.data.ttd != null) {
        this.modalData = true;
      }
    },
  },
};
</script>

<style lang="postcss">
.full {
  @apply w-full;
}
.half {
  @apply w-1/2;
}
.label {
  @apply block uppercase tracking-wide text-gray-700 text-base font-bold mb-2;
}
.box-form {
  @apply appearance-none block w-full bg-gray-100 text-gray-700 border border-gray-200 rounded py-3 px-4 mb-3 leading-tight focus:outline-none focus:bg-white focus:border-gray-500;
}
.modal-mask {
  position: fixed;
  z-index: 9999;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.849);
  display: table;
  transition: opacity 0.3s ease;
  color: whitesmoke;
}

.modal-wrapper {
  display: table-cell;
  vertical-align: middle;
}
</style>