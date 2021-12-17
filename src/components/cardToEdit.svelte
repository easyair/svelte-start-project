<script>
    import Btn from "../elements/btn.svelte";
    import { createEventDispatcher } from 'svelte';
    const dispatch = createEventDispatcher();
    
    export let cardName = ""
    export let cardSurname = ""
    export let cancelEditButton
    export let disableSaveEditButton = true

    
</script>
<div class="card">
    <div class="new">
      <label for="name">Имя</label>
      <input type="text"  name="name"
       bind:value={cardName}
       on:input
      >
    </div>
    <div class="new">
      <label for="surname">Фамилия</label>
      <input type="text" name="surname"
       bind:value={cardSurname}
       on:input 
      >
    </div>
    <div >
       <Btn
        btnText="Сохранить" 
        on:click={ () => dispatch ('clickedAgree')}
        clickable = {disableSaveEditButton}
       />
       <Btn
        btnText={cancelEditButton} 
        on:click={ () => dispatch ('clickedCancel')}
       />
    </div>
  </div>

<style>
.card{
    margin-left: 25px;
    background: #999999;
    box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
    border-radius: 5px;
    padding: 10px 20px;   
    height: 130px;
    width: 320px;
    min-width: 320px;
}

.new{
    width: 100%;
    display: flex;
    justify-content: space-between;
    margin: 10px 10px 10px 0;
    align-items: center;
    font-size: 10px;
    line-height: 10px;
}

.new label{
    margin-right: 10px;
    width: 30%;
}

.new input{
    background: #D5D5D5;
    border-radius: 5px;
    padding: 5px 10px;
    border: none;
    font-size: 10px;
    color: #000000;
    width: 100%;
    border: 1px solid #D5D5D5;

}
.new input:hover,
.new input:focus {
    border: 1px solid #404040;
    outline: none;
}
</style>