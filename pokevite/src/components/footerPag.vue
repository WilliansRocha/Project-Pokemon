<template>
    <div>
        <footer class="bg-primary text-light"> 
            <div>
               &copy; Willians Rocha {{ new Date().getFullYear() }}
            </div>
        </footer>
    </div>
</template>

<script>
    export default{
        name: 'teste'
    }
</script>

<style>
    footer{
       position: fixed;
       bottom: 0;
       width: 100%;
       display: flex;
       align-items: center;
       justify-content: center;
       height: 56px; 
    }

</style>