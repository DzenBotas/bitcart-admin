<template>
  <div>
    <div v-if="noServices" class="pt-5">
      No hidden services found. Enable tor via
      <code>export BITCART_ADDITIONAL_COMPONENTS=tor; ./setup.sh</code>
      to enable hidden services
    </div>
    <v-list v-if="!noServices">
      <div v-for="(service, name) in $store.state.services" :key="name">
        <v-list-item>
          <v-list-item-content>
            <v-list-item-title class="display-1 pb-4" v-text="name" />
            <v-list-item-subtitle class="text--primary">
              <p class="display-1">
                General information
              </p>
              <p class="title">
                Hostname
              </p>
              <p class="subtitle">
                {{ service.hostname }}
              </p>
              <div v-if="$auth.user.is_superuser">
                <p class="title">
                  Directory
                </p>
                <p class="subtitle">
                  {{ service.directory }}
                </p>
                <div v-if="service.port_definition">
                  <p class="display-1">
                    Port definition
                  </p>
                  <p class="title">
                    Virtual port
                  </p>
                  <p class="subtitle">
                    {{ service.port_definition[0] }}
                  </p>
                  <p class="title">
                    IP Address
                  </p>
                  <p class="subtitle">
                    {{ service.port_definition[1] }}
                  </p>
                  <p class="title">
                    Port
                  </p>
                  <p class="subtitle">
                    {{ service.port_definition[2] }}
                  </p>
                </div>
              </div>
            </v-list-item-subtitle>
          </v-list-item-content>
        </v-list-item>
        <v-divider />
      </div>
    </v-list>
  </div>
</template>

<script>
export default {
  layout: 'basicadmin',
  computed: {
    noServices () {
      return Object.keys(this.$store.state.services).length === 0 && this.$store.state.services.constructor === Object
    }
  }
}
</script>
