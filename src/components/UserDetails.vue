<template>
  <div>
    <p @click="loadAddress(user.id)">{{ user }}</p>
  </div>
  <div v-if = "addresses.length > 0">
      <div v-for = "address in addresses" :key="address.id">
      <AddressDetails :address="address"></AddressDetails>
    </div>

    <v-expansion-panels>
      <v-expansion-panel>
        <v-expansion-panel-titel>
          {{ user.firstname +" "+user.lastname }}
        </v-expansion-panel-titel>
          <v-expansion-panels>
            <v-expansion-panel
              v-for="address in addresses" 
              :key="address.id"
              :title="address.street"
              :text="address.number"
            >
          </v-expansion-panel>
        </v-expansion-panels>
      </v-expansion-panel>
    </v-expansion-panels>
    <!--<v-list>
      <v-list-item 
        v-for = "address in addresses" 
        :key="address.id"
        style="height: 60px;"
        :title="user.firstname + ' ' + user.lastname"
        :subtitle="user.firstname"
        >
        <AddressDetails :address="address"></AddressDetails>
        
          <template v-slot:append>
            <v-btn
            color="primary"
            size="medium"
            variant="text"
            icon="mdi-menu-down"
            @click="menuDown = !menuDown">
          </v-btn>
        </template> 
      </v-list-item>
    </v-list>
    -->
  </div>

</template>

<script>

import axios from 'axios'
import AddressDetails from './AddressDetails.vue';

export default {
    props: {
        user: {}
    },
    data() {
        return {
            addresses: []
        };
    },
    methods: {
        async loadAddress(userId) {
            var addresses = await axios.get("http://localhost:3000/addresses?userId=" + userId);
            addresses.data.forEach(address => console.log(address.street + " " + address.number));
            this.addresses = addresses.data; //legt die Daten der Addressen in addresses ab
        }
    },
    components: { AddressDetails }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
p {
  color: #b9425c;
}
</style>
