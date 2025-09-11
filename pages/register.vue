<template>
  <div class="static_page_content_wrapper register">
    <div class="page_content">
      <img class="circel d-none d-lg-block" src="~/assets/media/images/circel.svg" alt="" />
      <div class="container pt-16 pb-16">
        <div class="text-center">
          <img src="~/assets/media/logo/logo.png" width="200" height="150" alt="Logo" />
        </div>
        <div class="w-100 mt-16 gap-4 d-flex flex-column flex-lg-row justify-content-between align-center">
          <div class="img w-100 d-none d-lg-block">
            <img width="600" src="~/assets/media/images/sideImg.svg" alt="Tajamaly" />
          </div>
          <div class="form w-100">
            <form action="">
              <h1>{{ $t('register.title') }}</h1>
              <h5 class="pt-5 pb-3">{{ $t('register.provider_data') }}</h5>
              <!-- image -->
              <ValidationProvider rules="required" :name="$t('register.provider_avatar')">
                <p>{{ $t('register.provider_avatar') }}</p>
                <div class="form-group main_input">
                  <input type="file" @change="changeAvatar" style="display: none" id="shopImg" />
                  <label for="shopImg" class="shopImg">
                    <p v-if="!imageUrl" class="upload">
                      <i class="fa-solid fa-upload"></i>
                    </p>
                    <img class="singleimg" v-else :src="imageUrl" alt="" />
                  </label>
                </div>
              </ValidationProvider>
              <!-- image -->
              <p>{{ $t('register.full_name') }} <span class="text-danger">*</span></p>
              <div class="form-group">
                <img src="~/assets/media/icons/user.png" alt="Logo" class="store" />
                <input v-model="formData.name" class="px-5" type="text" :placeholder="$t('register.enter_name')" />
              </div>
              <p>{{ $t('register.phone') }} <span class="text-danger">*</span></p>
              <div class="form-group">
                <img src="~/assets/media/icons/call.png" alt="Logo" class="store" />
                <input v-model.trim="formData.phone" class="px-5" type="text"
                  :placeholder="$t('register.enter_phone')" />
              </div>
              <p>{{ $t('register.email') }} <span class="text-danger">*</span></p>
              <div class="form-group">
                <img src="~/assets/media/icons/sms2.png" alt="Logo" class="store" />
                <input v-model.trim="formData.email" class="px-5" type="text" autocomplete="off" readonly onfocus="this.removeAttribute('readonly');"
                  :placeholder="$t('register.enter_email')" />
              </div>
              <p>{{ $t('register.password') }} <span class="text-danger">*</span></p>
              <div class="form-group">
                <img src="~/assets/media/icons/key-solid.svg" alt="Logo" class="store" />
                <input v-model.trim="formData.password" class="px-5" :type="showPassword ? 'text' : 'password'" autocomplete="off" readonly onfocus="this.removeAttribute('readonly');"
                  :placeholder="$t('register.enter_password')" />
                  <img
                    v-if = "!showPassword"
                    class="mx-2"
                    src="~/assets/media/icons/eye-slash-solid.svg"
                    alt="Toggle visibility"
                    style="cursor: pointer;"
                    @click="togglePasswordVisibility"
                  />
                  <img
                    v-if = "showPassword"
                    class="mx-2"
                    src="~/assets/media/icons/eye-solid.svg"
                    alt="Toggle visibility"
                    style="cursor: pointer;"
                    @click="togglePasswordVisibility"
                  />
              </div>
              <p>{{ $t('register.password_confirmation') }} <span class="text-danger">*</span></p>
              <div class="form-group">
                <img src="~/assets/media/icons/key-solid.svg" alt="Logo" class="store" />
                <input v-model.trim="formData.password_confirmation" class="px-5" :type="showConfirmPassword ? 'text' : 'password'" autocomplete="off" readonly onfocus="this.removeAttribute('readonly');"
                  :placeholder="$t('register.enter_password')" />
                  <img
                    v-if = "!showConfirmPassword"
                    class="mx-2"
                    src="~/assets/media/icons/eye-slash-solid.svg"
                    alt="Toggle visibility"
                    style="cursor: pointer;"
                    @click="toggleConfirmPasswordVisibility"
                  />
                  <img
                    v-if = "showConfirmPassword"
                    class="mx-2"
                    src="~/assets/media/icons/eye-solid.svg"
                    alt="Toggle visibility"
                    style="cursor: pointer;"
                    @click="toggleConfirmPasswordVisibility"
                  />
              </div>

              <hr />
              <h5 class="pt-5 pb-3">{{ $t('register.salon_data') }}</h5>
              <!-- logo -->
              <ValidationProvider rules="required" :name="$t('register.salon_logo')">
                <p>{{ $t('register.salon_logo') }} <span class="text-danger">*</span></p>
                <div class="form-group main_input">
                  <input type="file" @change="changeLogo" style="display: none;" id="logoimg" />
                  <label for="logoimg" class="shopImg">
                    <p v-if="!logoUrl" class="upload">
                      <i class="fa-solid fa-upload"></i>
                    </p>
                    <img class="singleimg" v-else :src="logoUrl" alt="" />
                  </label>
                </div>
              </ValidationProvider>
              <!-- logo -->
              <!-- second image  -->
              <ValidationProvider rules="required" :name="$t('register.salon_images')">
                <p>{{ $t('register.salon_images') }} <span class="text-danger">*</span></p>
                <div class="form-group main_input w-100">
                  <input type="file" style="display: none" @change="changeImages" multiple id="images" />
                  <label for="images" class="shopImg">
                    <p class="upload"><i class="fa-solid fa-upload"></i></p>
                  </label>
                  <div class="d-flex flex-wrap imagesContainer">
                    <div v-for="(img, index) in imagesUrl" :key="index" class="position-relative mx-3">
                      <img class="smallImg" :src="img.url" alt="" />
                      <span @click="removeimg(index, img.name)" class="x">X</span>
                    </div>
                  </div>
                </div>
              </ValidationProvider>
              <!-- second image -->
              <p>{{ $t('register.salon_name_ar') }} <span class="text-danger">*</span></p>
              <div class="form-group">
                <input v-model="formData.salon_name_ar" class="px-5" type="text"
                  :placeholder="$t('register.salon_name_ar')" />
              </div>
              <p>{{ $t('register.salon_name_en') }} <span class="text-danger">*</span></p>
              <div class="form-group">
                <input v-model="formData.salon_name_en" class="px-5" type="text"
                  :placeholder="$t('register.salon_name_en')" />
              </div>
              <!-- desc -->
              <ValidationProvider rules="required|min:3" :name="$t('register.salon_desc_ar')">
                <p>{{ $t('register.salon_desc_ar') }} <span class="text-danger">*</span></p>
                <div class="form-group main_input" style="height: 100px;">
                  <!-- <img
                      src="~/assets/media/images/desc.png"
                      alt="Logo"
                      class="desc"
                    /> -->
                  <textarea class="px-5 w-100 h-100" v-model="formData.salon_desc_ar"
                    :placeholder="$t('register.salon_desc_ar')"></textarea>
                </div>
              </ValidationProvider>
              <ValidationProvider rules="required|min:3" :name="$t('register.salon_desc_en')">
                <p>{{ $t('register.salon_desc_en') }} <span class="text-danger">*</span></p>
                <div class="form-group main_input" style="height: 100px;">
                  <!-- <img
                      src="~/assets/media/images/desc.png"
                      alt="Logo"
                      class="desc"
                    /> -->
                  <textarea type="text" class="px-5 w-100 h-100" v-model="formData.salon_desc_en"
                    :placeholder="$t('register.salon_desc_en')"></textarea>
                </div>
              </ValidationProvider>
              <!-- desc -->

              <!-- phone -->
              <ValidationProvider rules="required" :name="$t('register.salon_number')">
                <p>{{ $t('register.salon_number') }} <span class="text-danger">*</span></p>
                <div class="form-group main_input">
                  <!-- <img
                      src="~/assets/media/images/phone.png"
                      alt="Logo"
                      class="phone"
                    /> -->
                  <input class="px-5" type="text" :placeholder="$t('register.salon_number')"
                    v-model="formData.salon_number" />
                </div>
              </ValidationProvider>
              <!-- phone -->
              <div class="d-flex justify-content-between gap-3">
                <div class="position-relative mb-3 w-50">
                  <p>{{ $t('register.main_cat') }} <span class="text-danger">*</span></p>
                  <multiselect
                      @input="getSubCategories(formData.category?.id)"
                      v-model="formData.category"
                      :options="filteredCategories"
                      track-by="id"
                      label="name"
                      :searchable="false"
                      :close-on-select="true"
                      :show-labels="false"
                      :placeholder="$t('register.main_cat')"
                      :multiple="false"
                      open-direction="bottom"
                    >
                    </multiselect>
                </div>

                <!-- Subcategory Section -->
                <div class="position-relative mb-3 w-50">
                  <p>{{ $t('register.sub_cat') }} <span class="text-danger">*</span></p>
                  <multiselect
                    v-model="formData.subCategory"
                    :options="subCategories"
                    track-by="id"
                    label="name"
                    :searchable="false"
                    :close-on-select="true"
                    :show-labels="false"
                    :placeholder="$t('register.sub_cat')"
                    :multiple="true"
                    open-direction="bottom"
                  >
                  </multiselect>
                </div>
              </div>
              <!-- Dynamic Category and Subcategory Fields -->
              <div v-for="(categoryField, index) in dynamicCategories" :key="index" class="mb-3">
                <div class="d-flex justify-content-between gap-3">
                  <div class="position-relative w-50">
                    <p>{{ $t('register.main_cat') }} #{{ index + 1 }}</p>
                    <multiselect
                      @input="getSubCategoriesForRow(index)"
                      v-model="categoryField.mainCategory"
                      :options="filteredCategories"
                      track-by="id"
                      label="name"
                      :searchable="false"
                      :close-on-select="true"
                      :show-labels="false"
                      :placeholder="$t('register.main_cat')"
                      :multiple="false"
                      open-direction="bottom"
                    >
                    </multiselect>
                  </div>

                  <div class="position-relative w-50">
                    <p>{{ $t('register.sub_cat') }} #{{ index + 1 }}</p>
                    <multiselect
                      v-model="categoryField.subCategory"
                      :options="categoryField.subCategories"
                      track-by="id"
                      label="name"
                      :searchable="false"
                      :close-on-select="true"
                      :show-labels="false"
                      :placeholder="$t('register.sub_cat')"
                      :multiple="true"
                      open-direction="bottom"
                    >
                    </multiselect>
                  </div>
                  <button type="button" class="btn btn-outline-danger mt-5 pb-2"
                    style="border-radius: 50%; height: 40px; width: 40px; padding-inline-end: 20px;" @click="removeCategoryField(index)"
                    v-if="dynamicCategories.length > 0">
                    <i class="fa fa-minus"></i>
                  </button>
                </div>
              </div>

              <!-- Button to Add New Category and Subcategory -->
              <div class="d-flex justify-content-end">
                <button type="button" class="btn btn-outline-primary" style="border-radius: 50%;" @click="addCategoryField">
                  <i class="fa fa-plus"></i>
                </button>
              </div>

              <!-- Commercial  -->
              <ValidationProvider rules="required" :name="$t('contact.prepare')">
                <p>{{ $t('register.commerical_number') }} <span class="text-danger">*</span></p>
                <div class="form-group main_input">
                  <!-- <img
                      src="~/assets/media/images/store.png"
                      alt="Logo"
                      class="pre"
                    /> -->
                  <input type="text" class="px-5" v-model="formData.Commercial"
                    :placeholder="$t('register.commerical_number')" />
                </div>
              </ValidationProvider>
              <!-- Commercial  -->
               <!-- maroof_number  -->
              <ValidationProvider rules="required" :name="$t('contact.prepare')">
                <p>{{ $t('register.maroof_number') }}</p>
                <div class="form-group main_input">
                  <!-- <img
                      src="~/assets/media/images/store.png"
                      alt="Logo"
                      class="pre"
                    /> -->
                  <input type="text" class="px-5" v-model="formData.maroof_number"
                    :placeholder="$t('register.maroof_number_placeholder')" />
                </div>
              </ValidationProvider>
              <!-- maroof_number  -->
              <hr />
              <!-- location -->
              <h5 class="pt-5 pb-3">{{ $t('register.address') }}</h5>
              <p>{{ $t('register.region') }} <span class="text-danger">*</span></p>
              <div class="position-relative mb-3">
                <multiselect
                  v-model="formData.area"
                  :options="areas"
                  track-by="id"
                  label="name"
                  :searchable="false"
                  :close-on-select="true"
                  :show-labels="false"
                  :placeholder="$t('register.region')"
                  :multiple="false"
                  open-direction="bottom"
                >
                </multiselect>
              </div>
              <!-- location -->

              <!-- map -->
              <div class="mapContent">
                <!-- <img src="~/assets/media/images/location.png" alt="" /> -->
                <p>{{ $t('register.map') }} <span class="text-danger">*</span></p>
              </div>
              <!-- map -->
              <p>{{ $t("register.address") }}: {{ place }}</p>
              <GmapMap :center="center" :zoom="7" map-type-id="terrain"
                style="width: 100%; height: 300px" @click="handleMapClick">
                <GmapMarker :position="marker.position" :clickable="true" :draggable="true" @click="markerClicked"
                  @dragend="markerDragged($event)" />
              </GmapMap>
              <div class="d-flex align-center gap-2 check my-5">
                <input type="checkbox" v-model="formData.terms" />
                <nuxt-link :to="localePath('/terms')" target="_blank">{{ $t('register.accept_terms') }} <span class="text-danger">*</span></nuxt-link>
              </div>
              <button :class="isLoading ? 'register_btn_disabled' : 'register_btn'" @click="submitFrom" type="button" :disabled="isLoading">
                {{ $t('register.save') }}
              </button>
            </form>
            <v-dialog v-model="showDialog" max-width="400">
              <v-card>
                <div class="text-center p-5">
                  <h5>{{ $t('register.verification_code_sent') }}</h5>
                </div>
                <v-card-text dir="ltr" class="my-3">
                  <v-otp-input v-model="otp" :loading="isLoading" label="One-Time Password" length="4"
                    style="border-radius: 20px;"></v-otp-input>
                </v-card-text>
                <div class="m-3">{{ $t('register.resend_code_timer') }} 00:{{ timer }}</div>
                <v-card-actions class="pb-5">
                  <v-btn class="verify_code" @click="verifyOtp">{{ $t('register.verify_code') }}</v-btn>
                  <v-spacer></v-spacer>
                  <v-btn @click="resendOtp" class="resend_btn" :disabled="timer > 0">{{ $t('register.resend_code') }}</v-btn>
                </v-card-actions>
              </v-card>
            </v-dialog>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ValidationProvider, ValidationObserver } from 'vee-validate'

// import Multiselect from 'vue-multiselect'

export default {
  // components: {
  //   Multiselect,
  // },
  layout: 'register',
  data() {
    return {
      dynamicCategories: [],
      imageUrl: '',
      imageFile: '',
      logoUrl: '',
      logoFile: '',
      imagesUrl: [],
      imagesFiles: [],
      showDialog: false,
      isLoading: false,
      otpPhone: null,
      otpToken: null,
      otp: null,
      showPassword: false,
      showConfirmPassword: false,
      timer: 60,
      formData: {
        type: null,
        name: null,
        phone: null,
        email: null,
        password: null,
        password_confirmation: null,
        terms: false,
        salon_name_ar: '',
        salon_name_en: '',
        salon_desc_ar: '',
        salon_desc_en: '',
        salon_number: '',
        category: null,
        area: null,
        subCategory: null,
        Commercial: '',
        maroof_number: '',
      },

      // google map

      center: { lat: 24.7136, lng: 46.6753 },
      zoom: 10,
      currentPlace: null,
      marker: {
        position: { lat: 24.7136, lng: 46.6753 }, // Initial marker position (Riyadh)
      },

      polylineOptions: {
        strokeColor: '#FF0000', // Red color
        strokeOpacity: 1.0,
        strokeWeight: 2,
        geodesic: true,
      },
      Latitude: 24.7136,
      Longitude: 46.6753,
      Radius: '',
      place: '6986 Ibn Al Athir, 3895, Ar Rahmaniyyah, Riyadh 12341, Saudi Arabia',
      categories: [],
      areas: [],
      subCategories: [],
      // google map
      selected: null,
      options: ['list', 'of', 'options'],
    }
  },
  methods: {
    togglePasswordVisibility() {
      this.showPassword = !this.showPassword;
    },
    toggleConfirmPasswordVisibility() {
      this.showConfirmPassword = !this.showConfirmPassword;
    },
    addCategoryField() {
      this.dynamicCategories.push({
        mainCategory: {id: null},
        subCategory: null,
        subCategories: [],
      });
    },

    removeCategoryField(index) {
      this.dynamicCategories.splice(index, 1);
    },

    async getCategories() {
      try {
        const response = await this.$axios.get(`client-api/v1/categories?page=0&limit=0`);
        this.categories = response.data.data;
      } catch (error) {
        console.log('catch : ' + error);
      }
    },

    async getSubCategoriesForRow(index) {
      this.$set(this.dynamicCategories, index, {
        ...this.dynamicCategories[index],
        subCategory: [],
      });
      const categoryId = this.dynamicCategories[index].mainCategory?.id;
      try {
        const response = await this.$axios.get(`client-api/v1/sub-categories?categoryId=${categoryId}&page=0&limit=0`);
        this.$set(this.dynamicCategories, index, {
          ...this.dynamicCategories[index],
          subCategories: response.data.data,
        });
      } catch (error) {
        console.log('catch : ' + error);
      }
    },

    async getSubCategories(id) {
      this.formData.subCategory=[];
      try {
        const response = await this.$axios.get(`client-api/v1/sub-categories?categoryId=${id}&page=0&limit=0`);
        this.subCategories = response.data.data;
      } catch (error) {
        console.log('catch : ' + error);
      }
    },
    changeAvatar(event) {
      const file = event.target.files[0]
      console.log(file)
      if (file) {
        if (file.name.endsWith('.png') || file.name.endsWith('.jpg') || file.name.endsWith('.jpeg')){
          this.imageUrl = URL.createObjectURL(file)
          this.imageFile = file
        }
        else {
          this.$toast.error(this.$t("register.image_validation"));
          event.target.value = '';
        }
      }
    },
    changeLogo(event) {
      const file = event.target.files[0]
      if (file) {
        if (file.name.endsWith('.png') || file.name.endsWith('.jpg') || file.name.endsWith('.jpeg')){
          this.logoUrl = URL.createObjectURL(file)
          this.logoFile = file
        }
        else {
          this.$toast.error(this.$t("register.image_validation"));
          event.target.value = '';
        }
      }
    },

    changeImages(event) {
      let files = event.target.files;
      let imagesFiles = Array.from(files);
      let validImageFiles = imagesFiles.filter(file => file.name.endsWith('.png') || file.name.endsWith('.jpg') || file.name.endsWith('.jpeg'));
      this.imagesFiles = [...this.imagesFiles, ...validImageFiles];
      validImageFiles.forEach((ele) => {
        this.imagesUrl.push({
            name: ele.name,
            url: URL.createObjectURL(ele),
        });
      });
        if (imagesFiles.length !== validImageFiles.length) {
        this.$toast.error(this.$t("register.image_validation"));
        event.target.value = ''; 
      }
      console.log(this.imagesUrl);
    },

    removeimg(index, nameToDelete) {
      this.imagesUrl.splice(index, 1);
      this.imagesFiles = this.imagesFiles.filter(
        (item) => item.name !== nameToDelete
      );
    },
    async submitFrom() {
      try {
        this.isLoading = true
        const REQUEST_DATA = new FormData()
        if (this.imageFile != ''){
          REQUEST_DATA.append('user[avatar]', this.imageFile)
        }
        REQUEST_DATA.append('user[name]', this.formData.name)
        REQUEST_DATA.append('user[mobile]', this.formData.phone)
        REQUEST_DATA.append('user[email]', this.formData.email)
        REQUEST_DATA.append('user[password]', this.formData.password)
        REQUEST_DATA.append(
          'user[password_confirmation]',
          this.formData.password_confirmation
        )
        REQUEST_DATA.append('salon[logo]', this.logoFile);
        this.imagesFiles.map((ele, index) => {
          REQUEST_DATA.append(`salon[images][]`, ele)
        })
        REQUEST_DATA.append('salon[name][ar]', this.formData.salon_name_ar)
        REQUEST_DATA.append('salon[name][en]', this.formData.salon_name_en)
        REQUEST_DATA.append('salon[description][ar]', this.formData.salon_desc_ar)
        REQUEST_DATA.append('salon[description][en]', this.formData.salon_desc_en)
        if (this.formData.category?.id){
          REQUEST_DATA.append('salon[category_ids][]', this.formData.category?.id)
        }
        if (this.formData.subCategory){
          for (let sub of this.formData.subCategory){
            REQUEST_DATA.append('salon[sub_category_ids][]', sub?.id);
          }
        }
        if (this.dynamicCategories){
          for (let catKey in this.dynamicCategories) {
            let cat = this.dynamicCategories[catKey];
            REQUEST_DATA.append('salon[category_ids][]', cat.mainCategory?.id);
            for (let sub2 of cat.subCategory){
              REQUEST_DATA.append('salon[sub_category_ids][]', sub2?.id);
            }
          }
        }
        REQUEST_DATA.append('salon[number]', this.formData.salon_number)
        REQUEST_DATA.append('salon[commercial_number]', this.formData.Commercial)
        if (this.formData.maroof_number != null){
          REQUEST_DATA.append('salon[maroof_number]', this.formData.maroof_number)
        }
        REQUEST_DATA.append('salon[region_id]', this.formData.area?.id)
        REQUEST_DATA.append('salon[lat]', this.Latitude)
        REQUEST_DATA.append('salon[long]', this.Longitude)
        REQUEST_DATA.append('salon[address]', this.place)
        REQUEST_DATA.append('terms', this.formData.terms ? 1 : 0)
        await this.$axios
          .$post('provider-api/v1/auth/register', REQUEST_DATA)
          .then((response) => {
            this.formData.name = null
            this.formData.phone = null
            this.formData.email = null
            this.formData.password = null
            this.formData.password_confirmation = null
            this.formData.terms = false
            this.imageUrl= '',
            this.imageFile= '',
            this.logoUrl= '',
            this.logoFile= '',
            this.imagesUrl= [],
            this.imagesFiles= [],
            this.place= '6986 Ibn Al Athir, 3895, Ar Rahmaniyyah, Riyadh 12341, Saudi Arabia',
            this.Latitude= 24.7136,
            this.Longitude= 46.6753,
            this.marker= {
              position: { lat: 24.7136, lng: 46.6753 }, // Initial marker position (Riyadh)
            },
            this.Radius= '',
            this.center= { lat: 24.7136, lng: 46.6753 },
            this.zoom= 10,
            this.currentPlace= null,
            this.otpToken = response.data.access_token
            this.otpPhone = response.data.user.mobile

            this.showDialog = true
            this.startTimer();
            /*this.$swal.fire({
              position: 'top',
              type: 'success',
              text: this.$t('register.registered_success'),
              showConfirmButton: false,
              timer: 6000,
            })*/
            this.isLoading = false

            // this.$router.push(this.localePath({ path: '/' }))
          })
          .catch((error) => {
            this.$toast.error(error.response.data.message);
            this.isLoading = false
          })
      } catch (error) {
        console.log('try catch =>', error)
      }
    },
    async verifyOtp() {
      try {
        this.isLoading = true
        const REQUEST_DATA = new FormData();
        REQUEST_DATA.append('code', this.otp)
        REQUEST_DATA.append('is_changed', 0)
        await this.$axios
          .$post('provider-api/v1/auth/verify-otp', REQUEST_DATA, {
            headers: {
              Authorization: `Bearer ${this.otpToken}`,
            },
          })
          .then((response) => {
            this.$swal.fire({
              position: 'top',
              type: 'success',
              text: this.$t('register.verified_success'),
              showConfirmButton: false,
              timer: 5000,
            })
            this.isLoading = false
            this.otpPhone = null
            this.otp = null
            this.showDialog = false
            //reset form
            this.formData = {
              name: null,
              phone: null,
              email: null,
              password: null,
              password_confirmation: null,
              terms: false,
              salon_name_ar: null,
              salon_name_en: null,
              salon_desc_ar: null,
              salon_desc_en: null,
              category: null,
              subCategory: null,
              salon_number: null,
              Commercial: null,
              maroof_number: null,
              area: null,
            };
            this.imageFile = null;
            this.logoFile = null;
            this.imagesFiles = [];
            this.dynamicCategories = [];
            this.Latitude = null;
            this.Longitude = null;
          
            this.otpPhone = null;
            this.otp = null;
            this.showDialog = false;
            // this.$router.push(this.localePath({ path: '/' }))
          })
          .catch((error) => {
            this.$toast.error(error.response.data.message);
            this.isLoading = false
            this.otp = null

            console.log(error)
          })
      } catch (error) {
        console.log('try catch =>', error)
      }
    },
    startTimer() {
      this.timer = 60;
      const interval = setInterval(() => {
        if (this.timer > 0) {
          this.timer--;
        } else {
          clearInterval(interval);
        }
      }, 1000);
    },
    async resendOtp() {
      this.startTimer();
      try {
        this.isLoading = true
        const REQUEST_DATA = new FormData()
        REQUEST_DATA.append('phone', this.otpPhone)
        await this.$axios
          .$post('provider-api/v1/auth/resend-otp', REQUEST_DATA, {
            headers: {
              Authorization: `Bearer ${this.otpToken}`,
            },
          })
          .then((response) => {
            this.$toast.success(this.$t('register.resent_success'));
            this.isLoading = false
            // this.$router.push(this.localePath({ path: '/' }))
          })
          .catch((error) => {
            this.$toast.error(error.response.data.message);
            this.isLoading = false
            console.log(error)
          })
      } catch (error) {
        console.log('try catch =>', error)
      }
    },
    async getCategories() {
      try {
        return await this.$axios
          .get(`client-api/v1/categories?page=0&limit=0`)
          .then((response) => {
            this.categories = response.data.data;
          })
          .catch((error) => {
            console.log(error)
          })
      } catch (error) {
        console.log('catch : ' + error)
      }
    },
    async getAreas() {
      try {
        return await this.$axios
          .get(`client-api/v1/regions`)
          .then((response) => {
            this.areas = response.data.data;
          })
          .catch((error) => {
            console.log(error)
          })
      } catch (error) {
        console.log('catch : ' + error)
      }
    },
    // google map
    handleMapClick(event) {
      const lat = event.latLng.lat()
      const lng = event.latLng.lng()

      const radius = this.calculateDistance(
        lat,
        lng,
        this.center.lat,
        this.center.lng
      )

      const geocoder = new google.maps.Geocoder()
      const latLng = new google.maps.LatLng(lat, lng)

      geocoder.geocode({ location: latLng }, (results, status) => {
        if (status === 'OK' && results[0]) {
          this.Latitude = lat
          this.Longitude = lng
          this.Radius = radius
          this.place = results[0].formatted_address

          console.log('Latitude:', lat)
          console.log('Longitude:', lng)
          console.log('Radius:', radius)
          console.log('Place:', results[0].formatted_address)

          this.marker.position = { lat, lng } // Update the marker's position
        }
      })
    },

    calculateDistance(lat1, lng1, lat2, lng2) {
      const R = 6371 // Radius of the earth in kilometers
      const dLat = this.deg2rad(lat2 - lat1)
      const dLng = this.deg2rad(lng2 - lng1)
      const a =
        Math.sin(dLat / 2) * Math.sin(dLat / 2) +
        Math.cos(this.deg2rad(lat1)) *
        Math.cos(this.deg2rad(lat2)) *
        Math.sin(dLng / 2) *
        Math.sin(dLng / 2)
      const c = 2 * Math.atan2(Math.sqrt(a), Math.sqrt(1 - a))
      const distance = R * c * 1000 // Convert to meters
      return distance
    },
    deg2rad(deg) {
      return deg * (Math.PI / 180)
    },
    handleMarkerClick(index) {
      console.log('Marker clicked:', index)
    },

    setPlace(place) {
      this.currentPlace = place
    },

    markerClicked() {
      // Handle marker click event
      const lat = this.marker.position.lat
      const lng = this.marker.position.lng
      const radius = this.calculateDistance(
        lat,
        lng,
        this.center.lat,
        this.center.lng
      )
      console.log('Marker clicked:', lat, lng)
      console.log(radius)
    },

    markerDragged(event) {
      const lat = event.latLng.lat()
      const lng = event.latLng.lng()
      this.marker.position = { lat, lng }

      const radius = this.calculateDistance(
        lat,
        lng,
        this.center.lat,
        this.center.lng
      )
      this.Latitude = lat
      this.Longitude = lng
      this.Radius = radius
      console.log('Marker dragged:', lat, lng)
      console.log(radius)
    },
    // google map
  },
  mounted() {
    this.getCategories()
    this.getAreas()
    setTimeout(() => {
      this.isLoading = false
      document.body.style.overflow = 'unset'
    }, 2000)
  },
  computed: {
    filteredCategories() {
      if (!Array.isArray(this.categories)) {
        return [];
      }

      const selectedCategories = [
        ...this.dynamicCategories.map(item => item.mainCategory?.id),
        this.formData.category?.id
      ];

      return this.categories.filter(category => !selectedCategories.includes(category.id));
    },

},
watch: {
  timer(newVal) {
    if (newVal === 0) {
      console.log("Timer reached zero.");
    }
  },
}
}
</script>

<style>
.dis {
  background-color: #A700FE;
  color: white;
  width: 100%;
  padding: 10px;
  cursor: not-allowed;
  pointer-events: none;
  border-radius: 10px;
}

.multiselect__tags {
  border: none;
}

.multiselect {
  display: flex !important;
  background-color: white !important;
  border-radius: 10px !important;
  margin-bottom: 10px;
}

.register_btn {
  background-color: #A700FE;
  color: white;
  width: 100%;
  padding: 10px;
  border-radius: 10px;
}

.register_btn_disabled {
  background-color: #e4b2ff;
  cursor: not-allowed !important;
  color: white;
  width: 100%;
  padding: 10px;
  border-radius: 10px;
}

p {
  margin-bottom: 10px !important;
}

.check p {
  margin-bottom: 0px !important;
}

.check a {
  color: black !important;
}

.check {
  margin-bottom: 10px;
}

.circel {
  position: absolute;
  z-index: 1;
}

.img {
  z-index: 1;
}

.form {
  background-color: #F8EBFF;
  border-radius: 40px;
  padding: 20px;
}

.form-group {
  margin-bottom: 20px;
  background-color: white;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 20px;
  width: 100%;
  min-height: 50px;
  overflow: hidden;
  padding-right: 10px;
}

.form-group input {
  background-color: white;
  width: 100%;
  height: 100%;
}

.form-group img {
  width: 20px;
  height: 20px;
}

.position-relative img, .singleimg {
  width: 80px !important;
  height: 80px !important;
  border-radius: 20px;
  margin-top: 10px;
  margin-bottom: 10px;
}

.form-group input:focus {
  border: none;
  outline: none;
}

.header_content_wrapper {
  position: sticky;
  background: var(--dark_secondary_theme_clr);
}

.verify_code {
  background-color: #A700FE !important;
  color: white !important;
}

.resend_btn {
  background-color: #F8EBFF !important;
}

.store {
  margin-inline-start: 15px;
}
.x {
  cursor: pointer;
  top: 0;
  font-weight: bold;
  color: white;
  justify-content: center;
  align-items: center;
  border-radius: 50%;
  z-index: 99;
  background-color: red;
  width: 20px;
  height: 20px;
  display: flex;
  left: 0;
  margin: 7px auto;
}
.register .btn{
  border-color: #A700FE;
  color: #A700FE;
}
.register .btn:hover{
  background-color: #A700FE;
  color: white;
}
.register .multiselect__option--highlight{
  background-color: #A700FE !important;
}
.register .multiselect__tag{
  background-color: #A700FE !important;
}
.register .upload{
  color: #AFAFB0;
  font-size: 20px;
  cursor: pointer;
}
.swal2-show{
  height: 400px !important;
  margin: auto !important;
}
</style>
