<template>
    <div id="head"> 
        <h1>Games</h1>
        <!-- <input type="text" value=""> -->
        <select name="order">
            <option value="pop">Mais populares</option>
            <option value="exp">Maiores valores</option>
            <option value="che">Menores valores</option>
            <option value="alf">Ordem Alfabética</option>
        </select>
    </div>
</template>

<script>
export default {

    
}
</script>

<style scoped>
    #head{
    display: flex;  
    align-items: center; 
    justify-content: space-between; 
    margin-bottom: 30px;
    }
    select{
        text-align: center;
        width: 262px;
        height: 40px;
        border-radius: 4px;
    }
    h1 {
        font-size: 48px;
    }
</style>