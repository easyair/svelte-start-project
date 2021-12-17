<script>
  export let selected
  export let throughtText 
  export let mainText
  export let clickOnAdd = false
</script>
<div 
  class:throught-text="{!!selected && (throughtText != mainText)}"
  class:italic ="{clickOnAdd}"
  {throughtText}
>
  {mainText}
</div>

<style>

  .throught-text{
    font-style: italic;
  }    
  .throught-text::before{
    content: attr(throughtText);
    text-decoration: line-through;
  }

  .italic{
    font-style: italic;
  }  
</style>