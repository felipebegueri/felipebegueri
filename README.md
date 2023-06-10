<!DOCTYPE html>
<html>
<head>
  <title>My Shooter Game</title>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/phaser/3.6.2/phaser.min.js"></script>
</head>
<body>
  <canvas width="800" height="600"></canvas>
  <script>
    var game = new Phaser.Game(800, 600, Phaser.AUTO);
    var player = new Phaser.Sprite(game, 400, 300);
    player.body.collideWorldBounds = true;
    var bullets = [];
    game.input.onDown.add(function () {
      var bullet = new Phaser.Sprite(game, player.x, player.y);
      bullet.body.velocity.x = 100;
      bullets.push(bullet);
    });
    game.physics.world.on(Phaser.Physics.P2.COLLISION_BEGIN, function (event) {
      if (event.other.type === "bullet") {
        event.other.destroy();
      }
    });
    game.render.onUpdate.add(function () {
      for (var i = 0; i < bullets.length; i++) {
        bullets[i].x += bullets[i].body.velocity.x;
        if (bullets[i].x < 0 || bullets[i].x > game.width) {
          bullets[i].destroy();
        }
      }
    });
  </script>
</body>
</html>
