<!-- SPDX-License-Identifier: AGPL-3.0-or-later -->
<template>
  <!-- Note: Content Sections Top for Mobile -->
  <div class="flex flex-col items-center justify-center space-y-5">
    <div class="flex flex-col items-center justify-center space-y-2">
      <p>
        {{ $t("i18n.components.footer.flex._global.scribe_tagline") }}
      </p>
      <!-- Note: Platform Links -->
      <div class="flex flex-wrap items-center justify-center">
        <template v-for="(platform, index) in links.platformLinks">
          <div class="hover:text-distinct-text">
            <NuxtLink
              v-if="platform.isLocalePath"
              class="focus-brand"
              :to="localePath(platform.url)"
            >
              {{ $t(platform.name) }}
            </NuxtLink>
            <a v-else :href="platform.url" class="focus-brand" target="_blank">
              {{ $t(platform.name) }}
            </a>
          </div>
          <div v-if="index < links.platformLinks.length - 1" class="px-2">
            •
          </div>
        </template>
      </div>
    </div>
    <div
      class="grid max-w-xl justify-items-center gap-0 text-center sm:grid-cols-1 sm:gap-12 sm:text-left md:gap-16"
    >
      <!-- Note: Connect Links -->
      <div class="text-center">
        <p class="text-xl font-medium">
          {{ $t("i18n.components.footer.flex._global.connect") }}
        </p>
        <div class="mt-1 flex gap-10 sm:mt-0 sm:flex-col sm:gap-0">
          <template v-for="(connect, index) in links.connectLinks">
            <a
              class="focus-brand mt-2 flex items-center space-x-2 text-base hover:text-distinct-text"
              :class="{ 'mt-3': index === 0 }"
              :href="connect.url"
              target="_blank"
              :aria-label="$t(connect.name)"
            >
              <MetaTagSocialMedia
                class="text-2xl sm:text-base"
                :iconName="connect.iconName"
                :text="$t(connect.name)"
                textUtilityClasses="sr-only sm:not-sr-only"
              />
            </a>
          </template>
        </div>
      </div>
      <!-- Note: Resources Links -->
      <div>
        <p class="mt-6 text-xl font-medium sm:mt-0">
          {{ $t("i18n.components.footer.flex._global.resources") }}
        </p>
        <div class="flex flex-wrap justify-center gap-x-1 sm:flex-col sm:gap-0">
          <template v-for="(resource, index) in links.resourcesLinks">
            <p
              class="mt-2 text-base hover:text-distinct-text"
              :class="{ 'sm:mt-3': index === 0 }"
            >
              <NuxtLink class="focus-brand" :to="localePath(resource.url)">
                {{ $t(resource.name) }}
              </NuxtLink>
              <span
                v-if="index < links.resourcesLinks.length - 1"
                class="flex-inline px-2 sm:hidden"
              >
                •
              </span>
            </p>
          </template>
        </div>
      </div>
      <!-- Note: Organization Links -->
      <div>
        <p class="mt-6 text-xl font-medium sm:mt-0">
          {{ $t("i18n.components.footer.flex._global.organization") }}
        </p>
        <div class="flex flex-wrap justify-center gap-x-1 sm:flex-col sm:gap-0">
          <template v-for="(oLink, index) in links.organizationLinks">
            <p
              class="mt-2 text-base hover:text-distinct-text"
              :class="{ 'sm:mt-3': index === 0 }"
            >
              <NuxtLink class="focus-brand" :to="localePath(oLink.url)">
                {{ $t(oLink.name) }}
              </NuxtLink>
              <span
                v-if="index < links.organizationLinks.length - 1"
                class="flex-inline px-2 sm:hidden"
              >
                •
              </span>
            </p>
          </template>
        </div>
      </div>
    </div>
    <div class="flex flex-col items-center justify-center">
      <!-- Note: Legal Links -->
      <div class="flex flex-wrap items-center justify-center">
        <template v-for="(policy, index) in links.legalLinks">
          <div class="hover:text-distinct-text">
            <NuxtLink class="focus-brand" :to="localePath(policy.url)">
              {{ $t(policy.name) }}
            </NuxtLink>
            <span
              v-if="index < links.legalLinks.length - 1"
              class="flex-inline px-2"
            >
              •
            </span>
          </div>
        </template>
      </div>
      <a
        class="mt-2 w-fit hover:text-distinct-text"
        href="https://www.netlify.com/"
        target="_blank"
      >
        {{ $t("i18n.components.footer.flex._global.powered_by_netlify") }}
      </a>
      <p class="mt-2">
        {{
          $t("i18n.components.footer.flex._global.copyright", {
            year: new Date().getFullYear(),
          })
        }}
      </p>
    </div>
  </div>
</template>

<script setup lang="ts">
const localePath = useLocalePath();

defineProps<{
  links: {
    platformLinks: {
      name: string;
      url: string;
      isLocalePath: boolean;
    }[];
    legalLinks: {
      name: string;
      url: string;
    }[];
    connectLinks: {
      name: string;
      url: string;
      iconName: string;
      iconSize: string;
    }[];
    resourcesLinks: {
      name: string;
      url: string;
    }[];
    organizationLinks: {
      name: string;
      url: string;
    }[];
  };
}>();
</script>
