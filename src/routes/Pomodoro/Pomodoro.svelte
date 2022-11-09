<svelte:head><link rel="stylesheet" href="../styles.css" /></svelte:head>

<script lang="ts">
    let min_remaining = 60;
    let sec_remaining = 0;
    let pomodoro_min = 40;
    let short_break_min = 10;
    let long_break_min = 20;
    function Make2Length(n : any) {
        let n_string = n.toString();
        if (n_string.length == 1) return "0" + n_string;
        return n_string;
    }
    let pomodoro_button_class = "pomo-state-button-on";
    let short_break_button_class = "pomo-state-button-off";
    let long_break_button_class = "pomo-state-button-off";
    enum PomoState {
        Pomodoro,
        ShortBreak,
        LongBreak
    }
    function ChangeState(state : PomoState) {
        switch(state) {
            case PomoState.Pomodoro:
                pomodoro_button_class = "pomo-state-button-on";
                short_break_button_class = "pomo-state-button-off";
                long_break_button_class = "pomo-state-button-off"; 
                min_remaining = pomodoro_min;
                sec_remaining = 0;
                break;
            case PomoState.ShortBreak:
                pomodoro_button_class = "pomo-state-button-off";
                short_break_button_class = "pomo-state-button-on";
                long_break_button_class = "pomo-state-button-off";  
                min_remaining = short_break_min;
                sec_remaining = 0;
                break;
            case PomoState.LongBreak:
                pomodoro_button_class = "pomo-state-button-off";
                short_break_button_class = "pomo-state-button-off";
                long_break_button_class = "pomo-state-button-on"; 
                min_remaining = long_break_min;
                sec_remaining = 0; 
                break;
        }
    }
    function ChangeStatePomodoro() {ChangeState(PomoState.Pomodoro);}
    function ChangeStateShortBreak() {ChangeState(PomoState.ShortBreak);}
    function ChangeStateLongBreak() {ChangeState(PomoState.LongBreak);}
    ChangeState(PomoState.Pomodoro);
</script>

<div class="pomo-background float-clear">
    <div class="center pomo-element float-clear" style="flex-direction:column;">
        <div style="flex-direction:row;">
        <button class="{pomodoro_button_class}" on:click={ChangeStatePomodoro}>Pomodoro</button>
        <button class="{short_break_button_class}" on:click={ChangeStateShortBreak}>Short Break</button>
        <button class="{long_break_button_class}" on:click={ChangeStateLongBreak}>Long Break</button>
        </div>
        <p style="font-size:100px;">{Make2Length(min_remaining)}:{Make2Length(sec_remaining)}</p>
        <button>Start</button>
    </div>
</div>

<style>
    .pomo-background {
        background-color:red;
        width:100%;
        height:100%;
    }
    .pomo-element {
        background-color:pink;
        margin-top:25%;
        margin-left:25%;
        width:50%;
        height:50%;
    }
    .pomo-state-button-on {
        background-color: red;
        border: none;
        border-radius:10px;
        color: white;
        padding: 5px 10px;
        text-align: center;
        text-decoration: none;
        display: inline-block;
        font-size: 16px;
        font-weight: bold;
    }
    .pomo-state-button-off {
        background-color: transparent;
        border: none;
        border-radius:10px;
        color: white;
        padding: 1px 3px;
        text-align: center;
        text-decoration: none;
        display: inline-block;
        font-size: 16px;
        font-weight: normal;
    }
    .float-clear {
        float:inherit;
    }
</style>