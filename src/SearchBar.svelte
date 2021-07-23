<div>
    <form class="search-box">
        <input type="search" placeholder="Search for anime...">
    </form>
</div>

<style>
    input{
        appearance: none;
        background: none;
        outline: none;
        border: none;
        

        display: block;
        width: 100%;
        max-width: 400px;
        padding: 16px;
        border-radius: 999px;
        background-color: #EEE;

        transition: var(--transition-speed);
    }

    input:focus{
        background-color: #313131;
        color: #FFF;
    }
    /* Small Screen */
    @media only screen and (max-width: 600px){
        input{
            margin:auto;
        }
    }

    /* Large Screen */
    @media only screen and (min-width: 600px){
        input{
            margin-left:auto;
        }
    }


</style>