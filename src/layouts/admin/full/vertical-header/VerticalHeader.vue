<script setup lang="ts">
import { ref, watch } from 'vue';
import NotificationDD from './NotificationDD.vue';
import ProfileDD from './ProfileDD.vue';
import Searchbar from './Searchbar.vue';
import RightMobileSidebar from './RightMobileSidebar.vue';
import { Icon } from '@iconify/vue';
import Logo from '../logo/Logo.vue';
import ThemeToggler from './ThemeToggler.vue';
import { useCustomizerStore } from '@/stores/customizer';
const customizer = useCustomizerStore();
const showSearch = ref(false);
const priority = ref(customizer.setHorizontalLayout ? 0 : 0);
function searchbox() {
    showSearch.value = !showSearch.value;
}
watch(priority, (newPriority) => {
    priority.value = newPriority;
});
</script>

<template>
    <v-app-bar elevation="0" :priority="priority" height="70" class="main-head">
        <v-btn
            class="hidden-lg-and-up custom-hover-primary"
            size="small"
            variant="text"
            color="primary"
            icon
            @click.stop="customizer.SET_SIDEBAR_DRAWER"
        >
            <Icon icon="solar:hamburger-menu-line-duotone" height="22" />
        </v-btn>

        <!-- ---------------------------------------------- -->
        <!-- Search part -->
        <!-- ---------------------------------------------- -->
        <!-- <Searchbar /> -->

        <!-- ---------------------------------------------- -->
        <!-- Mega menu -->
        <!-- ---------------------------------------------- -->

        <v-spacer class="hidden-sm-and-down" />

        <!-- ---------------------------------------------- -->
        <!-- Mobile Logo -->
        <!-- ---------------------------------------------- -->
        <div class="hidden-md-and-up">
            <Logo />
        </div>

        <!-- ThemeToggler -->
        <ThemeToggler />

        <!-- ---------------------------------------------- -->
        <!-- ShoppingCart -->
        <!-- ---------------------------------------------- -->
        <!-- <v-btn icon class="custom-hover-primary hidden-sm-and-down" size="small"  variant="text" color="primary" to="">
            <v-badge color="error" :content="0">
                <Icon icon="solar:cart-large-2-outline" height="22"   />
            </v-badge>
        </v-btn> -->

        <!-- ---------------------------------------------- -->
        <!-- Notification -->
        <!-- ---------------------------------------------- -->
        <!-- <div class="hidden-sm-and-down">
            <NotificationDD />
        </div>
         -->
        <!-- ---------------------------------------------- -->
        <!-- User Profile -->
        <!-- ---------------------------------------------- -->
        <div class="hidden-sm-and-down">
            <ProfileDD />
        </div>

        <!----Mobile ----->
        <v-menu :close-on-content-click="true" class="mobile_popup">
            <template v-slot:activator="{ props }">
                <v-btn icon class="hidden-md-and-up custom-hover-primary" color="primary" variant="text" v-bind="props" size="small">
                    <Icon icon="solar:menu-dots-bold-duotone" height="22" />
                </v-btn>
            </template>
            <v-sheet rounded="lg" elevation="10" class="px-4 py-3 mt-4 dropdown-box">
                <div class="d-flex justify-space-between align-center">
                    <RightMobileSidebar />
                    <v-btn icon variant="text" class="mr-2 mr-sm-3 custom-hover-primary" to="/ecommerce/checkout" size="small">
                        <v-badge color="primary" content="0" offset-x="-4" offset-y="-6">
                            <Icon icon="solar:cart-large-2-outline" height="22" />
                        </v-badge>
                    </v-btn>
                    <NotificationDD />
                    <ProfileDD />
                </div>
            </v-sheet>
        </v-menu>
    </v-app-bar>
</template>
