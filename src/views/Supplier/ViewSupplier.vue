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
          <base-button @click="$router.push('/supplier')" size="sm" type="neutral">Back</base-button>
          <base-button size="sm" type="primary">Save Supplier</base-button>
        </div>
      </div>
    </base-header>
    <div class="container-fluid mt--6">
      <div class="card mb-4">
        <div class="card-header">
          <h3 class="mb-0">View-Edit Supplier</h3>
        </div>
        <div class="card-body">
          <div class="row">
            <div class="col-md">
                <div class="row">
                   <div class="col-md-4">
                    <base-input v-model.trim="abrbrevation" label="Company:" placeholder="Company"/>
                  </div>
                  <div class="col-md-4">
                     <base-input v-model.trim="title" label="Name:" placeholder="Name"/>
                  </div>
                  <div class="col-md-4">
                    <base-input v-model.trim="abrbrevation" label="First Name:" placeholder="First Name"/>
                  </div>
                  
                  
                </div>
                <div class="row">
                  <div class="col-md-4">
                    <base-input v-model.trim="abrbrevation" label="Last Name:" placeholder="Last Name"/>
                  </div>
                  <div class="col-md-4">
                     <base-input v-model.trim="title" label="Username:" placeholder="Username"/>
                  </div>
                  <div class="col-md-4">
                     <base-input v-model.trim="title" label="Phone:" placeholder="Phone"/>
                  </div>
                </div>
                <div class="row">
                  <div class="col-md-4">
                    <base-input v-model.trim="abrbrevation" label="Optional Phone:" placeholder="Optional Phone"/>
                  </div>
                  <div class="col-md-4">
                    <base-input v-model.trim="abrbrevation" label="Address:" placeholder="Address"/>
                  </div>
                  
                </div>
                <div class="row">
                  <div class="col-md-4">
                    <base-input v-model.trim="abrbrevation" label="Email:" placeholder="Email"/>
                  </div>
                  <div class="col-md-4">
                     <base-input v-model.trim="title" label="Password:" placeholder="Password" type="password"/>
                  </div>
                  <div class="col-md-4">
                    <base-input v-model.trim="abrbrevation" label="Password Comfirm:" placeholder="Password Comfirm" type="password"/>
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
import { mapGetters, mapActions, mapMutations } from "vuex";
export default {
  name: "NewStations"
};
</script>
<style lang="scss">
</style>