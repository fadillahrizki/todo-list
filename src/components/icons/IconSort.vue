<template>
    <IconSortNewest v-if="type == 'IconSortNewest'" />
    <IconSortOldest v-else-if="type == 'IconSortOldest'" />
    <IconSortAz v-else-if="type == 'IconSortAz'" />
    <IconSortZa v-else-if="type == 'IconSortZa'" />
    <IconSortUnfinished v-else-if="type == 'IconSortUnfinished'" />
    <svg v-else width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
        <path d="M3 9L7 5M7 5L11 9M7 5V19" stroke="#888888" stroke-width="1.5" stroke-linecap="square" />
        <path d="M21 15L17 19M17 19L13 15M17 19V5" stroke="#888888" stroke-width="1.5" stroke-linecap="square" />
    </svg>
</template>

<script>
import IconBack from './IconBack.vue';
import IconSortNewest from './IconSortNewest.vue';
import IconSortOldest from './IconSortOldest.vue';
import IconSortAz from './IconSortAz.vue';
import IconSortZa from './IconSortZa.vue';
import IconSortUnfinished from './IconSortUnfinished.vue';
export default {
    props:['type'],
    components: { IconBack, IconSortNewest, IconSortOldest, IconSortAz, IconSortZa, IconSortUnfinished }
}
</script>