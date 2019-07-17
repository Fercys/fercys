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
          <base-button @click="$router.push(`/company/${$route.query.company}/suppliers`)" size="sm" type="neutral" v-if="$route.query.company !== undefined">Back</base-button>
          <base-button @click="$router.push('/suppliers')" size="sm" type="neutral" v-else>Back</base-button>
          <base-button size="sm" type="primary" @click="editSupplier($route.params.id)">Save Supplier</base-button>
        </div>
      </div>
    </base-header>
    <div class="container-fluid mt--6">
      <div class="card mb-4">
        <div class="card-header">
          <h3 class="mb-0">Edit Supplier</h3>
        </div>
        <div class="card-body">
          <div class="row">
            <div class="col-md">
              <div class="row">
                <div class="col-md-4">
                  <base-input
                    v-model.trim="supplier.name"
                    label="Name:"
                    placeholder="Europe Shuttle"
                  />
                </div>
                <div class="col-md-4">
                  <base-input
                    v-model.trim="supplier.email"
                    label="Email:"
                    placeholder="example@europeshuttle.com"
                  />
                </div>
                <div class="col-md-4">
                  <base-input
                    v-model.trim="supplier.address"
                    label="Address:"
                    placeholder="Venezuela, bolivar, bolivar, heres, 8000"
                  />
                </div>
              </div>
              <div class="row">
                <div class="col-md-4">
                  <base-input
                    v-model.trim="supplier.phone"
                    label="Phone:"
                    placeholder="58426159858"
                  />
                </div>
                <div class="col-md-4">
                  <base-input
                    v-model.trim="supplier.optional_phone"
                    label="Optional Phone:"
                    placeholder="58426159858"
                  />
                </div>
                <div class="col-md-4">
                  <label class="form-control-label">Company</label> <br>
                    <el-select class="select-danger" v-model="supplier.company" placeholder="Company" label="pepe" style="width:100%">
                        <el-option v-for="company in companySelections"
                        class="select-danger"
                        :value="company._id"
                        :label="company.name"
                        :key="company._id">
                        </el-option>
                    </el-select>
                </div>
              </div>
              <div class="row">
                <div class="col-md-4 mb-2">
                  <h3>Admin Account:</h3>
                </div>
              </div>
              <div class="row">
                <div class="col-md-4">
                  <base-input
                    v-model.trim="supplier.account_username"
                    label="User Name"
                    placeholder="supplier123"
                  />
                </div>
                <div class="col-md-4">
                  <base-input
                    v-model.trim="supplier.account_first_name"
                    label="First Name"
                    placeholder="John"
                  />
                </div>
                <div class="col-md-4">
                  <base-input
                    v-model.trim="supplier.account_last_name"
                    label="Last Name"
                    placeholder="Doe"
                  />
                </div>
              </div>
              <div class="row">
                <div class="col-md-4">
                  <base-input
                    v-model.trim="supplier.account_email"
                    label="Email:"
                    placeholder="Email"
                    disabled
                  />
                </div>
                <div class="col-md-4">
                  <base-input
                    v-model.trim="supplier.account_password"
                    type="password"
                    label="Password:"
                    placeholder="Password"
                  />
                </div>
                <div class="col-md-4">
                  <base-input
                    v-model.trim=" password_comfirm"
                    type="password"
                    label="Password Comfirm:"
                    placeholder="Password Comfirm"
                  />
                </div>
              </div>
              <div class="row">
                <div class="col-md-4">
                  <base-input
                    v-model.trim="supplier.account_phone"
                    label="Phone:"
                    placeholder="584975895123"
                  />
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
// @ is an alias to /src
import services from "../../commons/services/suppliers";
import { mapGetters, mapActions, mapMutations } from "vuex";
export default {
  name: "EditSupplier",
  data() {
    return {
      supplier: {
        address: "",
        name: "",
        phone: "",
        optional_phone: "",
        email: "",
        company: "",
        account_username: "",
        account_first_name: "",
        account_last_name: "",
        account_email: "",
        account_phone: ""
      },
      password: "",
      password_comfirm: ""
    };
  },
  created() {
    this.getSupplier(this.$route.params.id);
  },
  methods: {
    getSupplier(_id) {
      services.suppliers.getOneSupplier(_id).then(response => {
        if (response.data.code === 200) {
          let data = response.data.data;
          this.supplier.name = data.name;
          this.supplier.email = data.email;
          this.supplier.address = data.address;
          this.supplier.phone = data.phone;
          this.supplier.company = data.company;
          this.supplier.optional_phone = data.optional_phone;

          this.supplier.account_username = data.account_username;
          this.supplier.account_first_name = data.account_first_name;
          this.supplier.account_last_name = data.account_last_name;
          this.supplier.account_email = data.account_email;
          this.supplier.account_phone = data.account_phone;
        }
      });
    },
    editSupplier(_id) {
      let body = this.supplier;
      if (this.password !== "") {
        body["account_password"] = this.password;
      }
      services.suppliers
        .updateSupplier(_id, body)
        .then(response => {
          if (response.data.data !== null) {
            if (this.$route.query.company) {
              this.$router.push(`/company/${this.$route.query.company}/suppliers`)
            } else {
              this.$router.push('/suppliers');
            }
          } else {
          }
        })
        .catch(err => {});
    }
  },
  computed:{
    ...mapGetters(['companySelections'])
  }
};
</script>
<style lang="scss">
</style>