<template>
<div class="demo">
<span v-for="n in 10">{{ n }} ; </span>

<ul> <li v-for="item in items">{{ item }}</li> </ul>
</div>
</template>

<script>
export default {
    data(){
        return {
            items: ["apple","kiwi","mango"]
        }
    }
}
</script>
