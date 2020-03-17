<script>
    import { onMount, afterUpdate } from 'svelte';

    export let sections = [];
    let currentSection = 0;
    let sidelineSectionHeight = 0;
    let accumulatedHeight = 0;

    $: initVariables(sections);

    function getDocumentHeight() {
        var body = document.body,
            html = document.documentElement;
        return Math.max( body.scrollHeight, body.offsetHeight, 
            html.clientHeight, html.scrollHeight, html.offsetHeight );
    }

    function initSlider() {
        const slider = document.getElementById('slider');
        slider.addEventListener('touchstart', dragStart);
        slider.addEventListener('touchend', dragEnd);
        slider.addEventListener('touchmove', dragAction);
        initVariables();
    }

    function initVariables() {
        const slider = document.getElementById('slider');
        if (slider !== null && sections.length > 0) {
            syncDragOnScroll();
            let st = slider.style.top;
            let newTop = Number(st.substring(0, st.indexOf('px'))) + 7.5;
            let height = document.documentElement.clientHeight;
            sidelineSectionHeight = height / 10 * 9 / sections.length;
            currentSection = 0;
            accumulatedHeight = 0;
            while(sidelineSectionHeight * currentSection > newTop
                ||sidelineSectionHeight * (currentSection + 1) <= newTop) {
                accumulatedHeight += sections[currentSection++].offsetHeight;
            }
        }
    }

    function syncDragOnScroll(e) {
        const windowHeight = document.documentElement.clientHeight;
        const documentHeight = getDocumentHeight() - windowHeight;
        if (window.scrollY > accumulatedHeight + sections[currentSection].offsetHeight) {
            accumulatedHeight += sections[currentSection++].offsetHeight;
        } else if (window.scrollY < accumulatedHeight) {
            accumulatedHeight -= sections[--currentSection].offsetHeight
        }
        const portion = (window.scrollY - accumulatedHeight)
            / (sections[currentSection].offsetHeight - (currentSection === sections.length - 1 ? windowHeight - 70 : 0));
        const slider = document.getElementById('slider');
        console.log(portion);
        slider.style.top = (sidelineSectionHeight * (currentSection + portion) - 7.5) + 'px';
    }

    function dragStart(e) {
        e = e || window.event;
        e.preventDefault();
        document.onmouseup = dragEnd;
        document.onmousemove = dragAction;
    }

    function dragAction (e) {
        e = e || window.event;
        let posY1 = 0;
        if (e.type == 'touchmove') {
            posY1 = e.touches[0].clientY;
        } else {
            posY1 = e.clientY;
        }
        let slider = document.getElementById('slider');
        let height = document.documentElement.clientHeight;
        let newTop = (posY1 - height / 20);
        if (newTop >= 0 && newTop <= (height / 10 * 9)) {
            slider.style.top = (newTop - 7.5) + "px";
            window.removeEventListener('scroll', syncDragOnScroll);
            if (newTop > sidelineSectionHeight * (currentSection + 1)) {
                accumulatedHeight += sections[currentSection++].offsetHeight;
            } else if (newTop <= sidelineSectionHeight * (currentSection)) {
                accumulatedHeight -= sections[--currentSection].offsetHeight;
            }
            //which section height portion do i barrel?
            let portion = (newTop - (sidelineSectionHeight * currentSection))
                / sidelineSectionHeight;
            //where do i scroll?
            let scrollTo = accumulatedHeight + 
                (sections[currentSection].offsetHeight - (currentSection === sections.length - 1 ? height : 0)) * portion;
            //let it scroll!!
            window.scrollTo(0, scrollTo);
        }
    }
   
    function dragEnd (e) {
        document.onmouseup = null;
        document.onmousemove = null;
        window.addEventListener('scroll', syncDragOnScroll);
    }

    function allowSlide(e) {
        e.preventDefault();
    }

    function moveToSection(section) {
        currentSection = section;
        accumulatedHeight = 0;
        let i = 0;
        while (i < section)
            accumulatedHeight += sections[i++].offsetHeight;
        window.scrollTo(0, accumulatedHeight);
    }

    window.addEventListener('scroll', syncDragOnScroll);
    onMount(initSlider);
</script>

<style>
    .sideline__container {
        position: fixed;
        height: 90vh!important;
        width: 30px;
        top: 5vh;
        left: 45px;
    }
    .sideline__dot {
        width: 30px;
        height: 30px;
        border-radius: 30px;
        border: 2px solid #383838;
        background-color: #383838;
        position: absolute;
        cursor: pointer;
        transition: background-color 0.3s ease;
        z-index: 5;
    }
    .sideline__dot:hover, .sideline__slider:hover {
        background-color: white
    }
    .sideline__dot_tooltip {
        position: absolute;
        top: 5px;
        left: 31px;
        text-transform: uppercase;
        font-family: 'Raleway', sans-serif;
        font-weight: 800;
        opacity: 0;
        transition: opacity 0.2s ease-in,
                    left 0.2s ease-in;

    }
    .sideline__dot:hover .sideline__dot_tooltip, .sideline__dot_tooltip.hover {
        opacity: 1;
        left: 41px;
    }
    .sideline__line {
        width: 1px;
        height: 90vh!important;
        background-color: #383838;
        position: relative;
        left: 16px
    }
    .sideline__slider {
        width: 15px;
        height: 15px;
        position: absolute;
        left: 6.5px;
        top: 0;
        cursor: pointer;
        background-color: #535353;
        border: 2px solid #535353;
        border-radius: 15px;
        transition: background-color 0.3s ease,
            top 0.1s ease;
        z-index: 10;
    }
    .sideline__end {
        position: absolute;
        bottom: -5px;
        width: 34px;
        height: 10px;
        background-color: #535353;
    }
</style>

<div class="sideline__container">
    <div class="sideline__line"></div>
    {#each sections as section, i}
    <div class="sideline__dot" style="top: calc(90vh / {sections.length} * {i} - 17.5px)"
        on:click={() => moveToSection(i)}>
        <span class="sideline__dot_tooltip">{section.dataset.title}</span>
    </div>
    {/each}
    <div id="slider" class="sideline__slider" on:mousedown={dragStart}></div>
    <div class="sideline__end"></div>
</div>