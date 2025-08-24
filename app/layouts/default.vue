<script setup lang="ts">
import type { NavigationMenuItem } from "@nuxt/ui";

const open = ref(false);

const links = [
  [
    {
      label: "Home",
      icon: "i-lucide-house",
      to: "/",
      onSelect: () => {
        open.value = false;
      },
    },
    {
      label: "Stations",
      to: "#",
      icon: "i-lucide-power",
      defaultOpen: true,
      type: "trigger",
      children: [
        {
          label: "Transmission Stations",
          to: "#",
          exact: true,
          onSelect: () => {
            open.value = false;
          },
        },
        {
          label: "Injection Substations",
          to: "#",
          exact: true,
          onSelect: () => {
            open.value = false;
          },
        },
        {
          label: "Distribution Substations",
          to: "#",
          exact: true,
          onSelect: () => {
            open.value = false;
          },
        },
      ],
    },
    {
      label: "Feeders",
      to: "#",
      icon: "i-lucide-utility-pole",
      defaultOpen: true,
      type: "trigger",
      children: [
        {
          label: "33kV Feeders",
          to: "#",
          exact: true,
          onSelect: () => {
            open.value = false;
          },
        },
        {
          label: "11kV Feeders",
          to: "#",
          exact: true,
          onSelect: () => {
            open.value = false;
          },
        },
      ],
    },
  ],
] satisfies NavigationMenuItem[][];

const groups = computed(() => [{
  id: "links",
  label: "Go to",
  items: links.flat(),
}]);
</script>

<template>
  <UDashboardGroup unit="rem">
    <UDashboardSidebar
      id="default"
      v-model:open="open"
      collapsible
      resizable
      class="bg-elevated/25"
      :ui="{ footer: 'lg:border-t lg:border-default' }"
    >
      <template #header="{ collapsed }">
        <UButton
          label="KEAR"
          :avatar="{
            src: 'https://github.com/nuxt-hub.png',
            alt: 'NuxtHub',
          }"
          color="neutral"
          variant="ghost"
          block
          :square="collapsed"
          class="data-[state=open]:bg-elevated"
          :class="[!collapsed && 'py-2']"
          :ui="{
            base: 'justify-start',
          }"
        />
      </template>

      <template #default="{ collapsed }">
        <UDashboardSearchButton :collapsed="collapsed" class="bg-transparent ring-default" />

        <UNavigationMenu
          :collapsed="collapsed"
          :items="links[0]"
          orientation="vertical"
          tooltip
          popover
        />
      </template>

      <template #footer="{ collapsed }">
        <UserMenu :collapsed="collapsed" />
      </template>
    </udashboardsidebar>

    <UDashboardSearch :groups="groups" />

    <slot />
  </UDashboardGroup>
</template>
