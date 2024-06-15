<template>
  <v-data-table
    dir="rtl"
    :headers="headers"
    :items="desserts"
    :sort-by="[{ key: 'category', order: 'asc' }]"
  >
    <template v-slot:top>
      <v-toolbar flat>
        
        <v-dialog v-model="dialog" max-width="500px">
          <template v-slot:activator="{ props }">
            <v-btn class="mb-2 text-h6" color="green" dark v-bind="props">
              افزودن ایتم
            </v-btn>
          </template>
          <v-card>
            <v-card-title>
              <span class="text-h5">{{ formTitle }}</span>
            </v-card-title>

            <v-card-text>
              <v-container>
                <v-row>
                  <v-col cols="12" md="4" sm="6">
                    <v-text-field
                      v-model="editedItem.name"
                      label="Dessert name"
                    ></v-text-field>
                  </v-col>
                  <v-col cols="12" md="4" sm="6">
                    <v-text-field
                      v-model="editedItem.category"
                      label="category"
                    ></v-text-field>
                  </v-col>
                  <v-col cols="12" md="4" sm="6">
                    <v-text-field
                      v-model="editedItem.location"
                      label="location (g)"
                    ></v-text-field>
                  </v-col>
                  <v-col cols="12" md="4" sm="6">
                    <v-text-field
                      v-model="editedItem.organizer"
                      label="organizer (g)"
                    ></v-text-field>
                  </v-col>
                  <v-col cols="12" md="4" sm="6">
                    <v-text-field
                      v-model="editedItem.time"
                      label="time (g)"
                    ></v-text-field>
                  </v-col>
                </v-row>
              </v-container>
            </v-card-text>

            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn color="green-darken-1" variant="text" @click="close">
                لغو
              </v-btn>
              <v-btn color="green-darken-1" variant="text" @click="save">
                ذخیره
              </v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
        <v-dialog v-model="dialogDelete" max-width="500px">
          <v-card>
            <v-card-title class="text-h5 text-right"
              >از حذف ایتم اطمینان دارید؟</v-card-title
            >
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn color="green-darken-1" variant="text" @click="closeDelete"
                >لغو</v-btn
              >
              <v-btn
                color="green-darken-1"
                variant="text"
                @click="deleteItemConfirm"
                >بله</v-btn
              >
              <v-spacer></v-spacer>
            </v-card-actions>
          </v-card>
        </v-dialog>
        <v-divider class="mx-4" inset vertical></v-divider>
        <v-spacer></v-spacer>
        <v-toolbar-title class="text-right mr-4">نام جدول</v-toolbar-title>
      </v-toolbar>
    </template>
    <template v-slot:item.actions="{ item }">
      <v-icon class="me-2" size="small" @click="editItem(item)">
        mdi-pencil
      </v-icon>
      <v-icon size="small" @click="deleteItem(item)" color="red"> mdi-delete </v-icon>
    </template>
    <template v-slot:no-data>
      <v-btn color="primary" @click="initialize"> Reset </v-btn>
    </template>
  </v-data-table>
</template>
  
<script setup>
import { reactive, computed, watch, onMounted, ref } from "vue";

const props = defineProps(['events'])
const dialog = ref(false);
const dialogDelete = ref(false);
const headers = [
  {
    title: "title",
    align: "start",
    sortable: false,
    key: "title",
  },
  { title: "category", key: "category" },
  { title: "location", key: "location" },
  { title: "organizer", key: "organizer" },
  { title: "time", key: "time" },
  { title: "Actions", key: "actions", sortable: false },
];
const desserts = ref([]);
const editedIndex = ref(-1);
const editedItem = reactive({
  name: "",
  category: 0,
  location: 0,
  organizer: 0,
  time: 0,
});
const defaultItem = {
  name: "",
  category: "",
  location: "",
  organizer: "",
  time: 0,
};

const formTitle = computed(() => {
  return editedIndex.value === -1 ? "افزودن ایتم" : "تغییر ایتم";
});

watch(dialog, (val) => {
  if (!val) {
    close();
  }
});

watch(dialogDelete, (val) => {
  if (!val) {
    closeDelete();
  }
});

onMounted(() => {
  initialize();
});

function initialize() {
  desserts.value = props.events
  console.log('desserts desserts', desserts.value)

}

function editItem(item) {
  editedIndex.value = desserts.value.indexOf(item);
  editedItem.name = item.name;
  editedItem.category = item.category;
  editedItem.location = item.location;
  editedItem.organizer = item.organizer;
  editedItem.time = item.time;
  dialog.value = true;
}

function deleteItem(item) {
  editedIndex.value = desserts.value.indexOf(item);
  editedItem.name = item.name;
  editedItem.category = item.category;
  editedItem.location = item.location;
  editedItem.organizer = item.organizer;
  editedItem.time = item.time;
  dialogDelete.value = true;
}

function deleteItemConfirm() {
  desserts.value.splice(editedIndex.value, 1);
  closeDelete();
}

function close() {
  dialog.value = false;
  nextTick(() => {
    editedItem.name = defaultItem.name;
    editedItem.category = defaultItem.category;
    editedItem.location = defaultItem.location;
    editedItem.organizer = defaultItem.organizer;
    editedItem.time = defaultItem.time;
    editedIndex.value = -1;
  });
}

function closeDelete() {
  dialogDelete.value = false;
  nextTick(() => {
    editedItem.name = defaultItem.name;
    editedItem.category = defaultItem.category;
    editedItem.location = defaultItem.location;
    editedItem.organizer = defaultItem.organizer;
    editedItem.time = defaultItem.time;
    editedIndex.value = -1;
  });
}

function save() {
  if (editedIndex.value > -1) {
    Object.assign(desserts[editedIndex.value], editedItem);
  } else {
    desserts.value.push({ ...editedItem });
  }
  close();
}
</script>