<template>
    <div class="progress">
        <div class="progress_bar" :style="{width:myProgress}"></div>
    </div>
</template>

<script>
    export default {
        props:['myProgress']
    }
</script>

<style>
    .data_header .progress {
        width: 200px;
        height: 18px;
        margin: 0px 8px;
        background: #e2e0e0;
        border-radius: 12px;
    }
    .data_header .progress .progress_bar {
        height: 18px;
        background: #61aef8;
        border-radius: 12px;
    }
</style>

