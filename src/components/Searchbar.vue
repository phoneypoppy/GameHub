<template>
    <div>
        <input type="search" class="searchbar">
    </div>
</template>


<script>
const filters = [
    'HVAC',
    'Overhead Doors'
]
export default {
    data() {
        return {
            filters
        }
    }
}
</script>

<style lang="scss" scoped>
.searchbar{
     
    .wrapper{
            max-width:900px;
            width:100%;
            padding:15px 30px;
        }
        
        .wrapper .input{
            width:100%;
            padding: 15px 20px;
            border-radius: 5px;
            font-weight: bold;
        }
}
</style>