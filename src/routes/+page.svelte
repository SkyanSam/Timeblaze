<svelte:head><link rel="stylesheet" href="styles.css" /></svelte:head>
<script type="ts">
	import { src_url_equal } from 'svelte/internal';
	import WeekCalendarDay from './WeekCalendar/WeekCalendarDay.svelte';
    import Pomodoro from './Pomodoro/Pomodoro.svelte';
    function DayOfWeek(num : number) {
        switch(num) {
            case 0: return "Sunday"; break;
            case 1: return "Monday"; break;
            case 2: return "Tuesday"; break;
            case 3: return "Wednesday"; break;
            case 4: return "Thursday"; break;
            case 5: return "Friday"; break;
            case 6: return "Saturday"; break;
            default: return "Saturday"; break;
        }
    }
    function BoxesFloat(num : number, total : number) {
        if (num == total - 1) return "float-right";
        else return "float-left";
    }
</script>

<div class="flexbox">
    <div class="flexbox" style="width:50%;">
    {#each Array(7) as _, day_index (day_index)}
        <svelte:component this={WeekCalendarDay} day_index={day_index}/>
        <div class="day-padding float-left"></div>
    {/each}
    </div>
    <div class="flexbox" style="width:50%;height:100vh;">
        <svelte:component this={Pomodoro}></svelte:component>
    </div>
</div>
<style>
    .day-padding {
        padding-right:2px;
        padding-bottom:100%;
        background-color:gray;
    }
    .float-left {
        float:left;
    }
    .float-right {
        float:right;
    }
</style>

