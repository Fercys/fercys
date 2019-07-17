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
          <base-button @click="$router.push('/reservations')" size="sm" type="neutral">Back</base-button>
          <base-button @click="saveUser()" size="sm" type="primary">Save Reservation</base-button>
        </div>
      </div>
    </base-header>

  <div class="container-fluid mt--6">
    <div class="card mb-4">
      

        <el-tabs type="border-card" @tab-click="handleClick">
          <el-tab-pane label="Addres/Datetime">
            <div class="col-md">          
                <div class="row">
                  <div class="col-md-4">
                    <base-input v-model.trim="title" label="Reservation ID:" placeholder="Reservation ID:"  />
                  </div>
                  <div class="col-md-3">
                        <label>Reservation type:</label><br>
                          <el-select class="select-danger"
                            placeholder="Select type"
                            v-model="selects.simple">
                            <el-option v-for="option in selects.type"
                                class="select-danger"
                                :value="option.value"
                                :label="option.label"
                                :key="option.label">
                            </el-option>
                        </el-select>
                  </div>
                  <div class="col-md-5">
                        <label>Service:</label><br>
                          <el-select class="select-danger"
                            placeholder="Select Service"
                            v-model="selects.simpleservice">
                            <el-option v-for="option in selects.service"
                                class="select-danger"
                                :value="option.value"
                                :label="option.label"
                                :key="option.label">
                            </el-option>
                        </el-select>
                  </div>
                </div>

              
                <div class="row mt-3">
                  <div class="col-md-4">
                      <base-input v-model.trim="date" label="Date:" placeholder="Date"/>
                  </div>
                  <div class="col-md-4">
                    <base-input v-model.trim="time" label="Time:" placeholder="Time"/>
                  </div>
                </div>

                <div class="row">
                  <div class="col-md-4">
                    <base-input label="From:">
                      <textarea class="form-control" v-model.trim="from" rows="2" placeholder="From"></textarea>
                    </base-input>
                  </div>
                  <div class="col-md-4">
                    <base-input label="To:">
                      <textarea class="form-control" v-model.trim="to" rows="2" placeholder="To"></textarea>
                    </base-input>
                  </div>
                </div>  
                <div class="row">
                  <div class="col-md-4">
                    <base-input v-model.trim="flight_no" label="Flight no:" placeholder="Flight no"/>
                  </div>
                </div>  
            </div>
          
          </el-tab-pane>
          <el-tab-pane label="Service/Supplier"> 
              <div class="col-md">
                
                    <div class="row">
                        <div class="col-md-4">
                          <label>Supplier:</label><br>
                            <el-select class="select-danger"
                                placeholder="Supplier"
                                v-model="selects.simplesup">
                              <el-option v-for="option in selects.languages"
                                  class="select-danger"
                                  :value="option.value"
                                  :label="option.label"
                                  :key="option.label">
                              </el-option>
                            </el-select>
                        </div>
                        <div class="col-md-4">
                          <label>Branch:</label><br>
                            <el-select class="select-danger"
                                placeholder="Branch"
                                v-model="selects.simplebra">
                              <el-option v-for="option in selects.languages"
                                  class="select-danger"
                                  :value="option.value"
                                  :label="option.label"
                                  :key="option.label">
                              </el-option>
                            </el-select>
                        </div>
                        <div class="col-md-4">
                                  <base-input v-model.trim="driver" label="Driver:" placeholder="Driver"/>
                        </div>
                    </div>

                          <div class="card">
                            <div class="border-0 card-header">
                                <h3 class="mb-0">Service Type</h3>
                            </div>
                           <div class="card-body">    
                             Aqui se listan los servicios segun el supplier y branch seleccionado      
                              <div class="card-footer py-4 d-flex justify-content-end">
                                  <base-pagination v-model="currentPage" :total="50"></base-pagination>
                              </div>          
                            </div>
                          </div>
              </div>          
          </el-tab-pane>
          <el-tab-pane label="Passenger/Client">
              <div class="col-md">
                      <div class="row">
                        <div class="col-md-3">
                            <base-input v-model.trim="no_of_passengers" label="No. of passengers:" placeholder="No. of passengers"/>
                        </div>
                        <div class="col-md-3">
                          <base-input v-model.trim="main_passenger" label="Main passenger:" placeholder="Main passenger"/>
                        </div>
                        <div class="col-md-3">
                            <base-input v-model.trim="pickup_sign" label="Pickup sign:" placeholder="Pickup sign"/>
                        </div>
                        <div class="col-md-3">
                          <div class="form-group">
                            <label for="exampleFormControlFile1" class="btn btn-block es-select">
                              <img src="@/assets/images/actions/icon-upload-file.svg" alt class="mr-3"> Upload file (.pdf, .word)
                            </label>
                            <input type="file" class="form-control-file d-none" id="exampleFormControlFile1">
                          </div>
                        </div>
                      </div>

                      <div class="row">
                        <div class="col-md-3">
                            <base-input v-model.trim="booking_source" label="Booking Source:" placeholder="Booking Source"/>
                        </div>
                        <div class="col-md-3">
                          <base-input v-model.trim="email" label="Email:" placeholder="Email"/>
                        </div>
                        <div class="col-md-3">
                            <base-input v-model.trim="country_code" label="Country Code:" placeholder="Country Code"/>
                        </div>
                        <div class="col-md-3">
                          <base-input v-model.trim="phone" label="Phone:" placeholder="Phone"/>
                        </div>
                      </div>

                      <div class="row">  
                        <div class="col-md-4">
                          <base-input label="Special requirements:">
                            <textarea class="form-control" v-model.trim="special_requirements" rows="3" placeholder="Special requirements"></textarea>

                          </base-input>
                        </div>
                        <div class="col-md-4">
                          <br>
                          <base-checkbox class="mb-3" v-model.trim="children_seat">  Children seats required  </base-checkbox>
                        </div>
                      </div>
                </div>
          </el-tab-pane>
          <el-tab-pane label="Princing/Payment">
              <div class="col-md">
                    <div class="row">
                      <div class="col-md">
                        <div class="row">
                          <div class="col-md-4">
                              <base-input v-model.trim="net_price" label="Net price:" placeholder="Net price"/>
                          </div>
                          <div class="col-md-4">
                            <base-input v-model.trim="gross_price" label="Gross price:" placeholder="Gross price"/>
                          </div>
                          <div class="col-md-4">
                            <base-input v-model.trim="status" label="Status:" placeholder="Status"/>
                          </div>
                        </div>
                        
                        <div class="row">
                          <div class="col-md-4 align-self-center">
                            <div class="form-check">
                              <input class="form-check-input" type="checkbox" value id="defaultCheck1">
                              <label class="form-check-label" for="defaultCheck1">Special Pricing</label>
                            </div>
                          </div>
                          <div class="col-md-4">
                            <div class="form-group">
                              <select class="form-control" id="exampleFormControlSelect1">
                                <option>1</option>
                                <option>2</option>
                                <option>3</option>
                                <option>4</option>
                                <option>5</option>
                              </select>
                            </div>
                          </div>
                        </div>
                      </div>
                    </div>
                    <div class="row">
                      <div class="col-md">
                        <div class="row">
                          <div class="col-md">
                            <label for="" class="text-uppercase font-weight-bold">Payment</label>
                          </div>
                        </div>


                        <div class="row">
                          <div class="col-md-4">
                              <base-input v-model.trim="invoice" label="Invoice:" placeholder="Invoice"/>
                          </div>
                          <div class="col-md-4">
                            <base-input v-model.trim="client" label="Client:" placeholder="Client"/>
                          </div>
                          <div class="col-md-4">
                            <base-input v-model.trim="booking_reference" label="Booking reference:" placeholder="Booking reference"/>
                          </div>
                        </div>
                        
                      </div>
                    </div>
                    <div class="row">
                      <div class="col-md-4">
                        <base-input v-model.trim="payment_status" label="Payment status:" placeholder="Payment status"/>
                      </div>
                    </div>
               </div>
          </el-tab-pane>
          <el-tab-pane label="Review">
                  <div class="col-md">
                    <div class="row">
                      <div class="col-md">
                        <label for="" class="text-uppercase font-weight-bold" >Address / DATETIME</label>
                      </div>
                    </div>
                    <div class="row">
                      <div class="col-md">
                        <div class="form-group row">
                          <label
                            for="exampleFormControlSelect1"
                            class="col-sm-5 col-form-label es-col-form-label"
                          >Reservation ID:</label>
                          <div class="col-sm-7 align-self-start">
                            <input
                              type="email"
                              class="form-control border-0"
                              id="inputEmail3"
                              placeholder
                              readonly
                            >
                          </div>
                        </div>
                      </div>
                      <div class="col-md">
                        <button
                      class="btn btn-block text-left"
                      v-bind:class="{ 'es-select-active es-icon-airport-active': select === 1, 'es-select es-icon-airport': select !== 1 }"
                      @click="select = 1"
                    >Airport</button>
                      </div>
                      <div class="col-md">
                        <button
                      class="btn btn-block text-left"
                    >Airport</button>
                      </div>
                    </div>
                  </div>

                <div class="row">
                  <div class="col-md-4">
                      <base-input v-model.trim="date" label="Date:" placeholder="Date"/>
                  </div>
                  <div class="col-md-4">
                    <base-input v-model.trim="time" label="Time:" placeholder="Time"/>
                  </div>
                  <div class="col-md-4">
                    <base-input v-model.trim="flight_no" label="Flight no:" placeholder="Flight no"/>
                  </div>
                </div>
                <div class="row">
                  <div class="col-md-4">
                      <base-input v-model.trim="from" label="From:" placeholder="From"/>
                  </div>
                  <div class="col-md-4">
                    <base-input v-model.trim="to" label="To:" placeholder="To"/>
                  </div>
                </div>

                <div class="row">
                  <div class="col-md">
                    <div class="row">
                      <div class="col-md">
                        <label for="" class="text-uppercase font-weight-bold">Service / Supplier</label>
                      </div>
                    </div>
                    
                    <div class="row">
                      <div class="col-md-4">
                          <base-input v-model.trim="supplier" label="Supplier:" placeholder="Supplier"/>
                      </div>
                      <div class="col-md-4">
                        <base-input v-model.trim="branch" label="Branch:" placeholder="Branch"/>
                      </div>
                      <div class="col-md-4">
                        <base-input v-model.trim="service_type" label="Service Type:" placeholder="Service Type"/>
                      </div>
                    </div> 

                  </div>
                </div>
                <div class="row">
                  <div class="col-md">
                    <div class="row">
                      <div class="col-md">
                        <label for="" class="text-uppercase font-weight-bold">Passenger / Client</label>
                      </div>
                    </div>

                    <div class="row">
                      <div class="col-md-4">
                          <base-input v-model.trim="no_of_passengers" label="No of passengers:" placeholder="No of passengers"/>
                      </div>
                      <div class="col-md-4">
                        <base-input v-model.trim="main_passenger" label="Main passenger:" placeholder="Main passenger"/>
                      </div>
                      <div class="col-md-4">
                        <base-input v-model.trim="pickup_sign" label="Pickup sign:" placeholder="Pickup sign"/>
                      </div>
                    </div>

                    <div class="row">
                      <div class="col-md-4">
                          <base-input v-model.trim="booking_source" label="Booking source:" placeholder="Booking source"/>
                      </div>
                      <div class="col-md-4">
                        <base-input v-model.trim="email" label="Email:" placeholder="Email"/>
                      </div>
                      <div class="col-md-4">
                        <base-input v-model.trim="country_code" label="Country code:" placeholder="Country code"/>
                      </div>
                    </div>


                    <div class="row">
                      <div class="col-md-4">
                          <base-input v-model.trim="phone" label="Phone:" placeholder="Phone"/>
                      </div>
                      <div class="col-md-4">
                        <base-input v-model.trim="special_requirements" label="Special requirements:" placeholder="Special requirements"/>
                      </div>
                      <div class="col-md-4 mt-4">
                        <base-checkbox class="mb-3" v-model.trim="children_seats"> Children seats required </base-checkbox>
                      </div>
                    </div>            

                  </div>
                </div>
          </el-tab-pane>
       </el-tabs>      
    </div>
  </div>
  </section>
</template>

<script>
// @ is an alias to /src
import { mapGetters, mapActions, mapMutations } from "vuex";
import CardService from "../Services/components/CardService";
import { Tabs,TabPane,Table, TableColumn, DropdownMenu, DropdownItem, Dropdown} from 'element-ui';
export default {
  name: "NewReservations",
  data() {
    return {
      projects: [
          {
            title: 'Fercys Ramirez',
            type: 'Prueba',
            company: 'Prueba 2 CA',
            country: 'Venezuela',
            countrys: 'Venezuela'
          },
          {
            title: 'Jesus Flores',
            type: 'Prueba',
            company: 'Prueba 2 CA',
            country: 'Venezuela',
            countrys: 'Venezuela'
          },
          {
            title: 'Pablo Palmas',
            type: 'Prueba',
            company: 'Prueba 2 CA',
            country: 'Argentina',
            countrys: 'Venezuela'
          }
        ],
        currentPage: 1, 
      select: 1,
      service: "way",
      active: 1,
      activeName: 'first',
      selects: {
            simple: '',
            simplesup: '',
            simplebra: '',
            type: [
              {value: '1', label: 'Airport'},
              {value: '2', label: 'Station'},
              {value: '3', label: 'Port'}],
            simpleservice: '',
            service: [
              {value: '1', label: 'One Way'},
              {value: '2', label: 'Hourly'}],
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
    };
  },
  created() {
    this.setActiveItem("reservations");
  },
  methods: {
    setActive(index) {
      this.active = index;
      console.log(this.active);
    },
    ...mapMutations(["setActiveItem"]),
      handleClick(tab, event) {
        console.log(tab, event);
      }
  },
  components: {
    "cad-service": CardService,
    [Tabs.name]: Tabs,
    [TabPane.name]: TabPane,
    [TableColumn.name]: TableColumn,
    [Dropdown.name]: Dropdown,
    [DropdownItem.name]: DropdownItem,
    [DropdownMenu.name]: DropdownMenu,
  }
};
</script>
<style lang="scss">
.btn-act {
  background: #ffffff;
  border: 1px solid #e8e8e8;
  box-sizing: border-box;
  border-radius: 1px;
}

.tab-content {
  .tab-pane {
    &:focus {
      outline: none;
    }
  }
  &:focus {
    outline: none;
  }
}

.es-select-active {
  font-weight: normal;
  font-size: 1rem;
  padding-left: 3rem;
  background: #1f1f1f;
  border-radius: 4px;
  color: #ebebeb;
  &:hover {
    color: #ebebeb;
  }
  &:focus {
    outline: none;
    box-shadow: none;
  }
}
.es-select {
  font-weight: normal;
  font-size: 1rem;
  background: #f5f6ff;
  border-radius: 4px;
  padding-left: 3rem;
  color: #000000;
  &:hover {
    color: #000000;
  }
  &:focus {
    outline: none;
    box-shadow: none;
  }
}

.es-icon-airport {
  background-image: url("../../assets/images/icon-stationport-dark.svg");
  background-repeat: no-repeat;
  background-position: 1rem center;
}
.es-icon-airport-active {
  background-image: url("../../assets/images/icon-stationport-grey.svg");
  background-repeat: no-repeat;
  background-position: 1rem center;
}
.es-icon-station {
  background-image: url("../../assets/images/icon-station-dark.svg");
  background-repeat: no-repeat;
  background-position: 1rem center;
}
.es-icon-station-active {
  background-image: url("../../assets/images/icon-station-grey.svg");
  background-repeat: no-repeat;
  background-position: 1rem center;
}

.es-icon-port {
  background-image: url("../../assets/images/icon-port-dark.svg");
  background-repeat: no-repeat;
  background-position: 1rem center;
}
.es-icon-port-active {
  background-image: url("../../assets/images/icon-port-grey.svg");
  background-repeat: no-repeat;
  background-position: 1rem center;
}

.es-icon-way {
  background-image: url("../../assets/images/icon-way-dark.svg");
  background-repeat: no-repeat;
  background-position: 1rem center;
}
.es-icon-way-active {
  background-image: url("../../assets/images/icon-way-grey.svg");
  background-repeat: no-repeat;
  background-position: 1rem center;
}
.es-icon-hourly {
  background-image: url("../../assets/images/icon-hourly-dark.svg");
  background-repeat: no-repeat;
  background-position: 1rem center;
}
.es-icon-hourly-active {
  background-image: url("../../assets/images/icon-hourly-grey.svg");
  background-repeat: no-repeat;
  background-position: 1rem center;
}
</style>