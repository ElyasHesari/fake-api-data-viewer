<template>
  <v-responsive :aspect-ratio="16 / 9" style="max-height: 75vh">
    <v-app>
      <v-img src="/img/vue-mk-header.jpg" height="400" cover>
        <div class="header-menu-container" style="z-index: 10">
          <v-container
            fluid
            class="header-menu"
            style="height: 49px !important"
          >
            <v-app-bar
              app
              color="rgba(241, 246, 241, 0.92)"
              flat
              class="mt-6 rounded-lg"
              style="max-width: 1200px"
            >
              <v-menu>
                <template v-slot:activator="{ props }">
                  <NabvarItem v-bind="props" name="لینک ها" icon="link" to="" />
                </template>

                <v-list>
                  <v-list-item class="text-center my-4">
                    <v-list-item-title class="py-4">
                      <v-btn
                        flat
                        href="https://github.com/ElyasHesari/"
                        class="list-item"
                      >
                        <span class="">گیت هاب</span>
                        <v-icon>mdi-github</v-icon>
                      </v-btn>
                    </v-list-item-title>
                    <v-list-item-title>
                      <v-btn
                        flat
                        href="https://www.linkedin.com/in/elyashesari"
                        class="list-item d-flex justify-space-between"
                      >
                        لینکدین
                        <v-icon class="pl-5">mdi-phone-message-outline</v-icon>
                      </v-btn>
                    </v-list-item-title>
                    <v-list-item-title class="py-4">
                      <v-btn
                        flat
                        href="'mailto:' + elyashesari@gmail.com"
                        class="list-item d-flex justify-space-between"
                      >
                        ایمیل
                        <v-icon class="pl-9">mdi-gmail</v-icon>
                      </v-btn>
                    </v-list-item-title>
                  </v-list-item>
                </v-list>
              </v-menu>
              <v-menu>
                <template v-slot:activator="{ props }">
                  <NabvarItem
                    v-bind="props"
                    name="صفحه ها"
                    icon="widgets"
                    to=""
                  />
                </template>

                <v-list>
                  <v-list-item class="text-center my-4">
                    <v-list-item-title
                      class="py-4 list-item d-flex justify-space-between"
                    >
                      <span>درباره ما</span>
                      <v-icon>mdi-information-outline</v-icon>
                    </v-list-item-title>
                    <v-list-item-title
                      class="py-4 list-item d-flex justify-space-between"
                    >
                      ارتباط با ما
                      <v-icon>mdi-phone-message-outline</v-icon>
                    </v-list-item-title>
                    <v-list-item-title
                      class="py-4 d-flex justify-space-between list-item"
                    >
                      ثبت نام
                      <v-icon>mdi-login</v-icon>
                    </v-list-item-title>
                  </v-list-item>
                </v-list>
              </v-menu>
              <v-spacer></v-spacer>
              <span class="mr-6">نام برند</span>
            </v-app-bar>
          </v-container>
          <v-main
            dir="rtl"
            height="50vh"
            class="d-flex align-center justify-center flex-column"
          >
            <div class="text-h3 mb-10 text-white">عنوان اصلی</div>
            <div class="text-h6 text-white text-center" style="width: 600px">
              لورم ایپسوم متن ساختگی با تولید سادگی نامفهوم از صنعت چاپ لورم
              ایپسوم متن ساختگی با تولی از صنعت چاپ
            </div>
          </v-main>
        </div>
      </v-img>
    </v-app>
  </v-responsive>
</template>

<script setup lang="ts">
import NabvarItem from "@/components/NabvarItem.vue";
</script>

<style scoped>
.header-menu-container {
  position: absolute;
  left: 50%;
  transform: translateX(-45%);
  color: rgba(241, 246, 241, 0.92);
}

.header-menu {
  width: 1260px;
  /* background-color: transparent; */
}

:deep(.v-toolbar__content) {
  height: 55px !important;
}

.list-item {
  color: gray;
  font-size: 14px;
}

.text-white {
  color: white;
}
</style>