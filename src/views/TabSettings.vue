<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Settings</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <ion-list>
        <ion-item>
          <ion-input
            label="Size Column"
            v-model="sizeColumn"
          ></ion-input>
        </ion-item>
      </ion-list>
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import {
  IonPage,
  IonHeader,
  IonToolbar,
  IonTitle,
  IonContent,
  IonInput,
  IonItem,
  IonList,
  onIonViewWillEnter,
} from '@ionic/vue';
import ExploreContainer from '@/components/ExploreContainer.vue';
import { ref, watch } from 'vue';
import { Preferences } from '@capacitor/preferences';

const sizeColumn = ref<string>();

watch(sizeColumn, newValue => {
  Preferences.set({
    key: 'sizeColumn',
    value: newValue as string,
  });
  console.log('newValue', newValue);
});

onIonViewWillEnter(async () => {
  sizeColumn.value = (await Preferences.get({ key: 'sizeColumn' }))
    .value as string;
  console.log(`sizeColumn ${sizeColumn.value}!`);
});
</script>
