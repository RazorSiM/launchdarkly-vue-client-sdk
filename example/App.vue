<script setup lang="ts">
import { ldInit, useLDFlag, LD_FLAG } from '../src'

// Set clientSideID to your LaunchDarkly client-side ID
const clientSideID = 'CLIENT-SIDE-ID'

// Set up the context properties. This context should appear on your LaunchDarkly
// contexts dashboard soon after you run the demo.
const context = { kind:'user', key: 'example-context-key', name: 'Sandy' }

// Set featureFlagKey to the feature flag key you want to evaluate
const featureFlagKey = 'my-boolean-flag'

if (!clientSideID) {
  console.warn('Please edit App.vue to set clientSideID to your LaunchDarkly client-side ID')
}
const [ldReady, _ldClient] = ldInit({ clientSideID, context })
const flagValue = useLDFlag(featureFlagKey, false /* default flag value */)
</script>

<template>
  <div v-if="ldReady">
    SDK successfully initialized! Feature flag '{{ featureFlagKey }}' is {{ flagValue }}
    for this context.
  </div>
  <div v-else>LaunchDarkly client initializing...</div>
</template>
