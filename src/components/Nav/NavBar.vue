<template>
    <nav>
        <breadcrumb :items="breadcrumb" :title="title"/>
        <button class="leave-btn">
            <i class="bi bi-arrow-bar-right"></i>
        </button>
    </nav>
</template>

<script>
import Breadcumb from './Breadcumb/Breadcumb.vue';
export default {
    components: {Breadcumb},
    props: {
        breadcrumb: {
            type: Array,
            default: ''
        },
        title: {
            type: String, 
            default: ''
        }
    },
}
</script>

<style scoped>
nav {
    background-color: var(--body-color);
    height: 60px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 0 2rem;
}

.leave-btn {
    background-color: transparent;
    padding: .5rem;
    border: none;
    cursor: pointer;
}

.leave-btn i{
    color: red !important;
    font-weight: bold;
    font-size: 18px;
}
</style>