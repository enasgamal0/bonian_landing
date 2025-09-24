<template>
  <div class="static_page_content_wrapper register">
    <div class="page_content">
      <!-- <img class="circel d-none d-lg-block opacity-50" src="~/assets/media/images/circel.svg" alt="" /> -->
      <div class="container pt-16 pb-16">
        <div class="text-center">
          <nuxt-link :to="localePath('/')">
            <img src="~/assets/media/logo/logo.png" width="200" alt="Logo" />
          </nuxt-link>
        </div>
        <div
          class="w-100 mt-16 gap-4 d-flex flex-column flex-lg-row justify-content-between align-center"
        >
          <div class="img w-100 d-none d-lg-block">
            <img
              width="600"
              src="~/assets/media/images/sideImg.svg"
              alt="Bunyan Tech"
            />
          </div>
          <div class="form w-100">
            <form action="">
              <h1 class="text-white">{{ $t('register.title') }}</h1>
              <h5 class="pt-5 pb-3 text-white">
                {{ $t('register.provider_data') }}
              </h5>

              <!-- Service Provider Name - Required -->
              <p class="text-white">
                {{ $t('register.provider_name') }}
                <span class="text-danger">*</span>
              </p>
              <div class="form-group">
                <img
                  src="~/assets/media/icons/user.png"
                  alt="Logo"
                  class="store"
                />
                <input
                  v-model="formData.name"
                  class="px-5"
                  type="text"
                  :placeholder="$t('register.enter_provider_name')"
                />
              </div>

              <!-- Service Provider Image - Optional -->
              <p class="text-white">{{ $t('register.provider_image') }}</p>
              <div class="form-group main_input">
                <input
                  type="file"
                  @change="changeProviderImage"
                  style="display: none"
                  id="providerImg"
                />
                <label for="providerImg" class="shopImg">
                  <p v-if="!providerImageUrl" class="upload">
                    <i class="fa-solid fa-upload"></i>
                  </p>
                  <img
                    class="singleimg"
                    v-else
                    :src="providerImageUrl"
                    alt=""
                  />
                </label>
              </div>

              <!-- Referral Code - Optional -->
              <p class="text-white">{{ $t('register.referral_code') }}</p>
              <div class="form-group">
                <!-- <img src="~/assets/media/icons/gift.png" alt="Logo" class="store" /> -->
                <input
                  v-model.trim="formData.referral_code"
                  class="px-5"
                  type="text"
                  :placeholder="$t('register.enter_referral_code')"
                />
              </div>

              <!-- Description - Optional -->
              <p class="text-white">{{ $t('register.description') }}</p>
              <div class="form-group main_input" style="height: 100px">
                <textarea
                  class="px-5 w-100 h-100"
                  v-model="formData.description"
                  :placeholder="$t('register.enter_description')"
                ></textarea>
              </div>

              <!-- Phone - Required -->
              <p class="text-white">
                {{ $t('register.phone') }} <span class="text-danger">*</span>
              </p>
              <div class="form-group">
                <img
                  src="~/assets/media/icons/call.png"
                  alt="Logo"
                  class="store"
                />
                <input
                  v-model.trim="formData.mobile"
                  class="px-5"
                  type="text"
                  :placeholder="$t('register.enter_phone')"
                />
              </div>

              <!-- Email - Required -->
              <p class="text-white">
                {{ $t('register.email') }} <span class="text-danger">*</span>
              </p>
              <div class="form-group">
                <img
                  src="~/assets/media/icons/sms2.png"
                  alt="Logo"
                  class="store"
                />
                <input
                  v-model.trim="formData.email"
                  class="px-5"
                  type="text"
                  autocomplete="off"
                  readonly
                  onfocus="this.removeAttribute('readonly');"
                  :placeholder="$t('register.enter_email')"
                />
              </div>

              <!-- Password - Required -->
              <p class="text-white">
                {{ $t('register.password') }} <span class="text-danger">*</span>
              </p>
              <div class="form-group">
                <img
                  src="~/assets/media/icons/key-solid.svg"
                  alt="Logo"
                  class="store"
                />
                <input
                  v-model.trim="formData.password"
                  class="px-5"
                  :type="showPassword ? 'text' : 'password'"
                  autocomplete="off"
                  readonly
                  onfocus="this.removeAttribute('readonly');"
                  :placeholder="$t('register.enter_password')"
                />
                <img
                  v-if="!showPassword"
                  class="mx-2"
                  src="~/assets/media/icons/eye-slash-solid.svg"
                  alt="Toggle visibility"
                  style="cursor: pointer"
                  @click="togglePasswordVisibility"
                />
                <img
                  v-if="showPassword"
                  class="mx-2"
                  src="~/assets/media/icons/eye-solid.svg"
                  alt="Toggle visibility"
                  style="cursor: pointer"
                  @click="togglePasswordVisibility"
                />
              </div>

              <!-- Password Confirmation - Required -->
              <p class="text-white">
                {{ $t('register.password_confirmation') }}
                <span class="text-danger">*</span>
              </p>
              <div class="form-group">
                <img
                  src="~/assets/media/icons/key-solid.svg"
                  alt="Logo"
                  class="store"
                />
                <input
                  v-model.trim="formData.password_confirmation"
                  class="px-5"
                  :type="showConfirmPassword ? 'text' : 'password'"
                  autocomplete="off"
                  readonly
                  onfocus="this.removeAttribute('readonly');"
                  :placeholder="$t('register.enter_password_confirmation')"
                />
                <img
                  v-if="!showConfirmPassword"
                  class="mx-2"
                  src="~/assets/media/icons/eye-slash-solid.svg"
                  alt="Toggle visibility"
                  style="cursor: pointer"
                  @click="toggleConfirmPasswordVisibility"
                />
                <img
                  v-if="showConfirmPassword"
                  class="mx-2"
                  src="~/assets/media/icons/eye-solid.svg"
                  alt="Toggle visibility"
                  style="cursor: pointer"
                  @click="toggleConfirmPasswordVisibility"
                />
              </div>

              <!-- Commercial Registration Number - Optional -->
              <p class="text-white">
                {{ $t('register.commercial_registration_number') }}
              </p>
              <div class="form-group">
                <!-- <img src="~/assets/media/icons/document.png" alt="Logo" class="store" /> -->
                <input
                  v-model.trim="formData.commercial_registration_number"
                  class="px-5"
                  type="text"
                  :placeholder="$t('register.enter_commercial_number')"
                />
              </div>

              <!-- Commercial Registration Image - Optional -->
              <p class="text-white">{{ $t('register.commercial_image') }}</p>
              <div class="form-group main_input">
                <input
                  type="file"
                  @change="changeCommercialImage"
                  style="display: none"
                  id="commercialImg"
                />
                <label for="commercialImg" class="shopImg">
                  <p v-if="!commercialImageUrl" class="upload">
                    <i class="fa-solid fa-upload"></i>
                  </p>
                  <img
                    class="singleimg"
                    v-else
                    :src="commercialImageUrl"
                    alt=""
                  />
                </label>
              </div>

              <!-- Previous Works Images - Optional -->
              <p class="text-white">{{ $t('register.previous_works') }}</p>
              <div class="form-group main_input w-100">
                <input
                  type="file"
                  style="display: none"
                  @change="changePreviousWorks"
                  multiple
                  id="previousWorks"
                />
                <label for="previousWorks" class="shopImg">
                  <p class="upload"><i class="fa-solid fa-upload"></i></p>
                </label>
                <div class="d-flex flex-wrap imagesContainer">
                  <div
                    v-for="(img, index) in previousWorksUrl"
                    :key="index"
                    class="position-relative mx-3"
                  >
                    <img class="smallImg" :src="img.url" alt="" />
                    <span @click="removePreviousWork(index, img.name)" class="x"
                      >X</span
                    >
                  </div>
                </div>
              </div>

              <!-- Categories Section with Add/Remove functionality -->
              <div class="categories-section">
                <!-- Category Rows -->
                <div
                  v-for="(categoryRow, index) in categoryRows"
                  :key="index"
                  class="category-row"
                  style="
                    display: flex;
                    gap: 10px;
                    align-items: center;
                    margin-bottom: 15px;
                  "
                >
                  <div class="flex-grow-1">
                    <!-- Main Category -->
                    <p class="text-white">
                      {{ $t('register.main_category') }}
                      <span class="text-danger">*</span>
                    </p>
                    <div class="position-relative mb-3">
                      <multiselect
                        @input="
                          getSubCategories(categoryRow.category_id?.id, index)
                        "
                        v-model="categoryRow.category_id"
                        :options="getAvailableCategories(index)"
                        track-by="id"
                        label="name"
                        :searchable="false"
                        :close-on-select="true"
                        :show-labels="false"
                        :placeholder="$t('register.select_main_category')"
                        :multiple="false"
                        open-direction="bottom"
                      >
                      </multiselect>
                    </div>
                  </div>
                  <div class="flex-grow-1">
                    <!-- Sub Categories -->
                    <p class="text-white">
                      {{ $t('register.sub_categories') }}
                      <span class="text-danger">*</span>
                    </p>
                    <div class="position-relative mb-3">
                      <multiselect
                        v-model="categoryRow.sub_category_ids"
                        :options="categoryRow.subCategories"
                        track-by="id"
                        label="name"
                        :searchable="false"
                        :close-on-select="true"
                        :show-labels="false"
                        :placeholder="$t('register.select_sub_categories')"
                        :multiple="true"
                        open-direction="bottom"
                      >
                      </multiselect>
                    </div>
                  </div>
                  <div
                    style="
                      display: flex;
                      gap: 5px;
                      align-items: center;
                      margin-top: 15px;
                    "
                  >
                    <!-- Add Button (only show on last row) -->
                    <button
                      v-if="index === categoryRows.length - 1"
                      type="button"
                      @click="addCategoryRow"
                      class="category-btn add-btn"
                      title="Add Category Row"
                    >
                      +
                    </button>
                    <!-- Remove Button (show if more than 1 row) -->
                    <button
                      v-if="categoryRows.length > 1"
                      type="button"
                      @click="removeCategoryRow(index)"
                      class="category-btn remove-btn"
                      title="Remove Category Row"
                    >
                      -
                    </button>
                  </div>
                </div>
              </div>

              <!-- City - Required -->
              <p class="text-white">
                {{ $t('register.city') }} <span class="text-danger">*</span>
              </p>
              <div class="position-relative mb-3">
                <multiselect
                  @input="getDistricts(formData.city_id?.id)"
                  v-model="formData.city_id"
                  :options="cities"
                  track-by="id"
                  label="name"
                  :searchable="false"
                  :close-on-select="true"
                  :show-labels="false"
                  :placeholder="$t('register.select_city')"
                  :multiple="false"
                  open-direction="bottom"
                >
                </multiselect>
              </div>

              <!-- District - Optional -->
              <p class="text-white">{{ $t('register.district') }}</p>
              <div class="position-relative mb-3">
                <multiselect
                  v-model="formData.district_id"
                  :options="districts"
                  track-by="id"
                  label="name"
                  :searchable="false"
                  :close-on-select="true"
                  :show-labels="false"
                  :placeholder="$t('register.select_district')"
                  :multiple="false"
                  open-direction="bottom"
                >
                </multiselect>
              </div>

              <!-- Submit Button -->
              <div class="mt-4">
                <button
                  type="button"
                  @click="submitForm"
                  :disabled="isLoading"
                  :class="isLoading ? 'register_btn_disabled' : 'register_btn'"
                >
                  {{
                    isLoading ? $t('register.loading') : $t('register.register')
                  }}
                </button>
              </div>
            </form>

            <!-- OTP Verification Dialog -->
            <v-dialog v-model="showDialog" max-width="400">
              <v-card>
                <div class="text-center p-5">
                  <h5>{{ $t('register.verification_code_sent') }}</h5>
                </div>
                <v-card-text dir="ltr" class="my-3">
                  <v-otp-input
                    v-model="otp"
                    :loading="isLoading"
                    label="One-Time Password"
                    length="4"
                    style="border-radius: 20px"
                  ></v-otp-input>
                </v-card-text>
                <div class="m-3">
                  {{ $t('register.resend_code_timer') }} 00:{{ timer }}
                </div>
                <v-card-actions class="pb-5">
                  <v-btn class="verify_code" @click="verifyOtp">{{
                    $t('register.verify_code')
                  }}</v-btn>
                  <v-spacer></v-spacer>
                  <v-btn
                    @click="resendOtp"
                    class="resend_btn"
                    :disabled="timer > 0"
                    >{{ $t('register.resend_code') }}</v-btn
                  >
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

export default {
  layout: 'register',
  data() {
    return {
      providerImageUrl: '',
      providerImageFile: '',
      commercialImageUrl: '',
      commercialImageFile: '',
      previousWorksUrl: [],
      previousWorksFiles: [],
      showDialog: false,
      isLoading: false,
      otpPhone: null,
      otpToken: null,
      otp: null,
      showPassword: false,
      showConfirmPassword: false,
      timer: 60,
      formData: {
        name: '',
        referral_code: '',
        description: '',
        mobile: '',
        email: '',
        password: '',
        password_confirmation: '',
        commercial_registration_number: '',
        city_id: null,
        district_id: null,
      },
      // New structure for multiple category rows
      categoryRows: [
        {
          category_id: null,
          sub_category_ids: [],
          subCategories: [],
        },
      ],
      categories: [],
      cities: [],
      districts: [],
    }
  },
  methods: {
    togglePasswordVisibility() {
      this.showPassword = !this.showPassword
    },
    toggleConfirmPasswordVisibility() {
      this.showConfirmPassword = !this.showConfirmPassword
    },

    // Get available categories for a specific row (excluding already selected ones)
    getAvailableCategories(currentRowIndex) {
      if (!this.categories) return []

      // Get all selected category IDs from other rows
      const selectedCategoryIds = this.categoryRows
        .map((row, index) => {
          // Don't exclude the current row's selection
          if (index === currentRowIndex) return null
          return row.category_id?.id
        })
        .filter((id) => id !== null && id !== undefined)

      // Return categories that are not selected in other rows
      return this.categories.filter(
        (category) => !selectedCategoryIds.includes(category.id)
      )
    },

    // Category management methods
    addCategoryRow() {
      this.categoryRows.push({
        category_id: null,
        sub_category_ids: [],
        subCategories: [],
      })
    },

    removeCategoryRow(index) {
      if (this.categoryRows.length > 1) {
        this.categoryRows.splice(index, 1)
      }
    },

    changeProviderImage(event) {
      const file = event.target.files[0]
      if (file) {
        if (
          file.name.endsWith('.png') ||
          file.name.endsWith('.jpg') ||
          file.name.endsWith('.jpeg') ||
          file.name.endsWith('.webp') ||
          file.name.endsWith('.svg') ||
          file.name.endsWith('.gif') ||
          file.name.endsWith('.jfif')
        ) {
          this.providerImageUrl = URL.createObjectURL(file)
          this.providerImageFile = file
        } else {
          this.$toast.error(this.$t('register.image_validation'))
          event.target.value = ''
        }
      }
    },

    changeCommercialImage(event) {
      const file = event.target.files[0]
      if (file) {
        if (
          file.name.endsWith('.png') ||
          file.name.endsWith('.jpg') ||
          file.name.endsWith('.jpeg') ||
          file.name.endsWith('.webp') ||
          file.name.endsWith('.svg') ||
          file.name.endsWith('.gif') ||
          file.name.endsWith('.jfif')
        ) {
          this.commercialImageUrl = URL.createObjectURL(file)
          this.commercialImageFile = file
        } else {
          this.$toast.error(this.$t('register.image_validation'))
          event.target.value = ''
        }
      }
    },

    changePreviousWorks(event) {
      let files = event.target.files
      let imageFiles = Array.from(files)
      let validImageFiles = imageFiles.filter(
        (file) =>
          file.name.endsWith('.png') ||
          file.name.endsWith('.jpg') ||
          file.name.endsWith('.jpeg') ||
          file.name.endsWith('.webp') ||
          file.name.endsWith('.svg') ||
          file.name.endsWith('.gif') ||
          file.name.endsWith('.jfif')
      )
      this.previousWorksFiles = [...this.previousWorksFiles, ...validImageFiles]
      validImageFiles.forEach((ele) => {
        this.previousWorksUrl.push({
          name: ele.name,
          url: URL.createObjectURL(ele),
        })
      })
      if (imageFiles.length !== validImageFiles.length) {
        this.$toast.error(this.$t('register.image_validation'))
        event.target.value = ''
      }
    },

    removePreviousWork(index, nameToDelete) {
      this.previousWorksUrl.splice(index, 1)
      this.previousWorksFiles = this.previousWorksFiles.filter(
        (item) => item.name !== nameToDelete
      )
    },

    async getCategories() {
      try {
        const response = await this.$axios.get(
          `landing-api/v1/categories?limit=0&page=0`
        )
        this.categories = response.data.data?.data
      } catch (error) {
        console.log('catch : ' + error)
      }
    },

    // Updated to handle specific category row
    async getSubCategories(categoryId, rowIndex) {
      this.categoryRows[rowIndex].sub_category_ids = []
      if (!categoryId) return
      try {
        const response = await this.$axios.get(
          `landing-api/v1/sub-categories?category_id=${categoryId}&page=0&limit=0`,
          {
            headers: {
              'Content-Type': 'application/json',
            },
          }
        )
        this.categoryRows[rowIndex].subCategories = response.data.data?.data
      } catch (error) {
        console.log('catch : ' + error)
      }
    },

    async getCities() {
      try {
        const response = await this.$axios.get(
          `landing-api/v1/cities?limit=0&page=0`
        )
        this.cities = response.data.data?.data
      } catch (error) {
        console.log('catch : ' + error)
      }
    },

    async getDistricts(cityId) {
      this.formData.district_id = null
      if (!cityId) return
      try {
        const response = await this.$axios.get(
          `landing-api/v1/districts?cityId=${cityId}&page=0&limit=0`
        )
        this.districts = response.data.data?.data
      } catch (error) {
        console.log('catch : ' + error)
      }
    },

    validateCategories() {
      for (let i = 0; i < this.categoryRows.length; i++) {
        const row = this.categoryRows[i]
        if (
          row.category_id &&
          (!row.sub_category_ids || row.sub_category_ids.length === 0)
        ) {
          this.$toast.error(
            this.$t('register.category_subcategory_required') ||
              `Please select at least one subcategory for the selected main category in row ${
                i + 1
              }`
          )
          return false
        }
      }
      return true
    },

    async submitForm() {
      if (!this.validateCategories()) {
        return
      }
      try {
        this.isLoading = true
        const REQUEST_DATA = new FormData()

        // Required fields
        REQUEST_DATA.append('name', this.formData.name)
        REQUEST_DATA.append('mobile', this.formData.mobile)
        REQUEST_DATA.append('email', this.formData.email)
        REQUEST_DATA.append('password', this.formData.password)
        REQUEST_DATA.append(
          'password_confirmation',
          this.formData.password_confirmation
        )
        REQUEST_DATA.append('city_id', this.formData.city_id?.id || '')

        // Optional fields
        if (this.formData.referral_code) {
          REQUEST_DATA.append('referral_code', this.formData.referral_code)
        }
        if (this.formData.description) {
          REQUEST_DATA.append('description', this.formData.description)
        }
        if (this.formData.commercial_registration_number) {
          REQUEST_DATA.append(
            'commercial_registration_number',
            this.formData.commercial_registration_number
          )
        }
        if (this.formData.district_id?.id) {
          REQUEST_DATA.append('district_id', this.formData.district_id.id)
        }

        // Images
        if (this.providerImageFile) {
          REQUEST_DATA.append('image', this.providerImageFile)
        }
        if (this.commercialImageFile) {
          REQUEST_DATA.append('commercial_image', this.commercialImageFile)
        }

        let subIndex = 0

        this.categoryRows.forEach((row, index) => {
          if (row.category_id) {
            REQUEST_DATA.append(`category_ids[${index}]`, row.category_id.id)
          }

          if (row.sub_category_ids && row.sub_category_ids.length > 0) {
            row.sub_category_ids.forEach((subCategory) => {
              REQUEST_DATA.append(
                `sub_category_ids[${subIndex}]`,
                subCategory.id
              )
              subIndex++
            })
          }
        })

        // Previous works images
        this.previousWorksFiles.forEach((file, index) => {
          REQUEST_DATA.append(`previous_works[${index}]`, file)
        })

        const response = await this.$axios.post(
          'provider-api/v1/auth/register',
          REQUEST_DATA
        )

        this.otpToken = response.data?.data?.access_token
        this.otpPhone = response.data?.data?.user?.mobile
        this.showDialog = true
        this.startTimer()
        this.isLoading = false
      } catch (error) {
        this.$toast.error(
          error.response?.data?.message || 'Registration failed'
        )
        this.isLoading = false
      }
    },

    async verifyOtp() {
      try {
        this.isLoading = true
        const REQUEST_DATA = new FormData()
        REQUEST_DATA.append('code', this.otp)
        REQUEST_DATA.append('is_changed', 0)

        await this.$axios.post(
          'provider-api/v1/auth/verify-otp',
          REQUEST_DATA,
          {
            headers: {
              Authorization: `Bearer ${this.otpToken}`,
            },
          }
        )
        this.$swal.fire({
          position: 'top',
          type: 'success',
          title: this.$t('register.verified_success'),
          text: this.$t('register.redirect'),
          showConfirmButton: false,
          timer: 5000,
        })
        setTimeout(() => {
          window.location.href =
            'https://bonian.moltaqadev.com/provider-dashboard/home?logout=true'
        }, 5000)
        this.resetForm()
        this.isLoading = false
        this.showDialog = false
      } catch (error) {
        this.$toast.error(
          error.response?.data?.message || 'Verification failed'
        )
        this.isLoading = false
        this.otp = null
      }
    },

    async resendOtp() {
      this.startTimer()
      try {
        this.isLoading = true
        const REQUEST_DATA = new FormData()
        REQUEST_DATA.append('phone', this.otpPhone)

        await this.$axios.post(
          'provider-api/v1/auth/resend-otp',
          REQUEST_DATA,
          {
            headers: {
              Authorization: `Bearer ${this.otpToken}`,
            },
          }
        )

        this.$toast.success(this.$t('register.resent_success'))
        this.isLoading = false
      } catch (error) {
        this.$toast.error(error.response?.data?.message || 'Resend failed')
        this.isLoading = false
      }
    },

    startTimer() {
      this.timer = 60
      const interval = setInterval(() => {
        if (this.timer > 0) {
          this.timer--
        } else {
          clearInterval(interval)
        }
      }, 1000)
    },

    resetForm() {
      this.formData = {
        name: '',
        referral_code: '',
        description: '',
        mobile: '',
        email: '',
        password: '',
        password_confirmation: '',
        commercial_registration_number: '',
        city_id: null,
        district_id: null,
      }
      // Reset category rows to initial state
      this.categoryRows = [
        {
          category_id: null,
          sub_category_ids: [],
          subCategories: [],
        },
      ]
      this.providerImageFile = ''
      this.providerImageUrl = ''
      this.commercialImageFile = ''
      this.commercialImageUrl = ''
      this.previousWorksFiles = []
      this.previousWorksUrl = []
      this.otpPhone = null
      this.otp = null
    },
  },

  mounted() {
    this.getCategories()
    this.getCities()
    setTimeout(() => {
      this.isLoading = false
      document.body.style.overflow = 'unset'
    }, 2000)
  },

  watch: {
    timer(newVal) {
      if (newVal === 0) {
        console.log('Timer reached zero.')
      }
    },
  },
}
</script>

<style>
.dis {
  background-color: #609191;
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
  background-color: #609191;
  color: white;
  width: 100%;
  padding: 10px;
  border-radius: 10px;
  border: none;
}

.register_btn_disabled {
  background-color: #609191;
  opacity: 0.5;
  cursor: not-allowed !important;
  color: white;
  width: 100%;
  padding: 10px;
  border-radius: 10px;
  border: none;
}

/* Category button styles */
.category-btn {
  width: 30px;
  height: 30px;
  border-radius: 50%;
  border: none;
  font-size: 20px;
  font-weight: bold;
  cursor: pointer;
  display: flex;
  align-items: center;
  text-align: center;
  justify-content: center;
  transition: all 0.3s ease;
}

.add-btn {
  background-color: #609191;
  color: white;
}

.add-btn:hover {
  background-color: #4a7373;
  transform: scale(1.1);
}

.remove-btn {
  background-color: #a81927;
  color: white;
}

.remove-btn:hover {
  background-color: #c82333;
  transform: scale(1.1);
}

.category-row {
  background-color: rgba(255, 255, 255, 0.05);
  padding: 15px;
  border-radius: 15px;
  margin-bottom: 15px;
}

.categories-section {
  margin-bottom: 20px;
}

p {
  margin-bottom: 10px !important;
}

.check p {
  margin-bottom: 0px !important;
}

.check a {
  color: white !important;
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
  background-color: #8db8b8;
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

.form-group input,
.form-group textarea {
  background-color: white;
  width: 100%;
  height: 100%;
  border: none;
  outline: none;
}

.form-group img {
  width: 20px;
  height: 20px;
}

.position-relative img,
.singleimg {
  width: 80px !important;
  height: 80px !important;
  border-radius: 20px;
  margin-top: 10px;
  margin-bottom: 10px;
}

.smallImg {
  width: 80px !important;
  height: 80px !important;
  border-radius: 20px;
  margin-top: 10px;
  margin-bottom: 10px;
}

.header_content_wrapper {
  position: sticky;
  background: var(--dark_secondary_theme_clr);
}

.verify_code {
  background-color: #609191 !important;
  color: white !important;
}

.resend_btn {
  background-color: #8db8b8 !important;
}

.store {
  margin-inline-start: 15px;
}

.x {
  cursor: pointer;
  position: absolute;
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

.register .btn {
  border-color: #609191;
  color: #609191;
}

.register .btn:hover {
  background-color: #609191;
  color: white;
}

.register .multiselect__option--highlight {
  background-color: #609191 !important;
}

.register .multiselect__tag {
  background-color: #609191 !important;
}

.register .upload {
  color: #afafb0;
  font-size: 20px;
  cursor: pointer;
}

.swal2-show {
  height: 400px !important;
  margin: auto !important;
}

.shopImg {
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  min-height: 80px;
  border-radius: 20px;
  background-color: #f8f9fa;
}

.imagesContainer {
  margin-top: 10px;
}

.register_btn:hover {
  background-color: #4a7373;
  transition: all 0.3s ease;
  transform: scale(1.01);
  font-weight: bold;
}
</style>
