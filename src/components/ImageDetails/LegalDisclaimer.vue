<template>
  <div class="margin-top-normal">
    <p
      class="caption has-text-left has-text-grey-dark has-text-weight-semibold"
    >
      {{ $t('photo-details.legal-disclaimer') }}
    </p>
  </div>
</template>

<script>
export default {
  name: 'LegalDisclaimer',
}
</script>

<style lang="scss" scoped>
li:before {
  content: '\2022';
  color: #ccc;
  font-weight: bold;
  display: inline-block;
  margin-right: 0.5rem;
  font-size: 1rem;
}
</style>
