<style>
    .navbar {
        height: 70px;
    }
    .navbar__section {
        display: flex;
        align-items: center;
        width: calc(50% - 120px);
        height: 70px;
    }
    .navbar__section--left {
        float: left;
        justify-content: flex-end
    }
    .navbar__section--right {
        float: right;
        justify-content: flex-start
    }
    .navbar__logo {
        margin-top: 20px;
        display: inline-block;
        position: absolute;
        left: calc(50% - 93px);
        font-family: 'Raleway', sans-serif;
        font-weight: 800;
        text-transform: uppercase;
        font-size: 25px;
    }
    .navbar__icons {
        float: right;
        margin-right: 20px;
        display: flex;
        flex-grow: 1;
        justify-content: flex-end;
        font-family: 'Raleway', sans-serif
    }
    .navbar__icons_item {
        margin-left: 20px
    }

    .navbar__menu {
        margin: 0;
        padding: 0;
        display: inline-grid;
        grid-column-gap: 20px;
        grid-template-columns: repeat(3, auto); 
        font-family: 'Raleway', sans-serif;
    }
    .navbar__menu_item {
        display: inline-grid;
        grid-template-columns: repeat(2, auto);
    }

    .watermark {
        position: fixed;
        bottom: 10px;
        left: calc(50% - 17.5px);
        width: 35px;
        height: 35px;
        opacity: 0.2;
    }
    
</style>

<nav class="navbar">
    <div class="navbar__section navbar__section--left">
        <ul class="navbar__menu">
            <li class="navbar__menu_item">Hero</li>
            <li class="navbar__menu_item">Me</li>
            <li class="navbar__menu_item">Abilities</li>
        </ul>
    </div>
    <span class="navbar__logo">dany.dolphin</span>
    <div class="navbar__section navbar__section--right">
        <ul class="navbar__menu">
            <li class="navbar__menu_item">Portfolio</li>
            <li class="navbar__menu_item">Top 10</li>
            <li class="navbar__menu_item">Social Media</li>
        </ul>
        <div class="navbar__icons">
            <span class="navbar__icons_item">EN</span>
            <span class="navbar__icons_item">
                <i class="fas fa-umbrella-beach"></i>
            </span>
        </div>
    </div>
</nav>

<img src="data:image/gif;base64,R0lGODlhAQABAIAAAAUEBAAAACwAAAAAAQABAAACAkQBADs=" alt="DanyDolhin" class="watermark">