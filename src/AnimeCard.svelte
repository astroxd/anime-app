<script>
    export let id;
    export let title;
    export let cover;
    export let url;


</script>


<div class="anime-card">
    <a href="{url}" class="content" target="_blank">
        <img src="{cover}" alt="{title} cover">
        <h3>{title}</h3>
    </a>
</div>


<style>
    .anime-card{
        width: 200px; 
        max-width: 200px;
        margin: 1rem;
    }
    .content{
        text-overflow: ellipsis;
        word-wrap: break-word;
        line-height: 1.2em;
    }

    img{
        width: 200px;
        height: 300px;
    }
    h3{
        margin: 0;
    }

</style>