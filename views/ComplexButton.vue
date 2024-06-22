<template>
    <button
    class="button"
    :disable="disabled"
    :class="{
        primary: primary,
        secondary:secondary,
        error:error
    }"
    >
    <template v-if="!error">
        <template v-if="loading">
            <Icon :color="!disabled ? defaultIconColor:
            loadingIconColor"/>
            {{ loadingtext }}
        </template>
        <template v-else>
            <Icon
            v-if="showLeftIcon"
            :color="!disabled ? defaultIconColor:
            loadingIconColor"
            :name="leftIconName" 
            />
            {{ text }}
            <Icon
            v-if="showRightIcon"
            :color="!disabled ? defaultIconColor:
            rightIconColor"
            :name="leftIconName"
            /> 
        </template>
    </template>
    <template v-else>
        {{ errorText }}
    </template>
    </button>
</template>
<script>
export default {
    props:[
        "text",
        "loadingtext",
        "errorText",
        "primary",
        "secondary",
        "disabled",
        "loading",
        "error",
        "loadingIconColor",
        "leftIconName",
        "rightIconName",
        "showLeftIcon",
        "leftIconColor",
        "showRightIcon",
        "rightIconColor"
    ]
};
</script>