<template>
  <q-page class="bg-grey-2">

    <!-- ================= HEADER ================= -->

    <q-header class="bg-white text-dark shadow-1">

      <q-toolbar class="q-px-lg">

        <div class="text-h6 text-primary text-weight-bold">
          My Shop
        </div>

        <q-space />

        <q-btn
          flat
          no-caps
          label="Categories"
          icon-right="keyboard_arrow_down"
          color="primary"
        />

        <q-btn
          flat
          round
          icon="favorite_border"
          color="primary"
          @click="showWishlist"
        />

        <q-btn
          flat
          round
          icon="shopping_cart"
          color="primary"
          @click="cartDialog = true"
        >

          <q-badge
            v-if="cartQuantity > 0"
            color="orange"
            floating
          >
            {{ cartQuantity }}
          </q-badge>

        </q-btn>

      </q-toolbar>

    </q-header>


    <!-- ================= MAIN PAGE ================= -->

    <div class="page-container">

      <div class="row q-col-gutter-md">


        <!-- ================================================= -->
        <!-- PRODUCT IMAGE GALLERY -->
        <!-- ================================================= -->

        <div class="col-12 col-md-4">

          <q-card flat class="bg-white">

            <div class="main-image-wrapper">

              <q-btn
                round
                flat
                icon="chevron_left"
                class="gallery-arrow left-arrow"
                @click="previousImage"
              />

              <q-img
                :src="selectedImage"
                height="480px"
                fit="contain"
                class="main-product-image"
                @click="openImagePreview"
              />

              <q-btn
                round
                flat
                icon="chevron_right"
                class="gallery-arrow right-arrow"
                @click="nextImage"
              />

              <div class="image-number">
                {{ currentImageIndex + 1 }}
                /
                {{ productImages.length }}
              </div>

            </div>


            <!-- THUMBNAILS -->

            <div class="row items-center q-pa-md">

              <q-btn
                flat
                round
                icon="chevron_left"
                @click="previousImage"
              />

              <div class="row col q-col-gutter-sm">

                <div
                  v-for="(image, index) in productImages"
                  :key="image"
                  class="col"
                >

                  <q-img
                    :src="image"
                    height="75px"
                    fit="contain"
                    class="thumbnail"
                    :class="{
                      'selected-thumbnail':
                        currentImageIndex === index
                    }"
                    @click="selectImage(index)"
                  />

                </div>

              </div>

              <q-btn
                flat
                round
                icon="chevron_right"
                @click="nextImage"
              />

            </div>


            <div class="text-center q-pb-md">

              <q-btn
                flat
                no-caps
                icon="zoom_in"
                label="View larger image"
                color="primary"
                @click="openImagePreview"
              />

            </div>

          </q-card>

        </div>


        <!-- ================================================= -->
        <!-- PRODUCT INFORMATION -->
        <!-- ================================================= -->

        <div class="col-12 col-md-5">

          <q-card flat class="bg-white q-pa-lg">


            <!-- TITLE -->

            <div class="product-title">

              Stylish Full Check Trouser Pant for Men -
              Multicolor Random - Joggers For Men

            </div>


            <!-- SHARE / WISHLIST -->

            <div class="row justify-end">

              <q-btn
                flat
                round
                icon="share"
                @click="shareProduct"
              />

              <q-btn
                flat
                round
                :icon="
                  wishlist
                    ? 'favorite'
                    : 'favorite_border'
                "
                color="red"
                @click="toggleWishlist"
              />

            </div>


            <!-- RATING -->

            <div class="row items-center q-mt-sm">

              <q-rating
                v-model="productRating"
                color="orange"
                size="25px"
                readonly
              />

              <span class="text-primary q-ml-sm">
                {{ ratingCount }} Ratings
              </span>

              <q-separator
                vertical
                class="q-mx-sm"
              />

              <span class="text-primary">
                2 Answered Questions
              </span>

            </div>


            <!-- BRAND -->

            <div class="q-mt-lg text-grey-7">

              Brand:

              <span class="text-primary">
                No Brand
              </span>

              <span class="q-mx-sm">
                |
              </span>

              <span class="text-primary">
                More Men from No Brand
              </span>

            </div>


            <q-separator class="q-my-lg" />


            <!-- PRICE -->

            <div class="price">
              ৳ {{ productPrice }}
            </div>

            <div class="q-mt-sm">

              <span class="old-price">
                ৳ 500
              </span>

              <span class="q-ml-md">
                -62%
              </span>

            </div>


            <q-separator class="q-my-lg" />


            <!-- COLOR -->

            <div class="row items-center">

              <div class="option-label">
                Color Family
              </div>

              <div class="text-weight-medium">
                {{ selectedColor }}
              </div>

            </div>


            <div class="row q-gutter-sm q-mt-md">

              <q-btn
                v-for="color in colors"
                :key="color"
                :label="color"
                no-caps
                flat
                class="color-btn"
                :class="{
                  'active-color':
                    selectedColor === color
                }"
                @click="selectColor(color)"
              />

            </div>


            <q-img
              :src="selectedImage"
              width="65px"
              height="65px"
              fit="contain"
              class="color-image q-mt-md"
            />


            <!-- SIZE -->

            <div class="row q-mt-xl">

              <div class="option-label">
                Size
              </div>

              <div class="size-container">

                <q-btn
                  v-for="size in sizes"
                  :key="size"
                  :label="size"
                  flat
                  no-caps
                  class="size-btn"
                  :class="{
                    'active-size':
                      selectedSize === size
                  }"
                  @click="selectSize(size)"
                />

              </div>

            </div>


            <!-- QUANTITY -->

            <div class="row items-center q-mt-xl">

              <div class="option-label">
                Quantity
              </div>

              <q-btn
                flat
                round
                icon="remove"
                :disable="quantity === 1"
                @click="decreaseQuantity"
              />

              <div class="quantity">
                {{ quantity }}
              </div>

              <q-btn
                flat
                round
                icon="add"
                @click="increaseQuantity"
              />

            </div>


            <!-- SUBTOTAL -->

            <div class="row justify-between q-mt-lg">

              <div class="text-grey-7">
                Subtotal
              </div>

              <div class="text-h6 text-orange">
                ৳ {{ subtotal }}
              </div>

            </div>


            <!-- BUTTONS -->

            <div class="row q-col-gutter-md q-mt-xl">

              <div class="col">

                <q-btn
                  class="buy-btn full-width"
                  label="Buy Now"
                  no-caps
                  @click="buyNow"
                />

              </div>

              <div class="col">

                <q-btn
                  class="cart-btn full-width"
                  label="Add to Cart"
                  icon="shopping_cart"
                  no-caps
                  @click="addToCart"
                />

              </div>

            </div>

          </q-card>

        </div>


        <!-- ================================================= -->
        <!-- DELIVERY -->
        <!-- ================================================= -->

        <div class="col-12 col-md-3">

          <q-card flat class="bg-white">


            <div class="side-section">

              <div class="side-title">
                Delivery Options
              </div>


              <div class="row q-mt-lg">

                <q-icon
                  name="location_on"
                  size="28px"
                  color="grey-7"
                />

                <div class="q-ml-md">

                  <div>
                    {{ deliveryArea }}
                  </div>

                  <div>
                    {{ deliveryAddress }}
                  </div>

                </div>

                <q-space />

                <q-btn
                  flat
                  no-caps
                  label="CHANGE"
                  color="primary"
                  @click="addressDialog = true"
                />

              </div>

            </div>


            <q-separator />


            <div class="side-section">

              <div class="row">

                <q-icon
                  name="local_shipping"
                  size="28px"
                  color="grey-7"
                />

                <div class="q-ml-md">

                  <div>
                    Standard Delivery
                  </div>

                  <div class="text-grey-6">
                    Guaranteed by 22-25 Sep
                  </div>

                </div>

                <q-space />

                ৳ 85

              </div>

            </div>


            <q-separator />


            <div class="side-section">

              <div class="row items-center">

                <q-icon
                  name="payments"
                  size="28px"
                  color="grey-7"
                />

                <span class="q-ml-md">
                  Cash on Delivery Available
                </span>

              </div>

            </div>


            <q-separator />


            <div class="side-section">

              <div class="side-title">
                Return & Warranty
              </div>


              <div class="row q-mt-lg">

                <q-icon
                  name="favorite_border"
                  size="25px"
                />

                <span class="q-ml-md">
                  Change of Mind
                </span>

              </div>


              <div class="row q-mt-lg">

                <q-icon
                  name="update"
                  size="25px"
                />

                <span class="q-ml-md">
                  14 days easy return
                </span>

              </div>


              <div class="row q-mt-lg">

                <q-icon
                  name="verified_user"
                  size="25px"
                />

                <span class="q-ml-md">
                  Warranty not available
                </span>

              </div>

            </div>

          </q-card>


          <!-- SELLER -->

          <q-card
            flat
            class="bg-white q-mt-md q-pa-md"
          >

            <div class="text-grey-7">
              Sold by
            </div>

            <div class="text-h6">
              LIFE STYLE
            </div>

            <q-separator class="q-my-md" />


            <div class="row text-center">

              <div class="col">

                <div class="text-grey-7">
                  Positive Seller
                </div>

                <div class="text-h5">
                  83%
                </div>

              </div>


              <div class="col">

                <div class="text-grey-7">
                  Ship on Time
                </div>

                <div class="text-h5">
                  100%
                </div>

              </div>

            </div>


            <q-btn
              outline
              color="primary"
              label="GO TO STORE"
              no-caps
              class="full-width q-mt-md"
            />

          </q-card>

        </div>

      </div>


      <!-- ================================================= -->
      <!-- PRODUCT DETAILS -->
      <!-- ================================================= -->

      <q-card flat class="bg-white q-mt-md">

        <div class="section-title">
          Product details of Stylish Full Check Trouser Pant
        </div>

        <q-separator />


        <!-- ALWAYS VISIBLE PART -->

        <div class="q-pa-lg">

          <ul class="product-details">

            <li>
              প্রোডাক্ট: পুরুষদের স্টাইলিশ জিন্স প্যান্ট 
            </li>

            <li>
              ম্যাটেরিয়াল: কটন + অন্যান্য
            </li>

            <li>
              কালার: ছবি অনুযায়ী
            </li>

            <li>
              এক পাশে চেইনসহ পকেট আছে।
            </li>

            <li>
              পিছনে মানিব্যাগ রাখার পকেট আছে।
            </li>

            <li>
              কোমরের ইলাস্টিক রাবার ও ফিতা আছে।
            </li>

            <li>
              মাল্টিকালার অর্ডারে যেকোনো কালার দেওয়া হয়।
            </li>

            <li>
              সাইজ বুঝতে না পারলে চ্যাট এ আমাদের সাথে
              যোগাযোগ করতে পারেন।
            </li>

            <li>
              Product Type: Trouser
            </li>

          </ul>


          <!-- EXTRA PART -->

          <div
            v-if="showDetails"
            class="extra-details"
          >

            <ul class="product-details">

              <li>
                Color: Multicolor
              </li>

              <li>
                Main Material: Mixed Cotton
              </li>

              <li>
                S - waist 26-28, long 34/35
              </li>

              <li>
                M - waist 27-29, long 38-40
              </li>

              <li>
                L - waist 29-31, long 42
              </li>

              <li>
                XL - waist 32-35, long 44
              </li>

              <li>
                XXL - waist 35-38, long 44-46
              </li>

              <li>
                3XL - waist 37-42, long 46-48
              </li>

              <li>
                #joggers for men
              </li>

            </ul>

          </div>

        </div>


        <!-- VIEW MORE / LESS -->

        <div class="text-center q-pb-lg">

          <q-btn
            outline
            color="primary"
            no-caps
            :label="
              showDetails
                ? 'VIEW LESS'
                : 'VIEW MORE'
            "
            @click="
              showDetails = !showDetails
            "
          />

        </div>

      </q-card>


      <!-- ================================================= -->
      <!-- SPECIFICATIONS -->
      <!-- ================================================= -->

      <q-card flat class="bg-white q-mt-md">

        <div class="section-title">
          Specifications of Product
        </div>

        <q-separator />


        <div class="row q-pa-lg">

          <div class="col-12 col-md-6">

            <div class="text-grey-7">
              Brand
            </div>

            <div>
              No Brand
            </div>


            <div class="text-grey-7 q-mt-lg">
              Main Material
            </div>

            <div>
              Cotton
            </div>

          </div>


          <div class="col-12 col-md-6">

            <div class="text-grey-7">
              SKU
            </div>

            <div>
              266123990_BD
            </div>


            <div class="text-grey-7 q-mt-lg">
              What's in the box
            </div>

            <div>
              1 Piece Multicolor Random Trouser For Men
            </div>

          </div>

        </div>

      </q-card>


      <!-- ================================================= -->
      <!-- RATINGS -->
      <!-- ================================================= -->

      <q-card flat class="bg-white q-mt-md">

        <div class="section-title">
          Ratings & Reviews
        </div>

        <q-separator />


        <div class="row q-pa-xl">

          <!-- OVERALL RATING -->

          <div class="col-12 col-md-4 text-center">

            <div class="big-rating">
              4.1
              <span>/5</span>
            </div>

            <q-rating
              :model-value="4"
              color="orange"
              size="35px"
              readonly
            />

            <div class="text-grey-7">
              96 Ratings
            </div>

          </div>


          <!-- RATING BREAKDOWN -->

          <div class="col-12 col-md-6">

            <div
              v-for="item in ratingBreakdown"
              :key="item.star"
              class="row items-center q-mb-sm"
            >

              <q-rating
                :model-value="item.star"
                color="orange"
                size="20px"
                readonly
              />

              <q-linear-progress
                :value="item.value"
                color="orange"
                track-color="grey-3"
                class="rating-bar q-ml-md"
              />

              <span class="q-ml-md">
                {{ item.count }}
              </span>

            </div>

          </div>

        </div>


        <q-separator />


        <!-- REVIEW HEADER -->

        <div class="row items-center q-pa-md">

          <div class="text-h6">
            Product Reviews
          </div>

          <q-space />


          <q-select
            v-model="reviewSort"
            :options="reviewSortOptions"
            dense
            outlined
            label="Sort"
            style="width: 170px"
          />


          <q-select
            v-model="reviewFilter"
            :options="reviewFilterOptions"
            dense
            outlined
            label="Filter"
            class="q-ml-sm"
            style="width: 150px"
          />

        </div>


        <!-- REVIEWS -->

        <div
          v-for="review in filteredReviews"
          :key="review.id"
          class="review q-pa-lg"
        >

          <q-rating
            :model-value="review.rating"
            color="orange"
            readonly
          />

          <div class="text-grey-7">
            {{ review.name }}
          </div>

          <div class="q-mt-md text-body1">
            {{ review.comment }}
          </div>

          <div class="text-grey-6 q-mt-md">
            Helpful: {{ review.helpful }}
          </div>

        </div>


        <div
          v-if="filteredReviews.length === 0"
          class="text-center text-grey-6 q-pa-xl"
        >
          No reviews found.
        </div>


        <!-- WRITE REVIEW -->

        <q-separator />

        <div class="q-pa-lg">

          <div class="text-h6 q-mb-md">
            Rate this product
          </div>

          <q-rating
            v-model="userRating"
            color="orange"
            size="32px"
          />

          <q-input
            v-model="userReview"
            outlined
            type="textarea"
            label="Write your review"
            class="q-mt-md"
          />

          <q-btn
            color="primary"
            label="Submit Review"
            no-caps
            class="q-mt-md"
            @click="submitReview"
          />

        </div>

      </q-card>


      <!-- ================================================= -->
      <!-- QUESTIONS -->
      <!-- ================================================= -->

      <q-card flat class="bg-white q-mt-md">

        <div class="section-title">
          Questions about this product ({{ questions.length }})
        </div>

        <q-separator />


        <div class="q-pa-lg">

          <div class="text-primary">

            Login or Register

            <span class="text-dark">
              to ask questions
            </span>

          </div>


          <div class="text-h6 q-mt-lg">
            Other questions answered by LIFE STYLE
          </div>


          <div
            v-for="question in questions"
            :key="question.id"
            class="question q-mt-lg"
          >

            <div class="question-icon">
              Q
            </div>


            <div class="full-width">

              <div class="question-text">
                {{ question.question }}
              </div>

              <div class="text-grey-6">
                {{ question.date }}
              </div>


              <div class="answer q-mt-md">

                <span class="answer-icon">
                  A
                </span>

                {{ question.answer }}

              </div>

            </div>

          </div>


          <!-- ASK QUESTION -->

          <q-input
            v-model="newQuestion"
            outlined
            label="Ask a question"
            class="q-mt-xl"
          />

          <q-btn
            color="primary"
            label="Submit Question"
            no-caps
            class="q-mt-md"
            @click="submitQuestion"
          />

        </div>

      </q-card>


      <!-- ================================================= -->
      <!-- FOOTER -->
      <!-- ================================================= -->

      <div class="footer q-pa-xl q-mt-md">

        <div class="text-h6">
          My Shop
        </div>

        <div class="text-grey-7 q-mt-sm">
          Quality products at affordable prices.
        </div>

      </div>

    </div>


    <!-- ================================================= -->
    <!-- IMAGE PREVIEW -->
    <!-- ================================================= -->

    <q-dialog
      v-model="imagePreview"
      maximized
      transition-show="fade"
      transition-hide="fade"
    >

      <q-card class="preview-card">

        <q-btn
          round
          flat
          icon="close"
          color="white"
          class="preview-close"
          @click="imagePreview = false"
        />


        <q-btn
          round
          flat
          icon="chevron_left"
          color="white"
          size="28px"
          class="preview-left"
          @click="previousImage"
        />


        <q-img
          :src="selectedImage"
          fit="contain"
          class="preview-image"
        />


        <q-btn
          round
          flat
          icon="chevron_right"
          color="white"
          size="28px"
          class="preview-right"
          @click="nextImage"
        />


        <div class="preview-count">
          {{ currentImageIndex + 1 }}
          /
          {{ productImages.length }}
        </div>

      </q-card>

    </q-dialog>


    <!-- ================================================= -->
    <!-- CART -->
    <!-- ================================================= -->

    <q-dialog v-model="cartDialog">

      <q-card class="cart-dialog">

        <q-card-section>

          <div class="text-h6">
            Shopping Cart
          </div>

        </q-card-section>


        <q-separator />


        <q-card-section>

          <div
            v-if="cartQuantity > 0"
            class="row items-center"
          >

            <q-img
              :src="selectedImage"
              width="90px"
              height="90px"
              fit="contain"
            />

            <div class="q-ml-md">

              <div class="text-weight-bold">
                Stylish Full Check Trouser
              </div>

              <div class="text-grey-7">
                Size: {{ selectedSize }}
              </div>

              <div class="text-grey-7">
                Color: {{ selectedColor }}
              </div>

              <div>
                Quantity: {{ cartQuantity }}
              </div>

              <div class="text-orange text-h6">
                ৳ {{ cartTotal }}
              </div>

            </div>

          </div>


          <div
            v-else
            class="text-center text-grey-6 q-pa-lg"
          >
            Your cart is empty.
          </div>

        </q-card-section>


        <q-separator />


        <q-card-actions align="right">

          <q-btn
            flat
            label="Close"
            v-close-popup
          />

          <q-btn
            v-if="cartQuantity > 0"
            flat
            color="negative"
            label="Remove"
            @click="removeFromCart"
          />

          <q-btn
            v-if="cartQuantity > 0"
            color="orange"
            label="Checkout"
            no-caps
            @click="openCheckoutFromCart"
          />

        </q-card-actions>

      </q-card>

    </q-dialog>


    <!-- ================================================= -->
    <!-- CHECKOUT -->
    <!-- ================================================= -->

    <q-dialog
      v-model="checkoutDialog"
      persistent
    >

      <q-card class="checkout-dialog">

        <q-card-section>

          <div class="text-h6">
            Checkout
          </div>

          <div class="text-grey-7">
            Complete your order information
          </div>

        </q-card-section>


        <q-separator />


        <q-form @submit="placeOrder">

          <q-card-section>


            <div class="text-subtitle1 text-weight-bold">
              Customer Information
            </div>


            <q-input
              v-model="checkout.name"
              outlined
              label="Full Name"
              :rules="[
                value =>
                  !!value ||
                  'Name is required'
              ]"
              class="q-mt-md"
            />


            <q-input
              v-model="checkout.phone"
              outlined
              label="Phone Number"
              type="tel"
              :rules="[
                value =>
                  !!value ||
                  'Phone is required'
              ]"
              class="q-mt-md"
            />


            <q-input
              v-model="checkout.address"
              outlined
              label="Delivery Address"
              type="textarea"
              :rules="[
                value =>
                  !!value ||
                  'Address is required'
              ]"
              class="q-mt-md"
            />


            <div class="text-subtitle1 text-weight-bold q-mt-lg">
              Delivery Method
            </div>


            <q-option-group
              v-model="checkout.delivery"
              :options="deliveryOptions"
              color="primary"
              class="q-mt-sm"
            />


            <div class="text-subtitle1 text-weight-bold q-mt-lg">
              Payment Method
            </div>


            <q-option-group
              v-model="checkout.payment"
              :options="paymentOptions"
              color="orange"
              class="q-mt-sm"
            />


            <!-- ORDER SUMMARY -->

            <q-card
              flat
              bordered
              class="q-mt-lg bg-grey-1"
            >

              <q-card-section>

                <div class="text-subtitle1 text-weight-bold">
                  Order Summary
                </div>


                <div class="row justify-between q-mt-md">

                  <span>
                    Product
                  </span>

                  <span>
                    ৳ {{ productPrice }}
                  </span>

                </div>


                <div class="row justify-between q-mt-sm">

                  <span>
                    Quantity
                  </span>

                  <span>
                    {{ quantity }}
                  </span>

                </div>


                <div class="row justify-between q-mt-sm">

                  <span>
                    Delivery
                  </span>

                  <span>
                    ৳ {{ deliveryCharge }}
                  </span>

                </div>


                <q-separator class="q-my-md" />


                <div class="row justify-between">

                  <span class="text-weight-bold">
                    Total
                  </span>

                  <span class="text-h6 text-orange">
                    ৳ {{ checkoutTotal }}
                  </span>

                </div>

              </q-card-section>

            </q-card>

          </q-card-section>


          <q-separator />


          <q-card-actions align="right">

            <q-btn
              flat
              label="Cancel"
              color="grey"
              type="button"
              @click="
                checkoutDialog = false
              "
            />

            <q-btn
              unelevated
              label="Place Order"
              color="orange"
              type="submit"
            />

          </q-card-actions>

        </q-form>

      </q-card>

    </q-dialog>


    <!-- ================================================= -->
    <!-- CHANGE ADDRESS -->
    <!-- ================================================= -->

    <q-dialog v-model="addressDialog">

      <q-card class="address-dialog">

        <q-card-section>

          <div class="text-h6">
            Change Delivery Address
          </div>

        </q-card-section>


        <q-card-section>

          <q-input
            v-model="tempAddress"
            outlined
            label="Address"
          />

        </q-card-section>


        <q-card-actions align="right">

          <q-btn
            flat
            label="Cancel"
            v-close-popup
          />

          <q-btn
            color="primary"
            label="Save"
            @click="saveAddress"
          />

        </q-card-actions>

      </q-card>

    </q-dialog>

  </q-page>
</template>


<script setup>

import {
  ref,
  computed,
  onMounted,
  onBeforeUnmount
} from 'vue'

import { useQuasar } from 'quasar'

const $q = useQuasar()


/* ================================================= */
/* PRODUCT IMAGES */
/* ================================================= */

const productImages = [

  '/paint01.jpg',

  '/paint01.jpg',

  '/paint01.jpg',

  '/paint01.jpg',

  '/paint01.jpg'

]


const productPrice = 189


const currentImageIndex = ref(0)

const selectedImage =
  ref(productImages[0])

const imagePreview = ref(false)


/* ================================================= */
/* IMAGE FUNCTIONS */
/* ================================================= */

const selectImage = (index) => {

  currentImageIndex.value = index

  selectedImage.value =
    productImages[index]

}


const nextImage = () => {

  currentImageIndex.value =
    (
      currentImageIndex.value + 1
    ) %
    productImages.length

  selectedImage.value =
    productImages[
      currentImageIndex.value
    ]

}


const previousImage = () => {

  currentImageIndex.value =
    (
      currentImageIndex.value -
      1 +
      productImages.length
    ) %
    productImages.length

  selectedImage.value =
    productImages[
      currentImageIndex.value
    ]

}


const openImagePreview = () => {

  imagePreview.value = true

}


/* ================================================= */
/* KEYBOARD */
/* ================================================= */

const handleKeyboard = (event) => {

  if (!imagePreview.value) {
    return
  }

  if (event.key === 'ArrowRight') {

    nextImage()

  }

  if (event.key === 'ArrowLeft') {

    previousImage()

  }

  if (event.key === 'Escape') {

    imagePreview.value = false

  }

}


onMounted(() => {

  window.addEventListener(
    'keydown',
    handleKeyboard
  )

})


onBeforeUnmount(() => {

  window.removeEventListener(
    'keydown',
    handleKeyboard
  )

})


/* ================================================= */
/* COLOR */
/* ================================================= */

const colors = [
  'Multicolor'
]


const selectedColor =
  ref('Multicolor')


const selectColor = (color) => {

  selectedColor.value = color

}


/* ================================================= */
/* SIZE */
/* ================================================= */

const sizes = [

  'S',

  '3XL',

  'M',

  'L',

  'XL',

  'XXL',

  'XS'

]


const selectedSize = ref('M')


const selectSize = (size) => {

  selectedSize.value = size

}


/* ================================================= */
/* QUANTITY */
/* ================================================= */

const quantity = ref(1)


const increaseQuantity = () => {

  quantity.value++

}


const decreaseQuantity = () => {

  if (quantity.value > 1) {

    quantity.value--

  }

}


const subtotal = computed(() => {

  return (
    productPrice *
    quantity.value
  )

})


/* ================================================= */
/* CART */
/* ================================================= */

const cartQuantity = ref(0)

const cartDialog = ref(false)


const cartTotal = computed(() => {

  return (
    productPrice *
    cartQuantity.value
  )

})


const addToCart = () => {

  cartQuantity.value +=
    quantity.value

  cartDialog.value = true

  $q.notify({

    type: 'positive',

    message:
      'Product added to cart',

    position: 'top'

  })

}


const removeFromCart = () => {

  cartQuantity.value = 0

  $q.notify({

    type: 'info',

    message:
      'Product removed from cart'

  })

}


/* ================================================= */
/* CHECKOUT */
/* ================================================= */

const checkoutDialog = ref(false)


const openCheckoutFromCart = () => {

  cartDialog.value = false

  checkoutDialog.value = true

}


const buyNow = () => {

  checkoutDialog.value = true

}


/* ================================================= */
/* CHECKOUT DATA */
/* ================================================= */

const checkout = ref({

  name: '',

  phone: '',

  address: '',

  delivery: 'standard',

  payment: 'cod'

})


const deliveryOptions = [

  {

    label:
      'Standard Delivery - ৳ 85',

    value:
      'standard'

  },

  {

    label:
      'Express Delivery - ৳ 150',

    value:
      'express'

  }

]


const paymentOptions = [

  {

    label:
      'Cash on Delivery',

    value:
      'cod'

  },

  {

    label:
      'bKash',

    value:
      'bkash'

  },

  {

    label:
      'Card Payment',

    value:
      'card'

  }

]


const deliveryCharge =
  computed(() => {

    return checkout.value.delivery ===
      'express'
      ? 150
      : 85

  })


const checkoutTotal =
  computed(() => {

    return (
      productPrice *
      quantity.value
    ) +
    deliveryCharge.value

  })


const placeOrder = () => {

  checkoutDialog.value = false


  $q.dialog({

    title:
      'Order Confirmed',

    message:
      `Thank you ${checkout.value.name}! Your order has been placed successfully. Total: ৳ ${checkoutTotal.value}`,

    ok: {

      label: 'Done',

      color: 'primary'

    }

  })

}


/* ================================================= */
/* DELIVERY ADDRESS */
/* ================================================= */

const deliveryArea = ref(
  'Dhaka, Dhaka North, Banani'
)


const deliveryAddress = ref(
  'Road No. 12 - 19'
)


const addressDialog = ref(false)

const tempAddress = ref('')


const saveAddress = () => {

  if (
    !tempAddress.value.trim()
  ) {

    $q.notify({

      type: 'warning',

      message:
        'Please enter an address'

    })

    return

  }


  deliveryAddress.value =
    tempAddress.value

  addressDialog.value = false

  $q.notify({

    type: 'positive',

    message:
      'Delivery address updated'

  })

}


/* ================================================= */
/* WISHLIST */
/* ================================================= */

const wishlist = ref(false)


const toggleWishlist = () => {

  wishlist.value =
    !wishlist.value


  $q.notify({

    type:
      wishlist.value
        ? 'positive'
        : 'info',

    message:
      wishlist.value
        ? 'Added to wishlist'
        : 'Removed from wishlist'

  })

}


const showWishlist = () => {

  $q.notify({

    type:
      wishlist.value
        ? 'positive'
        : 'info',

    message:
      wishlist.value
        ? 'Product is in your wishlist'
        : 'Wishlist is empty'

  })

}


/* ================================================= */
/* SHARE */
/* ================================================= */

const shareProduct = async () => {

  if (navigator.share) {

    await navigator.share({

      title:
        'Stylish Full Check Trouser',

      text:
        'Check this product'

    })

  } else {

    $q.notify({

      type: 'info',

      message:
        'Share is not supported in this browser'

    })

  }

}


/* ================================================= */
/* PRODUCT DETAILS */
/* ================================================= */

const showDetails = ref(false)


/* ================================================= */
/* RATING */
/* ================================================= */

const productRating = ref(5)

const ratingCount = ref(96)

const userRating = ref(0)

const userReview = ref('')


/* ================================================= */
/* REVIEWS */
/* ================================================= */

const reviews = ref([

  {

    id: 1,

    name:
      'Ahnaf A.',

    rating: 5,

    comment:
      'Got the correct size and the quality is good for the price.',

    helpful: 0

  },

  {

    id: 2,

    name:
      'Nazrul Farazi',

    rating: 4,

    comment:
      'packing was good but stitching quality is not good',

    helpful: 0

  },

  {

    id: 3,

    name:
      'Customer',

    rating: 5,

    comment:
      'ডেলিভারি দ্রুত এসেছে ধন্যবাদ',

    helpful: 0

  }

])


const submitReview = () => {

  if (!userRating.value) {

    $q.notify({

      type: 'warning',

      message:
        'Please select a rating'

    })

    return

  }


  if (
    !userReview.value.trim()
  ) {

    $q.notify({

      type: 'warning',

      message:
        'Please write a review'

    })

    return

  }


  reviews.value.unshift({

    id: Date.now(),

    name: 'You',

    rating:
      userRating.value,

    comment:
      userReview.value,

    helpful: 0

  })


  userRating.value = 0

  userReview.value = ''


  $q.notify({

    type: 'positive',

    message:
      'Your review has been added'

  })

}


/* ================================================= */
/* REVIEW SORT / FILTER */
/* ================================================= */

const reviewSortOptions = [

  'Relevance',

  'Newest',

  'Highest Rating',

  'Lowest Rating'

]


const reviewFilterOptions = [

  'All stars',

  '5 stars',

  '4 stars',

  '3 stars',

  '2 stars',

  '1 star'

]


const reviewSort =
  ref('Relevance')


const reviewFilter =
  ref('All stars')


const filteredReviews =
  computed(() => {

    let result =
      [...reviews.value]


    if (
      reviewFilter.value !==
      'All stars'
    ) {

      const star =
        Number(
          reviewFilter.value.charAt(0)
        )


      result =
        result.filter(
          review =>
            review.rating === star
        )

    }


    if (
      reviewSort.value ===
      'Highest Rating'
    ) {

      result.sort(
        (a, b) =>
          b.rating - a.rating
      )

    }


    if (
      reviewSort.value ===
      'Lowest Rating'
    ) {

      result.sort(
        (a, b) =>
          a.rating - b.rating
      )

    }


    if (
      reviewSort.value ===
      'Newest'
    ) {

      result.sort(
        (a, b) =>
          b.id - a.id
      )

    }


    return result

  })


/* ================================================= */
/* RATING BREAKDOWN */
/* ================================================= */

const ratingBreakdown = [

  {

    star: 5,

    value: 0.65,

    count: 56

  },

  {

    star: 4,

    value: 0.20,

    count: 18

  },

  {

    star: 3,

    value: 0.08,

    count: 6

  },

  {

    star: 2,

    value: 0.06,

    count: 5

  },

  {

    star: 1,

    value: 0.12,

    count: 11

  }

]


/* ================================================= */
/* QUESTIONS */
/* ================================================= */

const questions = ref([

  {

    id: 1,

    question:
      '10 years er cheler jonno hobe???',

    date:
      'Jannatul ferdows - 19 Nov 2022',

    answer:
      'komorer size 26-28 hole M size nite parben'

  },

  {

    id: 2,

    question:
      'লম্বা কত হবে',

    date:
      '1****1 - 06 Oct 2022',

    answer:
      'Multicolor Random dewa hoy'

  }

])


const newQuestion = ref('')


const submitQuestion = () => {

  if (
    !newQuestion.value.trim()
  ) {

    $q.notify({

      type: 'warning',

      message:
        'Please write your question'

    })

    return

  }


  questions.value.push({

    id: Date.now(),

    question:
      newQuestion.value,

    date:
      'Just now',

    answer:
      'Your question has been received.'

  })


  newQuestion.value = ''


  $q.notify({

    type: 'positive',

    message:
      'Question submitted'

  })

}

</script>


<style scoped>

/* ================================================= */
/* PAGE */
/* ================================================= */

.page-container {

  max-width: 1500px;

  margin: auto;

  padding: 16px;

}


/* ================================================= */
/* GALLERY */
/* ================================================= */

.main-image-wrapper {

  position: relative;

  background: white;

}


.main-product-image {

  cursor: zoom-in;

}


.gallery-arrow {

  position: absolute;

  top: 50%;

  transform:
    translateY(-50%);

  z-index: 5;

  background:
    rgba(255, 255, 255, 0.9);

}


.left-arrow {

  left: 8px;

}


.right-arrow {

  right: 8px;

}


.image-number {

  position: absolute;

  right: 12px;

  bottom: 12px;

  background:
    rgba(0, 0, 0, 0.65);

  color: white;

  padding:
    5px 10px;

  border-radius: 4px;

  z-index: 5;

}


.thumbnail {

  border:
    1px solid #ddd;

  cursor: pointer;

  background: white;

}


.selected-thumbnail {

  border:
    2px solid #ff6b00;

}


/* ================================================= */
/* IMAGE PREVIEW */
/* ================================================= */

.preview-card {

  background:
    rgba(0, 0, 0, 0.96);

  width: 100%;

  height: 100%;

  position: relative;

  display: flex;

  align-items: center;

  justify-content: center;

}


.preview-image {

  width: 90%;

  height: 90%;

}


.preview-close {

  position: absolute;

  right: 20px;

  top: 20px;

  z-index: 10;

}


.preview-left {

  position: absolute;

  left: 25px;

  top: 50%;

  transform:
    translateY(-50%);

  z-index: 10;

}


.preview-right {

  position: absolute;

  right: 25px;

  top: 50%;

  transform:
    translateY(-50%);

  z-index: 10;

}


.preview-count {

  position: absolute;

  bottom: 25px;

  color: white;

  font-size: 18px;

}


/* ================================================= */
/* PRODUCT */
/* ================================================= */

.product-title {

  font-size: 28px;

  line-height: 1.3;

}


.price {

  color: #f57224;

  font-size: 42px;

}


.old-price {

  color: #999;

  text-decoration:
    line-through;

}


.option-label {

  width: 120px;

  color: #666;

}


.color-btn {

  border:
    1px solid #ddd;

}


.active-color {

  color: #ff6b00;

  border:
    2px solid #ff6b00;

}


.color-image {

  border:
    2px solid #ff6b00;

}


.size-container {

  display: flex;

  flex-wrap: wrap;

  gap: 8px;

}


.size-btn {

  min-width: 65px;

  border:
    1px solid #ddd;

}


.active-size {

  color: #ff6b00;

  border:
    2px solid #ff6b00;

}


.quantity {

  width: 45px;

  text-align: center;

  font-size: 18px;

}


.buy-btn {

  background:
    #2bb8df;

  color: white;

  height: 55px;

}


.cart-btn {

  background:
    #f57224;

  color: white;

  height: 55px;

}


/* ================================================= */
/* DELIVERY */
/* ================================================= */

.side-section {

  padding: 20px;

}


.side-title {

  color: #667085;

  font-weight: 600;

}


/* ================================================= */
/* PRODUCT DETAILS */
/* ================================================= */

.product-details {

  margin: 0;

  padding-left: 22px;

  line-height: 1.8;

  font-size: 16px;

}


.product-details li {

  margin-bottom: 3px;

}


.extra-details {

  margin-top: 12px;

  padding-top: 12px;

  border-top:
    1px solid #eeeeee;

}


/* ================================================= */
/* SECTION */
/* ================================================= */

.section-title {

  padding: 20px;

  font-size: 21px;

  font-weight: 600;

}


/* ================================================= */
/* RATING */
/* ================================================= */

.big-rating {

  font-size: 60px;

}


.big-rating span {

  color: #999;

  font-size: 25px;

}


.rating-bar {

  width: 280px;

}


/* ================================================= */
/* REVIEWS */
/* ================================================= */

.review {

  border-top:
    1px solid #eee;

}


/* ================================================= */
/* QUESTIONS */
/* ================================================= */

.question {

  display: flex;

  gap: 18px;

  border-bottom:
    1px solid #eee;

  padding-bottom: 20px;

}


.question-icon {

  min-width: 30px;

  height: 30px;

  background:
    #20a5c7;

  color: white;

  display: flex;

  align-items: center;

  justify-content: center;

}


.question-text {

  font-size: 18px;

}


.answer {

  font-size: 16px;

}


.answer-icon {

  background: #aaa;

  color: white;

  padding:
    4px 8px;

  margin-right: 8px;

}


/* ================================================= */
/* CART */
/* ================================================= */

.cart-dialog {

  width: 550px;

  max-width: 92vw;

}


/* ================================================= */
/* CHECKOUT */
/* ================================================= */

.checkout-dialog {

  width: 650px;

  max-width: 95vw;

}


/* ================================================= */
/* ADDRESS */
/* ================================================= */

.address-dialog {

  width: 450px;

  max-width: 90vw;

}


/* ================================================= */
/* FOOTER */
/* ================================================= */

.footer {

  background: white;

}


/* ================================================= */
/* MOBILE */
/* ================================================= */

@media (max-width: 700px) {

  .page-container {

    padding: 8px;

  }


  .product-title {

    font-size: 21px;

  }


  .price {

    font-size: 34px;

  }


  .rating-bar {

    width: 160px;

  }


  .preview-left {

    left: 5px;

  }


  .preview-right {

    right: 5px;

  }


  .preview-image {

    width: 95%;

  }


  .section-title {

    font-size: 18px;

  }

}

</style>