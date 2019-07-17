<template>
<section>
  <base-header class="pb-6">
      <div class="row align-items-center py-4">
        <div class="col-lg-6 col-7">
          <h6 class="h2 d-inline-block mb-0">{{$route.name}}</h6>
          <nav aria-label="breadcrumb" class="d-none d-md-inline-block ml-md-4">
            <route-breadcrumb/>
          </nav>
        </div>
        <div class="col-lg-6 col-5 text-right">
          <base-button @click="$router.push('/companies')" size="sm" type="neutral">Back</base-button>
          <base-button @click="editCompany($route.params.id)" size="sm" type="primary">Save Company</base-button>
        </div>
      </div>
    </base-header>
    <div class="container-fluid mt--6">
      <div class="card mb-4">
        <div class="card-header">
          <h3 class="mb-0">Edit Company</h3>
        </div>
        <div class="card-body">
          <div class="row">
            <div class="col-md">
                <div class="row">
                  <div class="col-md-4">
                    <base-input v-model.trim="company.name" label="Company Name:" placeholder="Europe Shuttle"/>
                  </div>
                  <div class="col-md-4">
                     <base-input v-model.trim="company.email"  label="Email:" placeholder="example@europeshuttle.com"/>
                  </div>
                  <div class="col-md-4">
                    <base-input v-model.trim="company.vat_number"  label="VAT Number:" placeholder="VAT Number"/>
                  </div>
                </div>
                <div class="row">
                  <div class="col-md-4">
                    <base-input v-model.trim="company.phone"  label="Phone:" placeholder="58424597852"/>
                  </div>
                  <div class="col-md-4">
                    <base-input v-model.trim="company.address"   label="Address" placeholder="Venezuela, bolivar, bolivar, heres, 8000"/>
                  </div>
                </div>  
                <div class="row">
                  <div class="col-md-4 mb-3">
                      <h3>Admin Account: </h3>
                  </div>
                </div>
                <div class="row">
                  <div class="col-md-4">
                     <base-input v-model.trim="company.account_username" label="Username:" placeholder="supplier123"/>
                  </div>
                  <div class="col-md-4">
                    <base-input v-model.trim="company.account_first_name" label="First Name:" placeholder="John"/>
                  </div>
                  <div class="col-md-4">
                    <base-input v-model.trim="company.account_last_name" label="Last Name:" placeholder="Doe"/>
                  </div>
                </div> 
                <div class="row">
                  <div class="col-md-4">
                    <base-input v-model.trim="company.account_email" label="Email:" placeholder="example@europeshuttle.com" disabled/>
                  </div>
                  <div class="col-md-4">
                     <base-input v-model.trim="password" label="Password:" placeholder="Password" type="password"/>
                  </div>
                  <div class="col-md-4">
                    <base-input v-model.trim="company.repeatPassword" label="Confirm Password:" placeholder="Confirm Password" type="password"/>
                  </div>
                  
                </div>
                <div class="row">
                  <div class="col-md-4">
                     <base-input v-model.trim="company.account_phone" label="Phone Number:" placeholder="58424597852"/>
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
import { mapMutations } from "vuex";
const {
  required,
  minLength,
  maxLength,
  email,
  sameAs,
  alpha
} = require("vuelidate/lib/validators");
import services from "../../commons/services/company";
export default {
  name: "EditCompany",
  data() {
    return {
      company: {
        name: "",
        address: "",
        phone: "",
        email: "",
        vat_number: "",
        account_username: "",
        account_first_name: "",
        account_last_name: "",
        account_phone: "",
        account_email: "",
      },
      password: "",
      repeatPassword: "",
    };
  },
  created() {
       this.getCompany(this.$route.params.id)
  },
  methods: {
      getCompany(_id){
          services.company.getOneCompany(_id).then((response)=>{
              if (response.data.code === 200) {
                  let data = response.data.data                 
                this.company.name = data.name
                this.company.address = data.address
                this.company.phone = data.phone
                this.company.email = data.email
                this.company.vat_number = data.vat_number

                this.company.account_username = data.account_username
                this.company.account_first_name = data.account_first_name
                this.company.account_last_name = data.account_last_name
                this.company.account_phone = data.account_phone
                this.company.account_email = data.account_email
              }
          })
      },
      editCompany(_id){
        let body = this.company
        if (this.password !== '') {
          body["account_password"] =this.password
        }
        services.company.updateCompany(_id, body).then((response)=>{
          if (response.data.data !== null) {
            this.$router.push('/companies') 
          } else {
            
          }
        })
      },
    ...mapMutations(["setActiveItem"])
  },
  validations: {
    user: {
      first_name: {
        required,
        minLength: minLength(5),
        maxLength: maxLength(45)
      },
      last_name: {
        minLength: minLength(5),
        maxLength: maxLength(45)
      },
      email: {
        required,
        email
      },
      email_two: {
        email
      },
      password: {
        required,
        minLength: minLength(8),
        maxLength: maxLength(45)
      },
      address: {
        maxLength: maxLength(45)
      },
      postal_code: {
        maxLength: maxLength(45)
      },
      phone: {
        minLength: minLength(7),
        maxLength: maxLength(15)
      },
      optional_phone: {
        minLength: minLength(7),
        maxLength: maxLength(15)
      },
      optional_phone_two: {
        minLength: minLength(7),
        maxLength: maxLength(15)
      },
      country: {
        required,
        minLength: minLength(8),
        maxLength: maxLength(45)
      },
      company: {
        required,
        minLength: minLength(8),
        maxLength: maxLength(45)
      },
      type_user: {
        required,
        alpha
      },
      device_id: {
        minLength: minLength(5),
        maxLength: maxLength(45)
      },
      family_name: {
        minLength: minLength(5),
        maxLength: maxLength(45)
      },
      notes: {
        maxLength: maxLength(45)
      },
      town: {
        maxLength: maxLength(45)
      },
      secondary_notes: {
        maxLength: maxLength(45)
      }
    },
    repeatPassword: {
      sameAsPassword: sameAs("user.password")
    }
  },
  components: {}
};
</script>
<style lang="scss"></style>
