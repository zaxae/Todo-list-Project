<template>
    <button>
        <slot></slot>
    </button>
</template>

<script>
export default {
    name: 'TodoBtn'
}
</script>

<style scoped>
button {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 4px;
    text-align: center;
    border-radius: 4px;
    cursor: pointer;
    opacity: 0.9;
    background: none rgba(255, 255, 255, 0.2);
    box-shadow: none;
    font-size: 12px;
    padding: 4px 10px;
    min-width: 70px;
    border: none;
    color: white !important;
    letter-spacing: .5px;
}
</style>