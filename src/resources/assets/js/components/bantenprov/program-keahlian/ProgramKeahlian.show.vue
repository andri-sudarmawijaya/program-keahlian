<template>
  <div class="card">
    <div class="card-header">
      <i class="fa fa-table" aria-hidden="true"></i> Program keahlian {{ model.label }}

      <ul class="nav nav-pills card-header-pills pull-right">
        <li class="nav-item">
          <button class="btn btn-primary btn-sm" role="button" @click="back">
            <i class="fa fa-arrow-left" aria-hidden="true"></i>
          </button>
        </li>
      </ul>
    </div>

    <div class="card-body">
      <vue-form class="form-horizontal form-validation" :state="state" @submit.prevent="onSubmit">
        <div class="form-row">
          <div class="col-md">
            <b>Label :</b> {{ model.label }}
          </div>
        </div>


        <div class="form-row mt-4">
          <div class="col-md">
            <b>Keterangan :</b> {{ model.keterangan }}
          </div>
        </div>

        <div class="form-row mt-4">
        </div>
      </vue-form>
    </div>
    <div class="card-footer text-muted">
        <div class="row">
          <div class="col-md">
            <b>Username :</b> {{ model.user.name }}
          </div>
          <div class="col-md">
            <div class="col-md text-right">Dibuat : {{ model.created_at }}</div>
            <div class="col-md text-right">Diperbaiki : {{ model.updated_at }}</div>
          </div>
        </div>
      </div>
  </div>
</template>

<script>
export default {
  mounted() {
    axios.get('api/program-keahlian/' + this.$route.params.id)
      .then(response => {
        if (response.data.status == true) {
          this.model.label          = response.data.program_keahlian.label;
          this.model.user           = response.data.program_keahlian.user;
          this.model.keterangan     = response.data.program_keahlian.keterangan;
          this.model.created_at     = response.data.program_keahlian.created_at;
          this.model.updated_at     = response.data.program_keahlian.updated_at;

        }
        else {
          alert('Failed');
        }
      })
      .catch(function(response) {
        alert('Break');
        window.location.href = '#/admin/program-keahlian';
      })

  },
  data() {
    return {
      state: {},
      model: {
        user:          "",
        keterangan:       "",
        label:            "",
        created_at:       "",
        updated_at:       "",

      },
      user: []
    }
  },
  methods: {
    back() {
      window.location = '#/admin/program-keahlian';
    }
  }
}
</script>
