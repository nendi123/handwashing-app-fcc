<script>

    import ProgressBar from './ProgressBar.svelte'

    const totalSecond = 20
    let secondLeft = totalSecond
    let isRunning = false
    $: progress = ((totalSecond - secondLeft) / totalSecond) * 100

    function startTimer(){
        isRunning = true
        const timer = setInterval(() => {
        secondLeft -= 1
        if(secondLeft == 0){
            clearInterval(timer)
            isRunning = false
            secondLeft = totalSecond
        }
    }, 1000)
    }
    
</script>

<style>
    h2 {
        margin: 0;
    }
    .start{
        background-color: rgb(154, 73, 73);   
        width: 100%;
        margin: 10px 0;
    }
    .start[disabled]{
        background-color: rgb(197, 197, 197);
        cursor: not-allowed;
    }
</style>
<div bp="grid">
    <h2 bp="offset-5@md 4@md 12@sm">
        Second Left : {secondLeft}
    </h2>
</div>
<ProgressBar progress={progress}/>
<div bp="grid">
    <button disabled="{isRunning}" class="start" bp="offset-5@md 4@md 12@sm" on:click="{startTimer}">
        Start
    </button>
</div>
