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
          <base-button @click="$router.push('/branchs')" size="sm" type="neutral">Back</base-button>
          <base-button @click="$router.push('/new-service')" size="sm" type="primary">New Service</base-button>
             </div>
      </div>
    </base-header>
    <div class="container-fluid mt--6">
      <div class="card">
        <div class="card-header">
          <h3 class="mb-0">Services of branch NameBranch-NameSupplier</h3>
        </div>
        <div class="card-body">
          <div class="row">
              <div class="col-md-4">
                <label class="form-control-label">Supplier</label>
              </div>
              <div class="col-md-4">
                <label class="form-control-label">Branch</label>
              </div>
          </div>
          <div class="row">
              <div class="col-md-5">
                  <el-select class="select-danger"
                      placeholder="Supplier"
                      v-model="selects.simple">
                    <el-option v-for="option in selects.languages"
                        class="select-danger"
                        :value="option.value"
                        :label="option.label"
                        :key="option.label">
                    </el-option>
                  </el-select>
              </div>
              <div class="col-md-5">
                  <el-select class="select-danger"
                      placeholder="Branch"
                      v-model="selects.simple">
                    <el-option v-for="option in selects.languages"
                        class="select-danger"
                        :value="option.value"
                        :label="option.label"
                        :key="option.label">
                    </el-option>
                  </el-select>
              </div>
          </div>
            <div class="card">
                            <div class="border-0 card-header">
                                <h3 class="mb-0">Services</h3>
                            </div>
                           <div class="card-body">    
                             Aqui se listan los servicios segun el supplier y branch seleccionado      
                              <div class="card-footer py-4 d-flex justify-content-end">
                                  <base-pagination v-model="currentPage" :total="50"></base-pagination>
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
import CardService from './components/CardService';

export default {
  name: "Services",
  data() {
      return {
        selects: {
            simple: '',
            languages: [{value: 'Bahasa Indonesia', label: 'Bahasa Indonesia'},
              {value: 'Bahasa Melayu', label: 'Bahasa Melayu'},
              {value: 'Català', label: 'Català'},
              {value: 'Dansk', label: 'Dansk'},
              {value: 'Deutsch', label: 'Deutsch'},
              {value: 'English', label: 'English'},
              {value: 'Español', label: 'Español'},
              {value: 'Eλληνικά', label: 'Eλληνικά'},
              {value: 'Français', label: 'Français'},
              {value: 'Italiano', label: 'Italiano'},
              {value: 'Magyar', label: 'Magyar'},
              {value: 'Nederlands', label: 'Nederlands'},
              {value: 'Norsk', label: 'Norsk'},
              {value: 'Polski', label: 'Polski'},
              {value: 'Português', label: 'Português'},
              {value: 'Suomi', label: 'Suomi'},
              {value: 'Svenska', label: 'Svenska'},
              {value: 'Türkçe', label: 'Türkçe'},
              {value: 'Íslenska', label: 'Íslenska'},
              {value: 'Čeština', label: 'Čeština'},
              {value: 'Русский', label: 'Русский'},
              {value: 'ภาษาไทย', label: 'ภาษาไทย'},
              {value: '中文 (简体)', label: '中文 (简体)'},
              {value: 'W">中文 (繁體)', label: 'W">中文 (繁體)'},
              {value: '日本語', label: '日本語'},
              {value: '한국어', label: '한국어'}]
          },
       }
    },
  created() {
    this.setActiveItem("services");
  },
  methods: {
    ...mapMutations(["setActiveItem"])
  },
  components: {
    "cad-service":CardService
  }
};
</script>
<style lang="scss">
</style>