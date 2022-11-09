<svelte:head><link rel="stylesheet" href="../styles.css" /></svelte:head>
<script type="ts">
    import WeekCalendarEvent from './WeekCalendarEvent.svelte';
    export let day_index = 0;
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
</script>

<div class="float-left week-calendar-day">
    <div>
        <p style="text-align: center">{day_index}</p>
        <p style="text-align: center">{DayOfWeek(day_index)}</p>
    </div>
    {#each Array(24) as _, hour_index (hour_index)}
        <div id=hour-padding-{day_index}-{hour_index} class="hour-padding"></div>
        <div class="hour"></div>
    {/each}
    <div id=hour-padding-{day_index}-24 class="hour-padding"></div>
</div>

<svelte:component this={WeekCalendarEvent} day={day_index} start_hour={day_index * 2} end_hour={(day_index * 2)+1} start_minute={30} end_minute={45}/>

<style>
    .hour {
        padding-bottom:2px;
        background-color:gray;
    }
    .hour-padding {
        padding-bottom:50px;
        color:white;
        background-color:white;
    }
    .float-left {
        float:left;
    }
    .week-calendar-day {
        width:14.28%;
    }
</style>