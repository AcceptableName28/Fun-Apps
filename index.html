<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Vespa Jump</title>
  <style>
    :root { --sky:#cfe9ff; --road:#2a2a2a; }
    html,body{height:100%;margin:0;background:var(--sky);font-family:system-ui,-apple-system,Segoe UI,Roboto,Helvetica,Arial,sans-serif}
    #wrap{display:grid;place-items:center;height:100%}
    canvas{background:linear-gradient(#cfe9ff, #a6d4ff 60%);box-shadow:0 10px 40px rgba(0,0,0,.25);border-radius:14px}

    .overlay{position:fixed;inset:0;display:flex;align-items:center;justify-content:center;background:rgba(255,255,255,.85);text-align:center}
    .card{background:#fff;border-radius:14px;box-shadow:0 12px 36px rgba(0,0,0,.2);padding:20px 28px}
    .btn{display:inline-block;background:#111;color:#fff;padding:10px 16px;border-radius:10px;font-weight:800;margin-top:10px}
    kbd{background:#111;color:#fff;border-radius:6px;padding:3px 6px;font-weight:700}
  </style>
</head>
<body>
  <div id="wrap">
    <canvas id="game" width="960" height="540" aria-label="Vespa Jump game"></canvas>
  </div>

  <!-- Start -->
  <div id="startScreen" class="overlay">
    <div class="card">
      <h1 style="margin:0 0 8px">🛵 Vespa Jump</h1>
      <div>Press <kbd>Space</kbd> or <kbd>↑</kbd> to jump. Press again mid-air for a double jump.<br/>After a crash, press <kbd>R</kbd> or click Restart.</div>
      <a href="#" id="startBtn" class="btn">Start</a>
    </div>
  </div>

  <!-- Game Over -->
  <div id="gameOver" class="overlay" style="display:none">
    <div class="card">
      <h2 style="margin:0 0 8px">Game Over</h2>
      <div>Score: <span id="finalScore">0</span> · Best: <span id="finalBest">0</span></div>
      <a href="#" id="restartBtn" class="btn">Restart (R)</a>
    </div>
  </div>

  <script>
    // ===== Canvas =====
    const canvas = document.getElementById('game');
    const ctx = canvas.getContext('2d');
    const W = canvas.width, H = canvas.height;

    // ===== UI =====
    const startScreen = document.getElementById('startScreen');
    const gameOverEl  = document.getElementById('gameOver');
    const startBtn    = document.getElementById('startBtn');
    const restartBtn  = document.getElementById('restartBtn');
    const finalScore  = document.getElementById('finalScore');
    const finalBest   = document.getElementById('finalBest');

    // ===== Sprite (your PNG) =====
    const vespaImg = new Image();
    vespaImg.src = 'Blue Vespa Right.png'; // <-- keep this file next to this HTML
    let vespaReady = false;
    vespaImg.onload = () => vespaReady = true;

    // ===== Physics / Tuning =====
    const floorY = H * 0.78;
    const gravity       = 0.9;    // faster fall for snappier feel
    const JUMP_VEL_1    = -14.5;  // tap jump
    const JUMP_VEL_2    = -12.2;  // second jump
    const COYOTE_FRAMES = 8;      // jump a few frames after leaving ground
    const BUFFER_FRAMES = 10;     // queue jump a few frames before landing

    // ===== World =====
    const world = {
      t: 0,
      speed: 8,
      baseSpeed: 8,
      maxSpeed: 18,
      score: 0,
      best: Number(localStorage.getItem('vespa_best') || 0),
      alive: false,
      spawnTimer: 0,
      spawnInterval: 80,
      difficultyTimer: 0
    };

    // ===== Input =====
    const keys = { up:false, space:false };
    const KEY  = { UP:38, SPACE:32, R:82 };

    // ===== Player =====
    const PLAYER_W = 120;  // scale matched to the earlier vector scooter
    const PLAYER_H = 80;
    const player = {
      x: W*0.18, y: floorY, vy: 0,
      w: PLAYER_W, h: PLAYER_H,
      onGround: true, jumps: 0,
      coyote: 0, jumpBuffer: 0, usedDouble: false
    };

    // ===== Obstacles =====
    const obstacles = [];
    function spawnObstacle(){
      const type   = Math.random() < 0.5 ? 'cone' : 'crate';
      const stacks = 1 + Math.floor(Math.random()*3);    // 1–3 high
      const w = type==='cone' ? 32 : 42;
      const h = type==='cone' ? 46 : 42;
      obstacles.push({ x: W+40, y: floorY - h, w, h, type, stacks });
    }

    // ===== State helpers =====
    function hardResetInput(){
      keys.up=false; keys.space=false; player.jumpBuffer=0;
    }
    function resetGame(){
      world.t=0; world.speed=world.baseSpeed; world.score=0;
      world.spawnTimer=0; world.spawnInterval=80; world.difficultyTimer=0;
      player.y=floorY; player.vy=0; player.onGround=true;
      player.jumps=0; player.usedDouble=false; player.coyote=0; player.jumpBuffer=0;
      obstacles.length=0; hardResetInput();
    }
    function startGame(){
      resetGame();
      world.alive = true;
      startScreen.style.display='none';
      gameOverEl.style.display='none';
    }
    function gameOver(){
      world.alive = false;
      finalScore.textContent = Math.floor(world.score);
      if(world.score > world.best){
        world.best = Math.floor(world.score);
        localStorage.setItem('vespa_best', world.best);
      }
      finalBest.textContent = world.best;
      gameOverEl.style.display = 'flex';
      hardResetInput();
    }

    // ===== Input handlers =====
    function keyHandler(e, down){
      if(e.keyCode===KEY.SPACE || e.keyCode===KEY.UP){
        if(down) e.preventDefault();
        if(e.keyCode===KEY.SPACE) keys.space = down; else keys.up = down;
        if(down && !world.alive){ startGame(); return; }     // start from menus
        if(down && world.alive){ player.jumpBuffer = BUFFER_FRAMES; } // buffer jump
      } else if(e.keyCode===KEY.R && down){
        startGame(); // always allow R to restart
      }
    }
    window.addEventListener('keydown', e=>keyHandler(e,true));
    window.addEventListener('keyup',   e=>keyHandler(e,false));
    startBtn.addEventListener('click',   e=>{ e.preventDefault(); startGame(); });
    restartBtn.addEventListener('click', e=>{ e.preventDefault(); startGame(); });

    // ===== Gameplay =====
    function handlePlayerControls(){
      // coyote & buffer decay
      if(player.onGround) player.coyote = COYOTE_FRAMES; else if(player.coyote>0) player.coyote--;
      if(player.jumpBuffer>0) player.jumpBuffer--;

      // first jump
      if(player.jumpBuffer>0 && (player.onGround || player.coyote>0)){
        player.vy = JUMP_VEL_1; player.onGround=false; player.jumps=1; player.usedDouble=false; player.jumpBuffer=0;
      }
      // double jump
      else if(player.jumpBuffer>0 && !player.onGround && !player.usedDouble){
        player.vy = JUMP_VEL_2; player.usedDouble=true; player.jumps=2; player.jumpBuffer=0;
      }
    }

    function update(){
      world.t++;

      if(world.alive){
        // difficulty ramp
        if(world.t % 180 === 0){
          world.speed = Math.min(world.speed + 0.6, world.maxSpeed);
          world.spawnInterval = Math.max(40, world.spawnInterval - 4);
        }

        handlePlayerControls();

        // physics
        player.vy += gravity;
        player.y  += player.vy;
        if(player.y >= floorY){
          player.y = floorY; player.vy = 0;
          if(!player.onGround){ player.onGround=true; player.usedDouble=false; player.jumps=0; }
        } else {
          player.onGround = false;
        }

        // spawn & move obstacles
        world.spawnTimer++;
        if(world.spawnTimer >= world.spawnInterval){
          world.spawnTimer = 0;
          spawnObstacle();
          if(Math.random()<0.25) setTimeout(spawnObstacle, 220 + Math.random()*280); // occasional close pair
        }
        for(let i=obstacles.length-1;i>=0;i--){
          const o = obstacles[i];
          o.x -= world.speed;
          if(o.x + o.w < -100) obstacles.splice(i,1);
        }

        // scoring
        world.score += 0.2 + world.speed*0.012;

        // collisions
        const pb = getPlayerBounds();
        for(const o of obstacles){
          for(let s=0; s<o.stacks; s++){
            const ob = { x:o.x, y:o.y - s*o.h, w:o.w, h:o.h };
            if(rectsOverlap(pb, ob)){ gameOver(); }
          }
        }
      }

      draw();
      requestAnimationFrame(update);
    }

    // ===== Bounds / Utils =====
    function getPlayerBounds(){
      // tight-ish box under the PNG; bottom-centered
      return { x: player.x - player.w*0.45, y: player.y - player.h, w: player.w*0.9, h: player.h*0.95 };
    }
    function rectsOverlap(a,b){
      return a.x < b.x + b.w && a.x + a.w > b.x && a.y < b.y + b.h && a.y + a.h > b.y;
    }

    // ===== Drawing =====
    function drawRoad(){
      ctx.fillStyle = '#2a2a2a';
      ctx.fillRect(0, floorY, W, H-floorY);
      // optional lane hints
      ctx.fillStyle = 'rgba(255,255,255,.25)';
      const stripeW = 120, stripeH = 6;
      const phase = (world.t*world.speed*0.5) % (stripeW*2);
      for(let x=-phase; x<W; x+=stripeW*2){
        ctx.fillRect(x, floorY+30, stripeW, stripeH);
        ctx.fillRect(x+60, floorY+60, stripeW, stripeH);
      }
    }
    function drawObstacles(){
      for(const o of obstacles){
        for(let s=0;s<o.stacks;s++){
          const x=o.x, y=o.y - s*o.h, w=o.w, h=o.h;
          if(o.type==='cone'){
            ctx.fillStyle = '#ff7a00';
            ctx.beginPath(); ctx.moveTo(x, y+h); ctx.lineTo(x+w/2, y); ctx.lineTo(x+w, y+h); ctx.closePath(); ctx.fill();
            ctx.fillStyle = '#fff'; ctx.fillRect(x+w*0.15, y+h*0.6, w*0.7, h*0.12);
          }else{
            ctx.fillStyle = '#8b5a2b'; ctx.fillRect(x, y, w, h);
            ctx.strokeStyle = 'rgba(0,0,0,.25)'; ctx.strokeRect(x+2, y+2, w-4, h-4);
          }
        }
      }
    }
    function drawVespa(){
      if(vespaReady){
        ctx.drawImage(vespaImg, player.x - player.w/2, player.y - player.h, player.w, player.h);
      }else{
        // minimal fallback block so game still runs before image loads
        ctx.fillStyle = '#1e8bff';
        ctx.fillRect(player.x - player.w/2, player.y - player.h, player.w, player.h);
      }
      // shadow
      ctx.fillStyle = 'rgba(0,0,0,.16)';
      ctx.beginPath(); ctx.ellipse(player.x, player.y-2, player.w*0.44, 8, 0, 0, Math.PI*2); ctx.fill();
    }
    function draw(){
      ctx.clearRect(0,0,W,H);
      drawRoad();
      drawObstacles();
      drawVespa();
    }

    // go
    update();
  </script>
</body>
</html>
