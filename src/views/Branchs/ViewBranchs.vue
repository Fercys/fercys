<template>
  <section>
    <base-header class="pb-6">
      <div class="row align-items-center py-4">
        <div class="col-lg-6 col-7">
          <h6 class="h2 d-inline-block mb-0">{{$route.name}}</h6>
          <nav aria-label="breadcrumb" class="d-none d-md-inline-block ml-md-4">
            <route-breadcrumb />
          </nav>
        </div>
        <div class="col-lg-6 col-5 text-right">
          <base-button @click="$router.push(`/supplier/${$route.query.supplier}/branchs`)" size="sm" type="neutral" v-if="$route.query.supplier !== undefined">Back</base-button>
          <base-button @click="$router.push('/branchs')" size="sm" type="neutral" v-else>Back</base-button>
          <base-button size="sm" type="primary" @click="updateBranch($route.params.id)">Save Branch</base-button>
        </div>
      </div>
    </base-header>
    <div class="container-fluid mt--6">
      <div class="card mb-4">
        <div class="card-header">
<<<<<<< HEAD:src/views/Branchs/ViewBranchs.vue
          <h3 class="mb-0">View-Edit Branch: NameBranch of NombreSupplier</h3>
=======
          <h3 class="mb-0">Edit Branch</h3>
>>>>>>> dev-fercys:src/views/Branchs/EditBranchs.vue
        </div>
        <div class="card-body">
          <div class="row">
            <div class="col-md">
              <div class="row">
                <div class="col-md-4">
                  <base-input v-model.trim="branch.name" label="Name:" placeholder="name" />
                </div>
                <div class="col-md-4">
                  <base-input v-model.trim="branch.email" label="Email:" placeholder="Email" />
                </div>
                <div class="col-md-4">
                    <label class="form-control-label">Supplier:</label>
                  <br />
                  <el-select
                    class="select-danger"
                    placeholder="Select Supplier"
                    v-model="branch.supplier"
                    style="width:100%"
                  >
                    <el-option
                      v-for="supplier in supplierSelections"
                      class="select-danger"
                      :value="supplier._id"
                      :label="supplier.name"
                      :key="supplier._id"
                    ></el-option>
                  </el-select>
                  
                </div>
              </div>
              <div class="row">
                <div class="col-md-4">
                  <base-input
                    v-model.trim="branch.first_name"
                    label="First Name:"
                    placeholder="First Name"
                  />
                </div>
                <div class="col-md-4">
                  <base-input
                    v-model.trim="branch.last_name"
                    label="Last Name:"
                    placeholder="Last Name"
                  />
                </div>
                <div class="col-md-4">
                  <base-input v-model.trim="branch.phone" label="Phone:" placeholder="Phone" />
                </div>
              </div>
              <div class="row">
                <div class="col-md-4">
                  <base-input v-model.trim="branch.country" label="Country:" placeholder="Argentina" />
                </div>
                <div class="col-md-4">
                  <base-input v-model.trim="branch.city" label="City:" placeholder="Rosario" />
                </div>
                <div class="col-md-4">
                   <label class="form-control-label">Hours advance booking:</label>
                  <br />
                  <el-select
                    class="select-danger"
                    placeholder="Select country"
                    v-model="branch.hours_advance_booking"
                    style="width:100%"
                  >
                    <el-option
                      v-for="option in selects_hours"
                      class="select-danger"
                      :value="option"
                      :label="option"
                      :key="option"
                    ></el-option>
                  </el-select>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
// @ is an alias to /src
import { mapGetters, mapActions, mapMutations } from "vuex";
import service from "../../commons/services/branchs";
export default {
  name: "EditBranchs",
  data() {
    return {
      branch: {
        name: "",
        country: "",
        email: "",
        last_name: "",
        first_name: "",
        phone: "",
        city: "",
        hours_advance_booking: "",
        supplier: ""
      },
      selects_hours: [2, 4, 6, 8, 10]
    };
  },
  created() {
     this.getBranch(this.$route.params.id)
  },
  methods: {
    getBranch(_id){
      service.branchs.getBranch(_id).then((response)=>{
        if (response.data.data !== null) {
          let data = response.data.data
          this.branch.name = data.name
          this.branch.country = data.country
          this.branch.email = data.email
          this.branch.first_name = data.first_name
          this.branch.last_name = data.last_name
          this.branch.phone = data.phone
          this.branch.city = data.city
          this.branch.hours_advance_booking = data.hours_advance_booking
          this.branch.supplier = data.supplier._id
        } else {
          
        }
      })
    },
    updateBranch(_id){
      let body = this.branch
      console.log(body)
      service.branchs.updateBranch(_id, body).then((response)=>{
        console.log(response.data)
        if (response.data.code) {
          if (this.$route.query.supplier) {
            this.$router.push(`/supplier/${this.$route.query.supplier}/branchs`) 
          } else {
            this.$router.push('/branchs') 
          }
        } else {
          
        }
      })
    },
    ...mapMutations(["setActiveItem"])
  },
  computed:{
    ...mapGetters(['supplierSelections'])
  },
  components: {}
};
</script>
<style lang="scss">
</style>