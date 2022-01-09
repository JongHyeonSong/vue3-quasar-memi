<script setup lang="ts">
import { initializeApp } from 'firebase/app';
import { getAnalytics } from 'firebase/analytics';
import {
  getAuth,
  connectAuthEmulator,
  signInWithPopup,
  onAuthStateChanged,
  User,
} from 'firebase/auth';
import { GoogleAuthProvider } from 'firebase/auth';
// TODO: Add SDKs for Firebase products that you want to use
// https://firebase.google.com/docs/web/setup#available-libraries

// Your web app's Firebase configuration
// For Firebase JS SDK v7.20.0 and later, measurementId is optional
const firebaseConfig = {
  apiKey: 'AIzaSyCMDOmvAM_jkwe_Ld1t2KPh5U8TBFM6kUI',
  authDomain: 'vue3-quasar-emi.firebaseapp.com',
  databaseURL: 'https://vue3-quasar-emi-default-rtdb.firebaseio.com',
  projectId: 'vue3-quasar-emi',
  storageBucket: 'vue3-quasar-emi.appspot.com',
  messagingSenderId: '1088846960177',
  appId: '1:1088846960177:web:48a42db9ac5c3558cda710',
  measurementId: 'G-RDZGG7YPQG',
};

// Initialize Firebase
const app = initializeApp(firebaseConfig);
// eslint-disable-next-line @typescript-eslint/no-unused-vars
const analytics = getAnalytics(app);

const auth = getAuth();
connectAuthEmulator(auth, 'http://localhost:9099');
const provider = new GoogleAuthProvider();
auth.useDeviceLanguage();

import { ref } from 'vue';
const firebaseUser = ref<User | null>(null);

onAuthStateChanged(auth, (user) => {
  console.log(user);
  firebaseUser.value = user;
});
</script>
<template>
  <q-btn @click="auth.signOut()" v-if="firebaseUser" round>
    <q-avatar size="md">
      <img :src="firebaseUser.photoURL || ''" alt="" />
    </q-avatar>
    <!-- {{ firebaseUser.uid }} -->
  </q-btn>
  <q-btn
    rounded
    color="primary"
    icon="check"
    label="OK"
    @click="signInWithPopup(auth, provider)"
  >
  </q-btn>
</template>
