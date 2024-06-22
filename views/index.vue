<template>
   <AppButton @click="log">
    add to favorites
    <Icon/>
   </AppButton>
</template>

<script>
import AppButton from "./components/AppButton";
import Icon from './components/Icon'
export default {
    components:{
        AppButton,
        Icon
    },
    methods:{
        log(){
            console.log("works");
        }
    }
};
</script>