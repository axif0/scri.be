<!-- SPDX-License-Identifier: AGPL-3.0-or-later -->
<template>
  <MenuLinkWrapper :to="routeUrl" :selected="selected">
    <div
      class="relative z-0 flex w-full items-center space-x-2 text-left text-sm font-medium"
    >
      <span class="pl-1">
        <Icon v-if="iconUrl" class="h-5 w-5 flex-shrink-0" :name="iconUrl" />
      </span>
      <Transition>
        <p
          v-if="sidebar.collapsed == false || sidebar.collapsedSwitch == false"
          class="select-none whitespace-nowrap"
        >
          <span class="sr-only">{{ $t("i18n._global.navigate_to") }}</span>
          {{ $t(label) }}
        </p>
        <span v-else class="sr-only">
          {{ $t("i18n._global.navigate_to") }} {{ $t(label) }}
        </span>
      </Transition>
    </div>
  </MenuLinkWrapper>
</template>

<script setup lang="ts">
defineProps<{
  label: string;
  routeUrl: string;
  iconUrl: string;
  selected: boolean;
}>();

const sidebar = useSidebar();
</script>

<style>
.v-enter-active {
  transition: opacity 0.25s ease;
  transition-delay: 0.125s;
}
.v-leave-active {
  transition: opacity 0.25s ease;
}

.v-enter-from,
.v-leave-to {
  opacity: 0;
}
.v-enter-from .inner {
  transition-delay: 0.25s;
}
</style>
