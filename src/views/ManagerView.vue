<script>
export default {

    data() {
        return {
            activeTab: 0,
        }
    },
}
</script>

<template>
  <div class="video-manager">
    <o-tabs v-model="activeTab"
            type="toggle">

      <o-tab-item :value="0" label="VIDEO">
        <p class="block">
          Here you can see all VIDEO resources available on QDN.
        </p>
      </o-tab-item>

      <o-tab-item :value="1" label="Q-Tube">
        <p class="block">
          Here you can see videos which have been published on Q-Tube.
        </p>
      </o-tab-item>

    </o-tabs>
  </div>
</template>
