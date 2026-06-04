<!DOCTYPE html>
<html>
<head>
    <title>Simple Shooting Game</title>
</head>
<body>
<canvas id="game" width="800" height="500"></canvas>

<script>
const canvas = document.getElementById("game");
const ctx = canvas.getContext("2d");

let player = {
    x: 380,
    y: 450,
    width: 40,
    height: 40
};

let bullets = [];

document.addEventListener("keydown", (e) => {
    if (e.key === "ArrowLeft") player.x -= 20;
    if (e.key === "ArrowRight") player.x += 20;

    if (e.key === " ") {
        bullets.push({
            x: player.x + 18,
            y: player.y
        });
    }
});

function update() {
    bullets.forEach(b => b.y -= 10);
}

function draw() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);

    // Player
    ctx.fillStyle = "blue";
    ctx.fillRect(player.x, player.y, player.width, player.height);

    // Bullets
    ctx.fillStyle = "red";
    bullets.forEach(b => {
        ctx.fillRect(b.x, b.y, 5, 10);
    });
}

function gameLoop() {
    update();
    draw();
    requestAnimationFrame(gameLoop);
}

gameLoop();
</script>
</body>
</html>
