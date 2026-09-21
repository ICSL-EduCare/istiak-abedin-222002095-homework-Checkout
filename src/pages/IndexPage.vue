<template>
  <q-page class="bg-white" style="min-height: 100vh;">

    <!-- ==================================================
         TOP HEADER
    =================================================== -->
    <div
      class="row items-center no-wrap"
      style="
        width: 100%;
        min-height: 88px;
        padding: 12px 4%;
        gap: 24px;
        background: white;
      "
    >

      <!-- LOGO -->
      <div style="min-width: 190px;">
        <q-img
          src="https://upload.wikimedia.org/wikipedia/commons/a/a1/AliExpress_logo_2024.png"
          width="180px"
          fit="contain"
          no-spinner
        />
      </div>


      <!-- SEARCH -->
      <div style="flex: 1; max-width: 750px;">

        <q-input
          v-model="search"
          outlined
          rounded
          dense
          placeholder="1 Cent Items"
        >
          <template #append>

            <q-icon
              name="center_focus_strong"
              size="23px"
              class="q-mr-sm cursor-pointer"
            />

            <q-btn
              round
              dense
              unelevated
              color="dark"
              icon="search"
            />

          </template>
        </q-input>

      </div>


      <!-- DOWNLOAD APP -->
      <div
        class="row items-center no-wrap"
        style="gap: 8px; white-space: nowrap;"
      >

        <q-icon
          name="qr_code_2"
          size="31px"
        />

        <div>
          <div style="font-size: 11px;">
            Download the
          </div>

          <div style="font-size: 13px;">
            AliExpress app
          </div>
        </div>

      </div>


      <!-- LANGUAGE -->
      <q-btn-dropdown
        flat
        dense
        no-caps
      >

        <template #label>

          <div class="row items-center no-wrap">

            <span style="font-size: 23px;">
              🇧🇩
            </span>

            <div class="q-ml-sm text-left">

              <div style="font-size: 11px;">
                EN/
              </div>

              <div class="text-weight-bold">
                BDT
              </div>

            </div>

          </div>

        </template>


        <q-list style="min-width: 190px;">

          <q-item clickable v-close-popup>
            <q-item-section>
              English / BDT
            </q-item-section>
          </q-item>

          <q-item clickable v-close-popup>
            <q-item-section>
              English / USD
            </q-item-section>
          </q-item>

          <q-item clickable v-close-popup>
            <q-item-section>
              বাংলা / BDT
            </q-item-section>
          </q-item>

        </q-list>

      </q-btn-dropdown>


      <!-- ==================================================
           ACCOUNT + POPUP
      =================================================== -->
      <q-btn
        flat
        no-caps
        padding="4px 8px"
        style="color: #111;"
      >

        <div
          class="row items-center no-wrap"
          style="gap: 8px; white-space: nowrap;"
        >

          <q-icon
            name="person_outline"
            size="32px"
          />

          <div style="text-align: left;">

            <div style="font-size: 11px;">
              Welcome
            </div>

            <div
              class="text-weight-bold"
              style="font-size: 13px;"
            >
              Sign in / Register
            </div>

          </div>

        </div>


        <q-menu
          anchor="bottom middle"
          self="top middle"
          :offset="[0, 10]"
        >

          <q-card
            style="
              width: 270px;
              border-radius: 18px;
              padding: 14px;
              box-shadow: 0 6px 25px rgba(0,0,0,0.18);
            "
          >

            <q-btn
              unelevated
              rounded
              color="dark"
              label="Sign in"
              no-caps
              class="full-width"
            />

            <q-btn
              flat
              no-caps
              label="Register"
              class="full-width"
              style="font-size: 12px; color: #666;"
            />

            <q-separator class="q-mb-sm" />


            <q-item clickable dense>
              <q-item-section avatar>
                <q-icon name="receipt_long" size="18px" />
              </q-item-section>

              <q-item-section>
                My Orders
              </q-item-section>
            </q-item>


            <q-item clickable dense>
              <q-item-section avatar>
                <q-icon name="paid" size="18px" />
              </q-item-section>

              <q-item-section>
                My Coins
              </q-item-section>
            </q-item>


            <q-item clickable dense>
              <q-item-section avatar>
                <q-icon name="mail_outline" size="18px" />
              </q-item-section>

              <q-item-section>
                Message Center
              </q-item-section>
            </q-item>


            <q-item clickable dense>
              <q-item-section avatar>
                <q-icon name="credit_card" size="18px" />
              </q-item-section>

              <q-item-section>
                Payment
              </q-item-section>
            </q-item>


            <q-item clickable dense>
              <q-item-section avatar>
                <q-icon name="favorite_border" size="18px" />
              </q-item-section>

              <q-item-section>
                Wish List
              </q-item-section>
            </q-item>


            <q-item clickable dense>
              <q-item-section avatar>
                <q-icon name="local_offer" size="18px" />
              </q-item-section>

              <q-item-section>
                My Coupons
              </q-item-section>
            </q-item>


            <q-separator class="q-my-sm" />


            <q-item clickable dense>
              <q-item-section>Settings</q-item-section>
            </q-item>

            <q-item clickable dense>
              <q-item-section>
                AliExpress Business
              </q-item-section>
            </q-item>

            <q-item clickable dense>
              <q-item-section>DS Center</q-item-section>
            </q-item>

            <q-item clickable dense>
              <q-item-section>Seller Log In</q-item-section>
            </q-item>

            <q-item clickable dense>
              <q-item-section>
                Return & refund policy
              </q-item-section>
            </q-item>

            <q-item clickable dense>
              <q-item-section>
                Help Center
              </q-item-section>
            </q-item>

          </q-card>

        </q-menu>

      </q-btn>


      <!-- CART -->
      <div
        class="row items-center no-wrap"
        style="gap: 8px;"
      >

        <div style="position: relative;">

          <q-icon
            name="shopping_cart"
            size="34px"
          />

          <q-badge
            floating
            rounded
            color="dark"
            label="0"
          />

        </div>

        <div class="text-weight-bold">
          Cart
        </div>

      </div>

    </div>



    <!-- ==================================================
         NAVBAR
    =================================================== -->
    <div
      class="row items-center no-wrap"
      style="
        width: 100%;
        min-height: 65px;
        padding: 0 4%;
        gap: 14px;
        overflow-x: auto;
      "
    >

      <q-btn-dropdown
        unelevated
        rounded
        no-caps
        color="grey-2"
        text-color="black"
        icon="menu"
        label="All Categories"
        style="min-width: 280px;"
      >

        <q-list style="min-width: 310px;">

          <q-item
            v-for="item in categories"
            :key="item.name"
            clickable
            v-close-popup
          >

            <q-item-section avatar>
              <q-icon :name="item.icon" />
            </q-item-section>

            <q-item-section>
              {{ item.name }}
            </q-item-section>

          </q-item>

        </q-list>

      </q-btn-dropdown>


      <q-btn
        flat
        no-caps
        color="negative"
        label="SuperDeals"
        class="text-weight-bold"
      />

      <q-btn
        flat
        no-caps
        label="AliExpress Business"
      />

      <q-btn
        flat
        no-caps
        label="Automotive"
      />

      <q-btn
        flat
        no-caps
        label="Appliances"
      />

      <q-btn
        flat
        no-caps
        label="Women's Clothing"
      />

      <q-btn
        flat
        no-caps
        label="Men's Clothing"
      />

      <q-btn
        flat
        no-caps
        label="Toys & Games"
      />


      <q-btn-dropdown
        flat
        no-caps
        label="More"
      >

        <q-list>

          <q-item clickable v-close-popup>
            <q-item-section>Shoes</q-item-section>
          </q-item>

          <q-item clickable v-close-popup>
            <q-item-section>Electronics</q-item-section>
          </q-item>

          <q-item clickable v-close-popup>
            <q-item-section>Jewelry</q-item-section>
          </q-item>

        </q-list>

      </q-btn-dropdown>

    </div>



    <!-- ==================================================
         MAIN CAROUSEL
    =================================================== -->
    <q-carousel
      v-model="slide"
      animated
      arrows
      navigation
      infinite
      :autoplay="4000"
      swipeable
      style="
        width: 100%;
        height: 360px;
        background: #ffe0a3;
      "
    >

      <q-carousel-slide
        v-for="item in saleSlides"
        :key="item.name"
        :name="item.name"
        class="q-pa-none"
      >

        <div
          style="
            width: 100%;
            height: 100%;
            padding: 32px 8%;
            background: #ffe0a3;
          "
        >

          <!-- TITLE -->
          <div
            class="row items-center"
            style="margin-bottom: 20px;"
          >

            <span
              style="
                font-family: Georgia, serif;
                font-style: italic;
                font-size: 48px;
                font-weight: bold;
                color: #b94d00;
              "
            >
              {{ item.firstTitle }}
            </span>

            <span
              style="
                font-size: 52px;
                font-weight: 900;
                color: #ff6500;
                margin-left: 10px;
              "
            >
              {{ item.secondTitle }}
            </span>

            <q-btn
              round
              dense
              unelevated
              color="orange-9"
              icon="chevron_right"
              class="q-ml-sm"
            />

          </div>


          <div class="row no-wrap" style="gap: 16px;">

            <!-- COUPONS -->
            <div
              class="row no-wrap"
              style="
                background: white;
                border: 4px solid #ffd1d8;
              "
            >

              <div
                v-for="coupon in item.coupons"
                :key="coupon.code"
                style="
                  width: 180px;
                  height: 145px;
                  padding: 18px 10px;
                  text-align: center;
                  border-right: 2px dashed #ffd1d8;
                "
              >

                <div
                  style="
                    font-size: 22px;
                    font-weight: 800;
                    color: #ff3156;
                  "
                >
                  {{ coupon.discount }}
                </div>

                <div
                  style="
                    margin: 10px 0 20px;
                    color: #ff5f79;
                    font-size: 13px;
                  "
                >
                  {{ coupon.order }}
                </div>

                <div
                  style="
                    color: #ff1744;
                    font-size: 12px;
                    font-weight: 700;
                  "
                >
                  Code: {{ coupon.code }}
                </div>

              </div>

            </div>


            <!-- PROMO -->
            <div
              class="row no-wrap"
              style="
                width: 300px;
                height: 149px;
                background: #ffcaca;
              "
            >

              <q-img
                :src="item.image"
                style="
                  width: 145px;
                  height: 149px;
                "
                fit="cover"
              />

              <div
                style="
                  flex: 1;
                  padding: 14px;
                  display: flex;
                  flex-direction: column;
                  justify-content: space-between;
                "
              >

                <div
                  style="
                    font-size: 17px;
                    font-weight: 700;
                    color: #ff6565;
                  "
                >
                  {{ item.title }}
                </div>

                <div
                  style="
                    background: #4d4141;
                    color: white;
                    padding: 6px;
                    width: fit-content;
                    font-weight: bold;
                  "
                >
                  {{ item.price }}
                </div>

              </div>

            </div>

          </div>

        </div>

      </q-carousel-slide>

    </q-carousel>



    <!-- SHIPPING -->
    <div
      class="row items-center justify-center"
      style="
        min-height: 45px;
        gap: 6px;
        background: #f6f6f6;
      "
    >

      <q-icon
        name="local_shipping"
        color="brown"
      />

      <b>Free shipping</b>

      <span>
        On all Choice items
      </span>

    </div>



    <!-- ==================================================
         TODAY'S DEALS
    =================================================== -->
    <div
      style="
        max-width: 1100px;
        margin: auto;
        padding: 28px 20px 45px;
      "
    >

      <div
        class="text-h5 text-weight-bold text-center q-mb-lg"
      >
        Today's deals
      </div>


      <div class="row q-col-gutter-lg">

        <!-- BUNDLE -->
        <div class="col-12 col-md-6">

          <q-card
            flat
            bordered
            style="padding: 18px;"
          >

            <div
              class="text-h6 text-weight-bold text-center"
            >
              Bundle deals
            </div>


            <div class="text-center q-my-sm">

              <q-badge
                rounded
                color="orange-2"
                text-color="black"
                style="padding: 6px 15px;"
              >
                🛍️ 3 from US $2.99
              </q-badge>

            </div>


            <div class="row q-col-gutter-md">

              <div
                v-for="product in bundleProducts"
                :key="product.name"
                class="col-4"
              >

                <q-card flat>

                  <q-img
                    :src="product.image"
                    ratio="1"
                    fit="cover"
                  />

                  <div
                    style="
                      margin-top: 7px;
                      font-size: 12px;
                      min-height: 34px;
                    "
                  >
                    {{ product.name }}
                  </div>

                  <div
                    style="
                      color: #e60012;
                      font-size: 16px;
                      font-weight: 800;
                    "
                  >
                    {{ product.price }}
                  </div>

                  <div
                    style="
                      color: #888;
                      font-size: 10px;
                      text-decoration: line-through;
                    "
                  >
                    {{ product.oldPrice }}
                  </div>

                  <div style="font-size: 10px;">

                    <q-icon
                      name="star"
                      color="orange"
                    />

                    {{ product.rating }}

                    | {{ product.sold }} sold

                  </div>

                </q-card>

              </div>

            </div>

          </q-card>

        </div>


        <!-- SUPER DEALS -->
        <div class="col-12 col-md-6">

          <q-card
            flat
            bordered
            style="padding: 18px;"
          >

            <div
              class="text-h6 text-weight-bold text-center"
            >
              SuperDeals
            </div>


            <div class="text-center q-my-sm">

              <q-badge
                rounded
                color="red-1"
                text-color="negative"
                style="padding: 6px 15px;"
              >
                🔥 Limited time deals
              </q-badge>

            </div>


            <div class="row q-col-gutter-md">

              <div
                v-for="product in superProducts"
                :key="product.name"
                class="col-4"
              >

                <q-card flat>

                  <q-img
                    :src="product.image"
                    ratio="1"
                    fit="cover"
                  />

                  <div
                    style="
                      margin-top: 7px;
                      font-size: 12px;
                      min-height: 34px;
                    "
                  >
                    {{ product.name }}
                  </div>

                  <div
                    style="
                      color: #e60012;
                      font-size: 16px;
                      font-weight: 800;
                    "
                  >
                    {{ product.price }}
                  </div>

                  <div
                    style="
                      color: #888;
                      font-size: 10px;
                      text-decoration: line-through;
                    "
                  >
                    {{ product.oldPrice }}
                  </div>

                  <q-badge
                    color="negative"
                    class="q-mt-xs"
                  >
                    {{ product.discount }}
                  </q-badge>

                </q-card>

              </div>

            </div>

          </q-card>

        </div>

      </div>

    </div>



    <!-- ==================================================
         SUPER BUYER
    =================================================== -->
    <div
      style="
        max-width: 1160px;
        margin: 0 auto 55px;
        padding: 0 20px;
      "
    >

      <div
        style="
          min-height: 430px;
          position: relative;
          overflow: hidden;
          background-image:
            linear-gradient(
              rgba(0,0,0,.42),
              rgba(0,0,0,.42)
            ),
            url('https://images.unsplash.com/photo-1521737604893-d14cc237f11d?auto=format&fit=crop&w=1600&q=85');
          background-size: cover;
          background-position: center;
        "
      >

        <!-- TOP -->
        <div
          style="
            position: relative;
            z-index: 2;
            padding: 28px 30px;
            color: white;
          "
        >

          <div
            style="
              font-size: 27px;
              font-weight: 800;
              font-style: italic;
            "
          >
            SuperBuyer
          </div>


          <div
            class="row"
            style="
              gap: 17px;
              font-size: 11px;
              margin: 8px 0 18px;
            "
          >

            <span>
              ◆ Tax exemptions
            </span>

            <span>
              ◈ Express payment
            </span>

            <span>
              ● Financial support
            </span>

          </div>


          <q-btn
            unelevated
            color="white"
            text-color="black"
            no-caps
            label="Shop now"
          />


          <!-- STATS -->
          <div
            class="row"
            style="
              position: absolute;
              right: 40px;
              top: 30px;
              gap: 60px;
            "
          >

            <div
              style="
                padding-left: 10px;
                border-left: 2px solid rgba(255,255,255,.6);
              "
            >

              <div
                style="
                  font-size: 22px;
                  font-weight: bold;
                "
              >
                5M+
              </div>

              <small>
                Factory direct supply
              </small>


              <div style="height: 16px;"></div>


              <div
                style="
                  font-size: 22px;
                  font-weight: bold;
                "
              >
                10
              </div>

              <small>
                Local warehouses worldwide
              </small>

            </div>


            <div
              style="
                padding-left: 10px;
                border-left: 2px solid rgba(255,255,255,.6);
              "
            >

              <div
                style="
                  font-size: 22px;
                  font-weight: bold;
                "
              >
                20M+
              </div>

              <small>
                Value dropshipping items
              </small>


              <div style="height: 16px;"></div>


              <div
                style="
                  font-size: 22px;
                  font-weight: bold;
                "
              >
                24H
              </div>

              <small>
                Personalized sourcing service
              </small>

            </div>

          </div>

        </div>


        <!-- PRODUCT BOXES -->
        <div
          class="row q-col-gutter-lg"
          style="
            position: absolute;
            left: 28px;
            right: 28px;
            bottom: 28px;
            z-index: 5;
          "
        >

          <!-- BULK SAVER -->
          <div class="col-6">

            <q-card
              flat
              style="
                background: white;
                padding: 12px;
              "
            >

              <div
                class="text-center text-weight-bold"
                style="
                  font-size: 17px;
                  margin-bottom: 10px;
                "
              >
                Bulk Saver Hub
              </div>


              <div class="row q-col-gutter-md">

                <div
                  v-for="item in bulkSaverProducts"
                  :key="item.name"
                  class="col-4"
                >

                  <q-img
                    :src="item.image"
                    ratio="1"
                    fit="cover"
                  />

                  <div
                    style="
                      font-size: 14px;
                      font-weight: bold;
                      margin-top: 6px;
                    "
                  >
                    {{ item.price }}

                    <span
                      style="
                        color: #777;
                        font-size: 9px;
                        text-decoration: line-through;
                      "
                    >
                      {{ item.oldPrice }}
                    </span>

                  </div>

                  <div style="font-size: 9px;">
                    {{ item.tag }}
                  </div>

                </div>

              </div>

            </q-card>

          </div>


          <!-- BUY AGAIN -->
          <div class="col-6">

            <q-card
              flat
              style="
                background: white;
                padding: 12px;
              "
            >

              <div
                class="text-center text-weight-bold"
                style="
                  font-size: 17px;
                  margin-bottom: 10px;
                "
              >
                Buy again
              </div>


              <div class="row q-col-gutter-md">

                <div
                  v-for="item in buyAgainProducts"
                  :key="item.name"
                  class="col-4"
                >

                  <q-img
                    :src="item.image"
                    ratio="1"
                    fit="cover"
                  />

                  <div
                    style="
                      font-size: 14px;
                      font-weight: bold;
                      margin-top: 6px;
                    "
                  >
                    {{ item.price }}

                    <span
                      style="
                        color: #777;
                        font-size: 9px;
                        text-decoration: line-through;
                      "
                    >
                      {{ item.oldPrice }}
                    </span>

                  </div>

                  <div style="font-size: 9px;">
                    {{ item.tag }}
                  </div>

                </div>

              </div>

            </q-card>

          </div>

        </div>

      </div>

    </div>



    <!-- ==================================================
         SHOP BY CATEGORY
    =================================================== -->
    <div
      style="
        max-width: 1160px;
        margin: auto;
        padding: 0 20px 25px;
      "
    >

      <div
        class="text-h5 text-weight-bold text-center"
        style="margin-bottom: 18px;"
      >
        Shop by category
      </div>


      <div class="row q-col-gutter-lg">

        <!-- LEFT VIVA -->
        <div class="col-12 col-md-6">

          <div
            style="
              height: 455px;
              padding: 25px 32px;
              background: #a9eff8;
              position: relative;
              overflow: hidden;
            "
          >

            <div
              style="
                position: relative;
                z-index: 4;
              "
            >

              <div
                style="
                  font-family: Georgia, serif;
                  font-size: 32px;
                  font-style: italic;
                  font-weight: 800;
                "
              >
                Viva
              </div>

              <div
                style="
                  font-size: 12px;
                  margin: 6px 0 14px;
                "
              >
                Your fashion choice
              </div>

              <q-btn
                unelevated
                color="black"
                text-color="white"
                label="Shop now"
                no-caps
                style="
                  border-radius: 0;
                  padding: 6px 18px;
                "
              />

            </div>


            <!-- BIG IMAGE -->
            <q-img
              src="https://images.unsplash.com/photo-1525507119028-ed4c629a60a3?auto=format&fit=crop&w=700&q=85"
              style="
                position: absolute;
                top: 0;
                right: 0;
                width: 54%;
                height: 230px;
              "
              fit="cover"
            />


            <!-- PRODUCTS -->
            <div
              class="row q-col-gutter-sm"
              style="
                position: absolute;
                left: 32px;
                right: 32px;
                bottom: 27px;
                z-index: 4;
              "
            >

              <div
                v-for="item in fashionCategoryProducts"
                :key="item.name"
                class="col-4"
              >

                <q-card
                  flat
                  square
                  style="
                    padding: 5px;
                    background: white;
                  "
                >

                  <q-img
                    :src="item.image"
                    style="
                      width: 100%;
                      height: 180px;
                    "
                    fit="cover"
                  />


                  <div
                    style="
                      font-size: 13px;
                      font-weight: 800;
                      margin-top: 7px;
                    "
                  >
                    {{ item.price }}

                    <span
                      style="
                        font-size: 9px;
                        color: #777;
                        text-decoration: line-through;
                      "
                    >
                      {{ item.oldPrice }}
                    </span>

                  </div>


                  <div style="font-size: 9px;">

                    <q-icon
                      name="star"
                      color="orange"
                    />

                    {{ item.rating }}

                    |
                    {{ item.sold }} sold

                  </div>

                </q-card>

              </div>

            </div>

          </div>

        </div>


        <!-- RIGHT CATEGORY GRID -->
        <div class="col-12 col-md-6">

          <div class="row q-col-gutter-md">

            <div
              v-for="category in shopCategories"
              :key="category.name"
              class="col-6"
            >

              <q-card
                flat
                square
                style="
                  height: 142px;
                  background: #f4f4f4;
                  position: relative;
                  overflow: hidden;
                  cursor: pointer;
                "
              >

                <div
                  style="
                    position: absolute;
                    left: 16px;
                    top: 17px;
                    z-index: 3;
                    font-size: 17px;
                    line-height: 18px;
                    font-weight: 700;
                    width: 110px;
                  "
                >
                  {{ category.name }}
                </div>


                <q-img
                  :src="category.image"
                  style="
                    position: absolute;
                    right: 0;
                    bottom: 0;
                    width: 60%;
                    height: 100%;
                  "
                  fit="contain"
                />

              </q-card>

            </div>

          </div>

        </div>

      </div>

    </div>



    <!-- ==================================================
         MORE TO LOVE
    =================================================== -->
    <div
      style="
        max-width: 1160px;
        margin: auto;
        padding: 0 20px 60px;
      "
    >

      <div
        class="text-h5 text-weight-bold text-center"
        style="margin: 10px 0 18px;"
      >
        More to love
      </div>


      <div class="row q-col-gutter-md">

        <div
          v-for="product in moreLoveProducts"
          :key="product.name"
          class="col-6 col-sm-4 col-md-2"
        >

          <q-card
            flat
            style="
              cursor: pointer;
              position: relative;
            "
          >

            <q-img
              :src="product.image"
              style="
                width: 100%;
                height: 180px;
                background: #f5f5f5;
              "
              fit="cover"
            />


            <q-btn
              round
              unelevated
              color="white"
              text-color="black"
              icon="add_shopping_cart"
              size="sm"
              style="
                position: absolute;
                right: 7px;
                top: 145px;
                z-index: 5;
              "
            />


            <div
              style="
                font-size: 10px;
                margin-top: 7px;
                height: 28px;
                overflow: hidden;
              "
            >
              {{ product.name }}
            </div>


            <div
              style="
                color: #e60012;
                font-size: 16px;
                font-weight: 800;
              "
            >
              {{ product.price }}

              <span
                style="
                  color: #888;
                  font-size: 9px;
                  text-decoration: line-through;
                "
              >
                {{ product.oldPrice }}
              </span>

            </div>


            <div
              style="
                font-size: 9px;
                margin-top: 4px;
              "
            >

              <q-icon
                name="star"
                color="orange"
              />

              {{ product.rating }}

              | {{ product.sold }} sold

            </div>


            <div
              style="
                color: #e60012;
                font-size: 9px;
                margin-top: 3px;
              "
            >
              {{ product.deal }}
            </div>

          </q-card>

        </div>

      </div>

    </div>



    <!-- ==================================================
         FOOTER INFORMATION
    =================================================== -->
    <div
      style="
        width: 100%;
        background: white;
        border-top: 1px solid #eeeeee;
      "
    >

      <div
        style="
          max-width: 1500px;
          margin: auto;
          padding: 28px 20px 38px;
        "
      >

        <div class="row q-col-gutter-xl">

          <!-- ================= LEFT COLUMN ================= -->
          <div class="col-12 col-md-6">

            <!-- HELP -->
            <div style="margin-bottom: 30px;">

              <div
                style="
                  font-size: 16px;
                  font-weight: 700;
                  margin-bottom: 9px;
                  color: #222;
                "
              >
                Help
              </div>

              <div
                style="
                  color: #666;
                  font-size: 14px;
                  line-height: 19px;
                "
              >
                Help Center, Disputes & Reports, Return&refund policy,
                Report IPR infringement, DSA/OSA Information,
                Information and contacts for Brazil, Integrity Compliance,
                Transparency Center, Submit report (non-registered users),
                Return Policy
              </div>

            </div>


            <!-- BROWSE CATEGORY -->
            <div>

              <div
                style="
                  font-size: 16px;
                  font-weight: 700;
                  margin-bottom: 9px;
                  color: #222;
                "
              >
                Browse by Category
              </div>

              <div
                style="
                  color: #666;
                  font-size: 14px;
                  line-height: 19px;
                "
              >
                All Popular, Product, Promotion, Low Price, Great Value,
                Reviews, Wiki, Blog, Video
              </div>

            </div>

          </div>


          <!-- ================= RIGHT COLUMN ================= -->
          <div class="col-12 col-md-6">

            <!-- LANGUAGE SITES -->
            <div style="margin-bottom: 30px;">

              <div
                style="
                  font-size: 16px;
                  font-weight: 700;
                  margin-bottom: 9px;
                  color: #222;
                "
              >
                AliExpress Multi-Language Sites
              </div>

              <div
                style="
                  color: #666;
                  font-size: 14px;
                  line-height: 19px;
                "
              >
                Russian, Portuguese, Spanish, French, German, Italian,
                Dutch, Turkish, Japanese, Korean, Thai, Arabic,
                Hebrew, Polish
              </div>

            </div>


            <!-- ALIBABA GROUP -->
            <div>

              <div
                style="
                  font-size: 16px;
                  font-weight: 700;
                  margin-bottom: 9px;
                  color: #222;
                "
              >
                Alibaba Group
              </div>

              <div
                style="
                  color: #666;
                  font-size: 14px;
                  line-height: 19px;
                "
              >
                Alibaba Group Website, AliExpress, Alimama, Fliggy,
                Alibaba Cloud, Alibaba International, AliTelecom,
                DingTalk, Juhuasuan, Taobao Marketplace, Tmall,
                Taobao Global, AliOS, 1688
              </div>

            </div>

          </div>

        </div>

      </div>

    </div>



    <!-- ==================================================
         FLOATING CART
    =================================================== -->
    <q-page-sticky
      position="bottom-right"
      :offset="[22, 22]"
    >

      <q-btn
        round
        color="white"
        text-color="dark"
        icon="shopping_cart"
        size="lg"
        class="shadow-4"
      />

    </q-page-sticky>

  </q-page>
</template>



<script setup>
import { ref } from 'vue'


const search = ref('')
const slide = ref('sale1')


/* ==================================================
   CATEGORIES
================================================== */

const categories = [
  {
    name: 'Automotive',
    icon: 'directions_car'
  },

  {
    name: 'Appliances',
    icon: 'kitchen'
  },

  {
    name: "Women's Clothing",
    icon: 'checkroom'
  },

  {
    name: "Men's Clothing",
    icon: 'checkroom'
  },

  {
    name: 'Toys & Games',
    icon: 'sports_esports'
  },

  {
    name: 'Furniture',
    icon: 'chair'
  },

  {
    name: 'Beauty & Health',
    icon: 'health_and_safety'
  },

  {
    name: 'Shoes',
    icon: 'hiking'
  },

  {
    name: 'Electronics',
    icon: 'devices'
  }
]


/* ==================================================
   SALE SLIDES
================================================== */

const saleSlides = [
  {
    name: 'sale1',

    firstTitle: 'Fall',
    secondTitle: 'SALE',

    title: 'Super fashion',

    price: '999.99৳',

    image:
      'https://images.unsplash.com/photo-1515886657613-9f3515b0c78f?auto=format&fit=crop&w=600&q=80',

    coupons: [
      {
        discount: '1,100৳ OFF',
        order: 'orders 8,500৳+',
        code: 'OPOCBD09'
      },

      {
        discount: '615৳ OFF',
        order: 'orders 4,800৳+',
        code: 'OPOCBD05'
      },

      {
        discount: '250৳ OFF',
        order: 'orders 1,900৳+',
        code: 'OPOCBD02'
      }
    ]
  },


  {
    name: 'sale2',

    firstTitle: 'Mega',
    secondTitle: 'SALE',

    title: 'New collection',

    price: '1,250.00৳',

    image:
      'https://images.unsplash.com/photo-1591047139829-d91aecb6caea?auto=format&fit=crop&w=600&q=80',

    coupons: [
      {
        discount: '900৳ OFF',
        order: 'orders 7,000৳+',
        code: 'MEGA900'
      },

      {
        discount: '500৳ OFF',
        order: 'orders 4,000৳+',
        code: 'MEGA500'
      },

      {
        discount: '200৳ OFF',
        order: 'orders 1,500৳+',
        code: 'MEGA200'
      }
    ]
  },


  {
    name: 'sale3',

    firstTitle: 'Super',
    secondTitle: 'DEALS',

    title: 'Fashion trends',

    price: '1,532.58৳',

    image:
      'https://images.unsplash.com/photo-1529139574466-a303027c1d8b?auto=format&fit=crop&w=600&q=80',

    coupons: [
      {
        discount: '1,500৳ OFF',
        order: 'orders 10,000৳+',
        code: 'SUPER15'
      },

      {
        discount: '750৳ OFF',
        order: 'orders 5,500৳+',
        code: 'SUPER75'
      },

      {
        discount: '350৳ OFF',
        order: 'orders 2,500৳+',
        code: 'SUPER35'
      }
    ]
  }
]


/* ==================================================
   TODAY'S DEALS
================================================== */

const bundleProducts = [
  {
    name: "Men's Luxury Silver Watch",

    image:
      'https://images.unsplash.com/photo-1523275335684-37898b6baf30?auto=format&fit=crop&w=700&q=80',

    price: '600.67৳',
    oldPrice: '633.06৳',
    rating: '4.6',
    sold: '5,000+'
  },

  {
    name: 'Modern Running Shoes',

    image:
      'https://images.unsplash.com/photo-1542291026-7eec264c27ff?auto=format&fit=crop&w=700&q=80',

    price: '766.50৳',
    oldPrice: '950.00৳',
    rating: '4.6',
    sold: '1,000+'
  },

  {
    name: 'Smart Mobile Phone',

    image:
      'https://images.unsplash.com/photo-1511707171634-5f897ff02aa9?auto=format&fit=crop&w=700&q=80',

    price: '14,618৳',
    oldPrice: '16,000৳',
    rating: '4.7',
    sold: '4,000+'
  }
]


const superProducts = [
  {
    name: 'Modern Laptop Computer',

    image:
      'https://images.unsplash.com/photo-1496181133206-80ce9b88a853?auto=format&fit=crop&w=700&q=80',

    price: '36,622৳',
    oldPrice: '47,982৳',
    discount: '-24%'
  },

  {
    name: 'Wireless Headphones',

    image:
      'https://images.unsplash.com/photo-1505740420928-5e560c06d30e?auto=format&fit=crop&w=700&q=80',

    price: '1,388.67৳',
    oldPrice: '3,585.94৳',
    discount: '-61%'
  },

  {
    name: 'Digital Camera',

    image:
      'https://images.unsplash.com/photo-1516035069371-29a1b244cc32?auto=format&fit=crop&w=700&q=80',

    price: '15,532৳',
    oldPrice: '23,456৳',
    discount: '-35%'
  }
]


/* ==================================================
   SUPER BUYER PRODUCTS
================================================== */

const bulkSaverProducts = [
  {
    name: 'Fast Charging Cable',

    image:
      'https://images.unsplash.com/photo-1583863788434-e58a36330cf0?auto=format&fit=crop&w=600&q=80',

    price: '133.89৳',
    oldPrice: '574.87৳',
    tag: 'Popular picks'
  },

  {
    name: 'Gaming Headset',

    image:
      'https://images.unsplash.com/photo-1585298723682-7115561c51b7?auto=format&fit=crop&w=600&q=80',

    price: '133.89৳',
    oldPrice: '479.70৳',
    tag: 'Popular picks'
  },

  {
    name: 'GaN Charger',

    image:
      'https://images.unsplash.com/photo-1609091839311-d5365f9ff1c5?auto=format&fit=crop&w=600&q=80',

    price: '195.31৳',
    oldPrice: '1,225.91৳',
    tag: 'Verified'
  }
]


const buyAgainProducts = [
  {
    name: 'Humidifier',

    image:
      'https://images.unsplash.com/photo-1585771724684-38269d6639fd?auto=format&fit=crop&w=600&q=80',

    price: '362.85৳',
    oldPrice: '2,150.90৳',
    tag: 'Popular picks'
  },

  {
    name: 'USB Adapter',

    image:
      'https://images.unsplash.com/photo-1587033411391-5d9e51cce126?auto=format&fit=crop&w=600&q=80',

    price: '1,265.23৳',
    oldPrice: '3,551.62৳',
    tag: 'Popular picks'
  },

  {
    name: 'Living Room Rug',

    image:
      'https://images.unsplash.com/photo-1505693416388-ac5ce068fe85?auto=format&fit=crop&w=600&q=80',

    price: '307.87৳',
    oldPrice: '1,989.28৳',
    tag: 'Popular picks'
  }
]


/* ==================================================
   SHOP BY CATEGORY
================================================== */

const fashionCategoryProducts = [
  {
    name: 'White Dress',

    image:
      'https://images.unsplash.com/photo-1566206091558-7f218b696731?auto=format&fit=crop&w=500&q=80',

    price: '2,358.46৳',
    oldPrice: '3,685.09৳',
    rating: '4.5',
    sold: '1,000+'
  },

  {
    name: 'Fashion Dress',

    image:
      'https://images.unsplash.com/photo-1551028719-00167b16eac5?auto=format&fit=crop&w=500&q=80',

    price: '1,293.46৳',
    oldPrice: '2,864.54৳',
    rating: '4.9',
    sold: '500+'
  },

  {
    name: 'Winter Fashion',

    image:
      'https://images.unsplash.com/photo-1548624313-0396c75e4b1a?auto=format&fit=crop&w=500&q=80',

    price: '5,823.86৳',
    oldPrice: '11,908.55৳',
    rating: '4.9',
    sold: '10,000+'
  }
]


const shopCategories = [
  {
    name: "Women's Clothing",

    image:
      'https://images.unsplash.com/photo-1534528741775-53994a69daeb?auto=format&fit=crop&w=500&q=80'
  },

  {
    name: "Men's Clothing",

    image:
      'https://images.unsplash.com/photo-1500648767791-00dcc994a43e?auto=format&fit=crop&w=500&q=80'
  },

  {
    name: 'Toys & Games',

    image:
      'https://images.unsplash.com/photo-1559454403-b8fb88521f11?auto=format&fit=crop&w=500&q=80'
  },

  {
    name: 'Furniture',

    image:
      'https://images.unsplash.com/photo-1567538096630-e0c55bd6374c?auto=format&fit=crop&w=500&q=80'
  },

  {
    name: 'Beauty & Health',

    image:
      'https://images.unsplash.com/photo-1596462502278-27bfdc403348?auto=format&fit=crop&w=500&q=80'
  },

  {
    name: 'Shoes',

    image:
      'https://images.unsplash.com/photo-1542291026-7eec264c27ff?auto=format&fit=crop&w=500&q=80'
  }
]


/* ==================================================
   MORE TO LOVE
================================================== */

const moreLoveProducts = [
  {
    name: 'Portable High Pressure Cleaning Spray Kit',

    image:
      'https://images.unsplash.com/photo-1586864387967-d02ef85d93e8?auto=format&fit=crop&w=500&q=80',

    price: '852.33৳',
    oldPrice: '2,491.49৳',
    rating: '3.4',
    sold: '411',
    deal: '250৳ off on 1,900৳+'
  },

  {
    name: 'Smart Stainless Steel Multifunction Ring',

    image:
      'https://images.unsplash.com/photo-1605100804763-247f67b3557e?auto=format&fit=crop&w=500&q=80',

    price: '47.9৳',
    oldPrice: '',
    rating: '4.3',
    sold: '2,000+',
    deal: '250৳ off on 1,900৳+'
  },

  {
    name: 'Portable Wireless Heavy Bass Speaker',

    image:
      'https://images.unsplash.com/photo-1608043152269-423dbba4e7e1?auto=format&fit=crop&w=500&q=80',

    price: '379.56৳',
    oldPrice: '',
    rating: '3.8',
    sold: '3,000+',
    deal: 'Save 791.28৳'
  },

  {
    name: 'Smart Watch Series 11 Fitness Watch',

    image:
      'https://images.unsplash.com/photo-1523275335684-37898b6baf30?auto=format&fit=crop&w=500&q=80',

    price: '453.27৳',
    oldPrice: '1,337.44৳',
    rating: '4.1',
    sold: '5,000+',
    deal: 'Best price in similar deals'
  },

  {
    name: 'Precision Screwdriver Tool Set',

    image:
      'https://images.unsplash.com/photo-1581147036324-c1c7c2c0d187?auto=format&fit=crop&w=500&q=80',

    price: '386.47৳',
    oldPrice: '555.21৳',
    rating: '4.1',
    sold: '5,000+',
    deal: '250৳ off on 1,900৳+'
  },

  {
    name: 'Men Fashion Black Slippers',

    image:
      'https://images.unsplash.com/photo-1603487742131-4160ec999306?auto=format&fit=crop&w=500&q=80',

    price: '624.66৳',
    oldPrice: '2,026.92৳',
    rating: '4.1',
    sold: '4,000+',
    deal: '250৳ off on 1,900৳+'
  }
]

</script>