<script>
 import stages from ".././data.json";
 export let count;
 let image = stages[count].img;
</script>
<div>
{count}
<img src={image} alt="">
</div>
