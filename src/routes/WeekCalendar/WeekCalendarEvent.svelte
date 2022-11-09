<svelte:head><link rel="stylesheet" href="../styles.css" /></svelte:head>
<script lang="ts">
    import { onMount } from 'svelte';
    export let event_id : string = "week-calendar-event-" + (Math.random() * 10000).toString().split('.')[0];
    export let day : number = 0;
    export let start_hour : number = 0;
    export let end_hour : number = 0;
    export let start_minute : number = 0;
    export let end_minute : number= 0;
    let rect_left : number;
    let rect_right : number;
    let rect_bottom : number;
    let rect_top : number;
    let rect_width : number;
    let rect_height : number;
    let hour_height : number = 0;


    let hour_paddings : any[][] = [];
    let bodyRect : any;
    try {
    onMount(() => {
        /*for (let i : number = 0; i < 7; i++) {
            hour_paddings.push([]);
            for (let j : number = 0; j <= 24; j++) {
                hour_paddings[i].push(document.getElementById("hour-padding-" + i + "-" + j));
            }
        }*/
        bodyRect = document.body.getBoundingClientRect();
        let e1 = document.getElementById("hour-padding-" + day + "-" + start_hour);
        let e1_after = document.getElementById("hour-padding-" + day + "-" + (start_hour + 1));
        let e2 = document.getElementById("hour-padding-" + day + "-" + end_hour);
        if (e1 != null && e2 != null && e1_after != null) {
            let e1_rect = e1.getBoundingClientRect();
            let e1_after_rect = e1_after.getBoundingClientRect();
            let e2_rect = e2.getBoundingClientRect();
            hour_height = e1_after_rect.top - e1_rect.top;
            rect_top = e1_rect.top + (hour_height * (start_minute/60));
            rect_bottom = e2_rect.top + (hour_height * (end_minute/60));
            rect_left = e1_rect.left;
            rect_right = e1_rect.right;
            rect_width = rect_right - rect_left;
            rect_height = rect_bottom - rect_top;
            let event_e_style = document.getElementById(event_id).style;
            if (event_e_style != null) {
                console.log("ELEMENT E STYLE" + event_e_style);
                //event_e_style.position = "fixed";
                //event_e_style.paddingTop = rect_top.toString();
                console.log(event_e_style.paddingTop + "," + rect_top.toString() + "," + rect_top);
                //event_e.style.right = rect_right.toString();
                //event_e_style.paddingLeft = rect_left.toString();

                //event_e.style.bottom = rect_bottom.toString();
            }

            console.log("WeekCalendarEvent Log :" + rect_top + "," + rect_bottom + "," + rect_right + "," + rect_left);
        }
        else {
            console.log("e1 e1_after and e2 are null in WeekCalendarEvent.svelte");
        }
        
        /*function GetLocation(d : number, h:number, m:number) : Array<number> {
            let frac = m/60;
            //let element = document.getElementById("hour-padding-" + d + "-" + h);
            //let element2 = document.getElementById("hour-padding-" + d + "-" + (h + 1));
            let element = hour_paddings[d][h];
            let element2 = hour_paddings[d][h + 1];
            //let bodyRect = document.body.getBoundingClientRect();
            console.log("Element " + element + ", Element2 " + element2);

            if (element != null && element2 != null) {
                let elemRect = element.getBoundingClientRect();
                let elemRect2 = element2.getBoundingClientRect();
                console.log("ElementRect " + elemRect + ", Element2Rect " + elemRect2);
                let offset = elemRect.top - bodyRect.top;
                let offset2 = elemRect2.top - bodyRect.top;
                hour_height = elemRect2.top - elemRect.top;
                console.log("Offset : " + offset);
                return [elemRect.top + (hour_height * (m/60)), elemRect.left, elemRect.right];
            }
            return [];
        }
        let location_1 = GetLocation(day, start_hour, start_minute);
        let location_2 = GetLocation(day, end_hour, end_minute);
        rect_top = location_1[0];
        rect_bottom = location_2[0];
        rect_left = location_1[1];
        rect_right = location_1[2];
        console.log("WeekCalendarEvent Log :" + rect_top + "," + rect_bottom + "," + rect_right + "," + rect_left);*/
    });
    }
    catch(error) {
        console.log("ERROR : " + error);
    }
    // left:{rect_left}; right:{rect_right}, top:{rect_top}, bottom:{rect_bottom}
</script>

<div id={event_id} class="week-calendar-event" style="position:absolute;top:{rect_top}px;left:{rect_left}px;width:{rect_width}px;height:{rect_height}px;">
    <p class="text-center">Event Name</p>
</div>

<style>
    .week-calendar-event {
        background-color: red;
        border-radius: 10px;
    }
</style>
