<!-- SPDX-License-Identifier: AGPL-3.0-or-later -->
<template>
  <div
    v-if="contentPosition === 'left'"
    class="flex items-center justify-center py-8 sm:py-12 md:py-16 lg:space-x-20 lg:py-24 xl:space-x-32 xl:py-28 2xl:space-x-40"
  >
    <div
      class="flex w-full flex-col items-center space-y-3 sm:w-10/12 lg:max-w-sm lg:items-start xl:max-w-md xl:space-y-4"
    >
      <!-- Note: image on top of content. -->
      <img
        v-if="$colorMode.value == 'light' && !aboveLargeBP"
        class="mb-4 h-48 sm:h-52 md:h-56"
        :src="imgURL + '_light.png'"
        :alt="$t(imageAltText)"
      />
      <img
        v-else-if="$colorMode.value == 'dark' && !aboveLargeBP"
        class="mb-4 h-48 sm:h-52 md:h-56"
        :src="imgURL + '_dark.png'"
        :alt="$t(imageAltText)"
      />
      <h2
        class="w-10/12 text-center text-2xl font-semibold sm:w-full sm:text-3xl lg:text-left xl:text-4xl"
      >
        {{ $t(header) }}
      </h2>
      <p
        class="text-transform: w-10/12 text-center text-base uppercase tracking-wider text-distinct-text sm:w-full sm:text-lg lg:text-left xl:text-xl"
      >
        {{ $t(tagline) }}
      </p>
      <p
        class="w-10/12 pb-2 text-center text-sm sm:w-full sm:text-base md:text-lg lg:text-left"
      >
        {{ $t(text) }}
      </p>
      <!-- <BtnRouteInternal
        :id="btnId1"
        :cta="true"
        :label="`${btnText1}`"
        :linkTo="`${btnUrl1}`"
        fontSize="xl"
        :ariaLabel="btnAriaLabel1 ? btnAriaLabel1 : ''"
      /> -->
    </div>
    <!-- Note: image right of content. -->
    <div v-if="aboveLargeBP" class="h-60 w-60 xl:h-72 xl:w-72">
      <img
        v-if="$colorMode.value == 'light'"
        :src="imgURL + '_light.png'"
        :alt="$t(imageAltText)"
      />
      <img
        v-else-if="$colorMode.value == 'dark'"
        :src="imgURL + '_dark.png'"
        :alt="$t(imageAltText)"
      />
    </div>
  </div>
  <div
    v-else-if="contentPosition === 'right'"
    class="flex items-center justify-center bg-layer-0 py-8 sm:py-12 md:py-16 lg:space-x-20 lg:py-24 xl:space-x-32 xl:py-28 2xl:space-x-40"
  >
    <!-- Note: image left of content. -->
    <div v-if="aboveLargeBP" class="h-60 w-60 xl:h-72 xl:w-72">
      <img
        v-if="$colorMode.value == 'light'"
        :src="imgURL + '_light.png'"
        :alt="$t(imageAltText)"
      />
      <img
        v-else-if="$colorMode.value == 'dark'"
        :src="imgURL + '_dark.png'"
        :alt="$t(imageAltText)"
      />
    </div>
    <div
      class="flex w-full flex-col items-center space-y-3 sm:w-10/12 lg:max-w-sm lg:items-start xl:max-w-md xl:space-y-4"
    >
      <!-- Note: image on top of content. -->
      <img
        v-if="$colorMode.value == 'light' && !aboveLargeBP"
        class="mb-4 h-48 sm:h-52 md:h-56"
        :src="imgURL + '_light.png'"
        :alt="$t(imageAltText)"
      />
      <img
        v-else-if="$colorMode.value == 'dark' && !aboveLargeBP"
        class="mb-4 h-48 sm:h-52 md:h-56"
        :src="imgURL + '_dark.png'"
        :alt="$t(imageAltText)"
      />
      <h2
        class="w-10/12 text-center text-2xl font-semibold sm:w-full sm:text-3xl lg:text-left xl:text-4xl"
      >
        {{ $t(header) }}
      </h2>
      <p
        class="text-transform: w-10/12 text-center text-base uppercase tracking-wider text-distinct-text sm:w-full sm:text-lg lg:text-left xl:text-xl"
      >
        {{ $t(tagline) }}
      </p>
      <p
        class="w-10/12 pb-2 text-center text-sm sm:w-full sm:text-base md:text-lg lg:text-left"
      >
        {{ $t(text) }}
      </p>
      <!-- <BtnRouteInternal
        :id="btnId1"
        :cta="true"
        :label="`${btnText1}`"
        :linkTo="`${btnUrl1}`"
        fontSize="xl"
        :ariaLabel="btnAriaLabel1 ? btnAriaLabel1 : ''"
      /> -->
    </div>
  </div>
  <div
    v-else-if="contentPosition === 'top'"
    class="flex items-center justify-center pb-10 pt-16 sm:pb-16 md:pb-20 xl:py-24"
  >
    <div class="flex flex-col items-center space-y-3 xl:space-y-4">
      <h2
        class="w-10/12 text-center text-2xl font-semibold sm:w-full sm:text-3xl xl:text-4xl"
      >
        {{ $t(header) }}
      </h2>
      <p
        class="text-transform: w-10/12 text-center text-base uppercase tracking-wider text-distinct-text sm:w-full sm:text-lg xl:text-xl"
      >
        {{ $t(tagline) }}
      </p>
      <p
        class="mx-12 w-10/12 pb-2 text-center text-sm sm:text-base md:w-full md:max-w-lg md:text-lg lg:max-w-xl"
      >
        {{ $t(text) }}
      </p>
      <!-- <div class="style-btns-next-to-one-another">
        <BtnRouteInternal
          :id="btnId1"
          class="w-full"
          :cta="true"
          :label="`${btnText1}`"
          :linkTo="`${btnUrl1}`"
          fontSize="xl"
          :ariaLabel="btnAriaLabel1 ? btnAriaLabel1 : ''"
        />
        <BtnRouteInternal
          :id="btnId2"
          class="w-full"
          :cta="true"
          :label="`${btnText2}`"
          :linkTo="`${btnUrl2}`"
          fontSize="xl"
          :ariaLabel="btnAriaLabel2 ? btnAriaLabel2 : ''"
        />
      </div> -->
      <div>
        <GridSupporters class="mt-6 xl:mt-8" />
      </div>
      <p
        v-if="subText"
        class="mx-12 pt-8 text-center text-distinct-text md:max-w-md lg:max-w-lg xl:pt-12"
      >
        {{ $t(subText) }}
      </p>
    </div>
  </div>
</template>

<script setup lang="ts">
defineProps<{
  contentPosition: "left" | "right" | "top";
  header: string;
  tagline: string;
  text: string;
  imgURL?: string;
  imageAltText: string;
  btnText1: string;
  btnUrl1: string;
  btnAriaLabel1?: string;
  btnId1?: string;
  btnId2?: string;
  btnText2?: string;
  btnUrl2?: string;
  btnAriaLabel2?: string;
  subText?: string;
}>();

const aboveLargeBP = useBreakpoint("lg");
</script>
