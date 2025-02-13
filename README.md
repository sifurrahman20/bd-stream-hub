!DOCTYPE html>
<html lang="bn">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>BD STREAM HUB </title>
  <script src="https://cdn.jsdelivr.net/npm/hls.js@latest"></script>
  <style>
    body {
      margin: 0;
      padding: 0;
      background: #111;
      color: #fff;
      font-family: Arial, sans-serif;
      overflow-y: auto;
    }
    header {
      background: #222;
      padding: 20px;
      text-align: center;
    }
    .video-container {
      text-align: center;
      padding: 20px;
    }
    video {
      width: 100%;
      max-width: 800px;
      border: 5px solid #444;
    }
    .category {
      margin: 20px;
      padding: 10px;
      background: #222;
      border-radius: 5px;
    }
    .category h2 {
      text-align: center;
      color: #ffcc00;
    }
    .channels {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      gap: 10px;
    }
    .channel-btn {
      background: #333;
      color: #fff;
      border: none;
      padding: 10px 20px;
      font-size: 1em;
      cursor: pointer;
      border-radius: 5px;
      transition: background 0.3s;
    }
    .channel-btn:hover {
      background: #555;
    }
    .channel-btn.active {
      background: #007BFF;
    }
    .announcement {
      text-align: center;
      margin: 20px;
    }
    .announcement input {
      width: 80%;
      padding: 10px;
      font-size: 1em;
      border-radius: 5px;
      border: 1px solid #fff;
      background: #333;
      color: #fff;
    }
    .title-button {
      display: block;
      margin: 20px auto;
      padding: 10px 20px;
      font-size: 1.2em;
      background: #ffcc00;
      color: #111;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }
  </style>
</head>
<body>
  <header>
    <h1>BD STREAM HUB</h1>
    <button class="title-button" onclick="setTitle()">কেউ প্লেলিস্টের লিংক চাহিয়া লজ্জা দিবেন না</button>
  </header>
  
  <div class="video-container">
    <video id="livePlayer" controls poster="https://via.placeholder.com/800x450">
      Your browser does not support the video tag.
    </video>
  </div>
  
  <div class="announcement">
    <input type="text" id="announcementText" placeholder="এখানে আপনার বার্তা লিখুন...">
  </div>
  
  <!-- Sports Channels -->
  <div class="category">
    <h2>Sports Channels</h2>
    <div class="channels">
      <button class="channel-btn" onclick="loadStream('https://live.tsports.com/mobile_hls/tsports_live_2/playlist.m3u8', this)">T Sports</button>
      <button class="channel-btn" onclick="loadStream('http://125.209.88.166:45793/BRN/TenSports.stream/playlist.m3u8', this)">Ten Sports HD</button>
      <button class="channel-btn" onclick="loadStream('https://criccoder.pages.dev/astro.m3u8', this)">Astro Cricket HD</button>
      <button class="channel-btn" onclick="loadStream('http://125.209.88.166:45793/BRN/ArySports.stream/playlist.m3u8', this)">A Sports</button>
    </div>
  </div>
  
  <!-- News Channels -->
  <div class="category">
    <h2>News Channels</h2>
    <div class="channels">
      <button class="channel-btn" onclick="loadStream('http://lkn1.chowdhury-shaheb.com/jamuna/index.m3u8', this)">Jamuna TV</button>
      <button class="channel-btn" onclick="loadStream('http://lkn1.chowdhury-shaheb.com/dbc/index.m3u8', this)">DBC News</button>
      <button class="channel-btn" onclick="loadStream('http://lkn1.chowdhury-shaheb.com/somoy/index.m3u8', this)">Somoy TV</button>
      <button class="channel-btn" onclick="loadStream('http://lkn1.chowdhury-shaheb.com/ekattor/index.m3u8', this)">Ekattor TV</button>
    </div>
  </div>
  
  <!-- Entertainment Channels -->
  <div class="category">
    <h2>Entertainment Channels</h2>
    <div class="channels">
      <button class="channel-btn" onclick="loadStream('https://d35j504z0x2vu2.cloudfront.net/v1/master/0bc8e8376bd8417a1b6761138aa41c26c7309312/mastiii/master.m3u8', this)">AB Masti iii</button>
      <button class="channel-btn" onclick="loadStream('http://lkn1.chowdhury-shaheb.com/starjalsha/index.m3u8', this)">Star Jalsha</button>
      <button class="channel-btn" onclick="loadStream('http://lkn1.chowdhury-shaheb.com/zeebangla/index.m3u8', this)">Zee Bangla</button>
      <button class="channel-btn" onclick="loadStream('http://lkn1.chowdhury-shaheb.com/sonyatt/index.m3u8', this)">Sony Aath</button>
    </div>
  </div>
  
  <script>
    function loadStream(url, btn) {
      var video = document.getElementById('livePlayer');
      var buttons = document.getElementsByClassName('channel-btn');
      for (var i = 0; i < buttons.length; i++) {
        buttons[i].classList.remove('active');
      }
      btn.classList.add('active');
      if (Hls.isSupported()) {
        if (window.hls) {
          window.hls.destroy();
        }
        window.hls = new Hls();
        window.hls.loadSource(url);
        window.hls.attachMedia(video);
        window.hls.on(Hls.Events.MANIFEST_PARSED, function() {
          video.play();
        });
      } else if (video.canPlayType('application/vnd.apple.mpegurl')) {
        video.src = url;
        video.addEventListener('loadedmetadata', function() {
          video.play();
        });
      }
    }
  </script>
</body>
</html>
