<script>
 export let btnText = "undefined"
 export let clickable = false
</script>

<button 
 disabled={clickable} 
 on:click>{btnText}
</button>

<style>
    
button{
    font-size: 10px;
    line-height: 12px;
    padding: 5px 10px;
    border-radius: 5px;
    background: #D5D5D5;
    cursor: pointer;
    border: 1px solid #D5D5D5;
}

button:hover{
    border: 1px solid #909090;
}

button:active{
    background: #D5D5D5;
    border: 1px solid #909090;
    box-sizing: border-box;
    box-shadow: inset 0px 2px 6px rgba(0, 0, 0, 0.25);
}

button:disabled{
    color: rgba(0, 0, 0, 0.45);
    cursor: default;
}

</style>

