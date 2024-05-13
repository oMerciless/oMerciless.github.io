<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Text Typing Animation</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div class="animated-text">
        I'm a <span></span>
    </div>
</body>
</html>

body{
    margin: 0;
    padding: 0;
    background-color: #2f3542;
    color: #fff;
    height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
    font-family: "Montserrat", sans-serif;
}

.animated-text{
    font-size: 34px;
    font-weight: 600;
    min-width: 280px;
}

.animated-text span{
    position: relative;
}

.animated-text span::before{
    content: "Youtuber";
    color: #ff7f50;
    animation: words 20s infinite;
}

.animated-text span::after{
    content: "";
    position: absolute;
    width: calc(100% + 8px);
    height: 100%;
    background-color: #2f3542;
    border-left: 2px solid #ff7f50;
    right: -8px;
    animation: cursor .8s infinite, typing 20s steps(14) infinite;
}

@keyframes cursor {
    to{
        border-left: 2px solid #ff7f5000;
    }
}

@keyframes words {
    0%,20%{
        content: "Youtuber";
    }
    21%,40%{
        content: "Blogger";
    }
    41%,60%{
        content: "Developer";
    }
    61%,80%{
        content: "Designer";
    }
    81%,100%{
        content: "Gamer";
    }
}

@keyframes typing {
    10%,15%,30%,35%,50%,55%,70%,75%,90%,95%{
        width: 0;
    }
    5%,20%,25%,40%,45%,60%,65%,80%,85%{
        width: calc(100% + 8px);
    }
}
