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
    .sideline__dot--1 {
        top: 0
    }
    .sideline__dot--2 {
        top: calc(90vh / 5 - 17.5px)!important;
    }
    .sideline__dot--3 {
        top: calc(90vh / 5 * 2 - 17.5px)!important;
    }
    .sideline__dot--4 {
        top: calc(90vh / 5 * 3 - 17.5px)!important;
    }
    .sideline__dot--5 {
        top: calc(90vh / 5 * 4 - 17.5px)!important;
    }
    .sideline__dot--6 {
        bottom: 0
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
            top 0.1 s ease;
        z-index: 10;
    }
</style>

<script>
    let slideInit = false;

    function getDocumentHeight() {
        var body = document.body,
            html = document.documentElement;
        return Math.max( body.scrollHeight, body.offsetHeight, 
            html.clientHeight, html.scrollHeight, html.offsetHeight );
    }

    window.addEventListener('scroll', function(e) {
        const windowHeight = document.documentElement.clientHeight;
        const documentHeight = getDocumentHeight();
        const portion = window.scrollY / documentHeight;
        const slider = document.getElementById('slider');
        slider.style.top = 
            /* 90vh * portion */ (windowHeight / 10 * 9 * portion) + 'px';
    });

    var posY1 = 0, posY2 = 0;

    function dragStart(e) {
        if (!slideInit) {
            slideInit = true;
            const slider = document.getElementById('slider');
            slider.addEventListener('touchstart', dragStart);
            slider.addEventListener('touchend', dragEnd);
            slider.addEventListener('touchmove', dragAction);
        }
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
        let newTop = (posY1 - height / 20 - 7.5);
        let portion = newTop / (height / 10 * 9);
        console.log(portion +' '+ getDocumentHeight());
        if (newTop >= 0 && newTop <= (height / 10 * 9 - 15)) {
            slider.style.top = newTop + "px";
            window.scrollTo(0, getDocumentHeight() * portion);
        }
    }
   
    function dragEnd (e) {
        document.onmouseup = null;
        document.onmousemove = null;
    }

    function allowSlide(e) {
        e.preventDefault();
    }
</script>

<div class="sideline__container">
    <div class="sideline__line"></div>
    <div class="sideline__dot sideline__dot--1"></div>
    <div class="sideline__dot sideline__dot--2"></div>
    <div class="sideline__dot sideline__dot--3"></div>
    <div class="sideline__dot sideline__dot--4"></div>
    <div class="sideline__dot sideline__dot--5"></div>
    <div class="sideline__dot sideline__dot--6"></div>
    <div id="slider" class="sideline__slider" on:mousedown={dragStart}></div>
</div>