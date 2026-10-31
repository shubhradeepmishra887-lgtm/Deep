# Deep
Hi
<!DOCTYPE html>
<html lang="bn">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>মিনি স্পটিফাই - নো লগইন মিউজিক</title>
    <!-- ফন্ট অসম আইকনের জন্য -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background-color: #121212;
            color: #ffffff;
            display: flex;
            flex-direction: column;
            height: 100vh;
            overflow: hidden;
        }

        /* হেডার */
        header {
            background-color: #000000;
            padding: 15px 20px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            border-bottom: 1px solid #282828;
        }

        header h2 {
            color: #1db954;
            font-size: 22px;
        }

        header p {
            font-size: 12px;
            color: #b3b3b3;
        }

        /* মূল কন্টেন্ট এরিয়া */
        .main-container {
            flex: 1;
            padding: 20px;
            overflow-y: auto;
            padding-bottom: 100px;
        }

        h3 {
            margin-bottom: 15px;
            font-size: 18px;
            color: #fff;
        }

        /* মিউজিক লিস্ট */
        .song-list {
            display: flex;
            flex-direction: column;
            gap: 10px;
        }

        .song-card {
            display: flex;
            align-items: center;
            justify-content: space-between;
            background-color: #181818;
            padding: 12px 15px;
            border-radius: 8px;
            cursor: pointer;
            transition: 0.3s;
        }

        .song-card:hover {
            background-color: #282828;
        }

        .song-info {
            display: flex;
            align-items: center;
            gap: 15px;
        }

        .song-info img {
            width: 45px;
            height: 45px;
            border-radius: 5px;
            object-fit: cover;
        }

        .song-title {
            font-size: 15px;
            font-weight: 500;
        }

        .song-artist {
            font-size: 12px;
            color: #b3b3b3;
        }

        .play-btn-icon {
            color: #1db954;
            font-size: 20px;
        }

        /* নিচের মিউজিক প্লেয়ার বার (Fixed Bottom Player) */
        .player-bar {
            position: fixed;
            bottom: 0;
            left: 0;
            width: 100%;
            background-color: #181818;
            border-top: 1px solid #282828;
            padding: 12px 20px;
            display: flex;
            flex-direction: column;
            gap: 8px;
        }

        .player-content {
            display: flex;
            align-items: center;
            justify-content: space-between;
        }

        .current-playing {
            display: flex;
            align-items: center;
            gap: 12px;
            width: 30%;
        }

        .current-playing img {
            width: 40px;
            height: 40px;
            border-radius: 4px;
        }

        .current-title {
            font-size: 14px;
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
        }

        .current-artist {
            font-size: 11px;
            color: #b3b3b3;
        }

        /* প্লেয়ার কন্ট্রোল বাটন */
        .player-controls {
            display: flex;
            align-items: center;
            gap: 20px;
            font-size: 20px;
        }

        .player-controls i {
            cursor: pointer;
            color: #b3b3b3;
            transition: 0.2s;
        }

        .player-controls i:hover {
            color: #fff;
        }

        .player-controls .fa-play, .player-controls .fa-pause {
            background-color: #fff;
            color: #000;
            padding: 10px;
            border-radius: 50%;
            font-size: 16px;
        }

        .player-controls .fa-play:hover, .player-controls .fa-pause:hover {
            transform: scale(1.05);
            color: #000;
        }

        /* প্রোগ্রেস বার */
        .progress-container {
            display: flex;
            align-items: center;
            gap: 10px;
            width: 100%;
        }

        .progress-bar {
            flex: 1;
            height: 4px;
            background-color: #535353;
            border-radius: 2px;
            cursor: pointer;
            appearance: none;
        }

        .time-display {
            font-size: 11px;
            color: #b3b3b3;
        }

        /* মোবাইল ফ্রেন্ডলি রেসপন্সিভ ডিজাইন */
        @media (max-width: 600px) {
            .current-playing {
                width: 50%;
            }
        }
    </style>
</head>
<body>

    <!-- হেডার অংশ -->
    <header>
        <div>
            <h2><i class="fa-brands fa-spotify"></i> Mini Spotify</h2>
            <p>লগইন ছাড়াই গান শুনুন</p>
        </div>
    </header>

    <!-- গানের তালিকা -->
    <div class="main-container">
        <h3>জনপ্রিয় গানসমূহ</h3>
        <div class="song-list" id="songList">
            <!-- জাভাস্ক্রিপ্ট দিয়ে গানগুলো এখানে লোড হবে -->
        </div>
    </div>

    <!-- ফিক্সড মিউজিক প্লেয়ার -->
    <div class="player-bar">
        <div class="player-content">
            <div class="current-playing">
                <img id="currCover" src="https://images.unsplash.com/photo-1470225620780-dba8ba36b745?w=100" alt="Cover">
                <div>
                    <div class="current-title" id="currTitle">গান সিলেক্ট করুন</div>
                    <div class="current-artist" id="currArtist">আর্টিস্ট</div>
                </div>
            </div>

            <div class="player-controls">
                <i class="fa-solid fa-backward-step" id="prevBtn"></i>
                <i class="fa-solid fa-play" id="playPauseBtn"></i>
                <i class="fa-solid fa-forward-step" id="nextBtn"></i>
            </div>
            
            <div style="width: 20%; text-align: right;">
                <i class="fa-solid fa-volume-high" style="color: #b3b3b3;"></i>
            </div>
        </div>

        <div class="progress-container">
            <span class="time-display" id="currentTime">0:00</span>
            <input type="range" class="progress-bar" id="progressBar" value="0" max="100">
            <span class="time-display" id="totalDuration">0:00</span>
        </div>
    </div>

    <!-- অডিও ট্যাগ (লুকানো) -->
    <audio id="audioPlayer"></audio>

    <!-- জাভাস্ক্রিপ্ট লজিক -->
    <script>
        // গানের ডাটাবেস (এখানে ফ্রি অডিও লিংক দেওয়া হয়েছে)
        const songs = [
            {
                title: "Ukulele Acoustic",
                artist: "Bensound",
                cover: "https://images.unsplash.com/photo-1511671782779-c97d3d27a1d4?w=100",
                src: "https://www.bensound.com/bensound-music/bensound-ukulele.mp3"
            },
            {
                title: "Creative Minds",
                artist: "Bensound",
                cover: "https://images.unsplash.com/photo-1465847899084-d164df4dedc6?w=100",
                src: "https://www.bensound.com/bensound-music/bensound-creativeminds.mp3"
            },
            {
                title: "Acoustic Breeze",
                artist: "Bensound",
                cover: "https://images.unsplash.com/photo-1514525253161-7a46d19cd819?w=100",
                src: "https://www.bensound.com/bensound-music/bensound-acousticbreeze.mp3"
            },
            {
                title: "Sunny",
                artist: "Bensound",
                cover: "https://images.unsplash.com/photo-1501386761578-eac5c94b800a?w=100",
                src: "https://www.bensound.com/bensound-music/bensound-sunny.mp3"
            }
        ];

        let currentSongIndex = 0;
        const audioPlayer = document.getElementById('audioPlayer');
        const playPauseBtn = document.getElementById('playPauseBtn');
        const songListContainer = document.getElementById('songList');
        const currTitle = document.getElementById('currTitle');
        const currArtist = document.getElementById('currArtist');
        const currCover = document.getElementById('currCover');
        const progressBar = document.getElementById('progressBar');
        const currentTimeEl = document.getElementById('currentTime');
        const totalDurationEl = document.getElementById('totalDuration');

        // গানগুলোর লিস্ট স্ক্রিনে রেন্ডার করা
        function loadSongList() {
            songListContainer.innerHTML = '';
            songs.forEach((song, index) => {
                const songCard = document.createElement('div');
                songCard.classList.add('song-card');
                songCard.innerHTML = `
                    <div class="song-info">
                        <img src="${song.cover}" alt="Cover">
                        <div>
                            <div class="song-title">${song.title}</div>
                            <div class="song-artist">${song.artist}</div>
                        </div>
                    </div>
                    <div class="play-btn-icon">
                        <i class="fa-solid fa-circle-play"></i>
                    </div>
                `;
                songCard.addEventListener('click', () => {
                    currentSongIndex = index;
                    playSong();
                });
                songListContainer.appendChild(songCard);
            });
        }

        // গান প্লে করার ফাংশন
        function playSong() {
            const song = songs[currentSongIndex];
            audioPlayer.src = song.src;
            currTitle.innerText = song.title;
            currArtist.innerText = song.artist;
            currCover.src = song.cover;
            
            audioPlayer.play();
            playPauseBtn.classList.remove('fa-play');
            playPauseBtn.classList.add('fa-pause');
        }

        // প্লে/পজ টগল করা
        playPauseBtn.addEventListener('click', () => {
            if (audioPlayer.paused) {
                if(audioPlayer.src === "") {
                    playSong();
                } else {
                    audioPlayer.play();
                    playPauseBtn.classList.remove('fa-play');
                    playPauseBtn.classList.add('fa-pause');
                }
            } else {
                audioPlayer.pause();
                playPauseBtn.classList.remove('fa-pause');
                playPauseBtn.classList.add('fa-play');
            }
        });

        // পরবর্তী গান
        document.getElementById('nextBtn').addEventListener('click', () => {
            currentSongIndex = (currentSongIndex + 1) % songs.length;
            playSong();
        });

        // পূর্ববর্তী গান
        document.getElementById('prevBtn').addEventListener('click', () => {
            currentSongIndex = (currentSongIndex - 1 + songs.length) % songs.length;
            playSong();
        });

        // প্রোগ্রেস বার আপডেট
        audioPlayer.addEventListener('timeupdate', () => {
            if (audioPlayer.duration) {
                const progressPercent = (audioPlayer.currentTime / audioPlayer.duration) * 100;
                progressBar.value = progressPercent;

                // বর্তমান সময় ফরম্যাট
                let currentMinutes = Math.floor(audioPlayer.currentTime / 60);
                let currentSeconds = Math.floor(audioPlayer.currentTime % 60);
                if (currentSeconds < 10) currentSeconds = "0" + currentSeconds;
                currentTimeEl.innerText = `${currentMinutes}:${currentSeconds}`;

                // মোট সময় ফরম্যাট
                let totalMinutes = Math.floor(audioPlayer.duration / 60);
                let totalSeconds = Math.floor(audioPlayer.duration % 60);
                if (totalSeconds < 10) totalSeconds = "0" + totalSeconds;
                totalDurationEl.innerText = `${totalMinutes}:${totalSeconds}`;
            }
        });

        // প্রোগ্রেস বার টেনে গান ফরোয়ার্ড/ব্যাকওয়ার্ড করা
        progressBar.addEventListener('input', () => {
            const seekTime = (progressBar.value / 100) * audioPlayer.duration;
            audioPlayer.currentTime = seekTime;
        });

        // গান শেষ হলে অটোমেটিক পরের গান বাজবে
        audioPlayer.addEventListener('ended', () => {
            currentSongIndex = (currentSongIndex + 1) % songs.length;
            playSong();
        });

        // প্রথম লোড
        loadSongList();
    </script>
</body>
</html>
<script>
    const songs = [
        {
            title: "Ukulele Acoustic",
            artist: "Bensound",
            cover: "https://images.unsplash.com/photo-1511671782779-c97d3d27a1d4?w=100",
            src: "https://www.bensound.com/bensound-music/bensound-ukulele.mp3"
        },
        {
            title: "Creative Minds",
            artist: "Bensound",
            cover: "https://images.unsplash.com/photo-1465847899084-d164df4dedc6?w=100",
            src: "https://www.bensound.com/bensound-music/bensound-creativeminds.mp3"
        },
        {
            title: "Acoustic Breeze",
            artist: "Bensound",
            cover: "https://images.unsplash.com/photo-1514525253161-7a46d19cd819?w=100",
            src: "https://www.bensound.com/bensound-music/bensound-acousticbreeze.mp3"
        },
        {
            title: "Sunny",
            artist: "Bensound",
            cover: "https://images.unsplash.com/photo-1501386761578-eac5c94b800a?w=100",
            src: "https://www.bensound.com/bensound-music/bensound-sunny.mp3"
        }
    ];

    let currentSongIndex = 0;
    const audioPlayer = document.getElementById('audioPlayer');
    const playPauseBtn = document.getElementById('playPauseBtn');
    const songListContainer = document.getElementById('songList');
    const currTitle = document.getElementById('currTitle');
    const currArtist = document.getElementById('currArtist');
    const currCover = document.getElementById('currCover');
    const progressBar = document.getElementById('progressBar');
    const currentTimeEl = document.getElementById('currentTime');
    const totalDurationEl = document.getElementById('totalDuration');

    audioPlayer.preload = "metadata";
    audioPlayer.volume = 0.8;

    function formatTime(seconds) {
        if (!Number.isFinite(seconds) || seconds < 0) return "0:00";
        const minutes = Math.floor(seconds / 60);
        const secs = Math.floor(seconds % 60);
        return `${minutes}:${String(secs).padStart(2, "0")}`;
    }

    function updatePlayPauseUI(isPlaying) {
        playPauseBtn.classList.toggle('fa-play', !isPlaying);
        playPauseBtn.classList.toggle('fa-pause', isPlaying);
    }

    function highlightCurrentSong() {
        const cards = document.querySelectorAll('.song-card');
        cards.forEach((card, index) => {
            card.classList.toggle('active', index === currentSongIndex);
            card.style.border = index === currentSongIndex ? '1px solid #1db954' : '1px solid transparent';
        });
    }

    function loadSongList() {
        songListContainer.innerHTML = '';
        songs.forEach((song, index) => {
            const songCard = document.createElement('div');
            songCard.classList.add('song-card');
            if (index === currentSongIndex) songCard.style.border = '1px solid #1db954';
            songCard.innerHTML = `
                <div class="song-info">
                    <img src="${song.cover}" alt="Cover">
                    <div>
                        <div class="song-title">${song.title}</div>
                        <div class="song-artist">${song.artist}</div>
                    </div>
                </div>
                <div class="play-btn-icon">
                    <i class="fa-solid fa-circle-play"></i>
                </div>
            `;
            songCard.addEventListener('click', () => {
                currentSongIndex = index;
                playSong();
            });
            songListContainer.appendChild(songCard);
        });
        highlightCurrentSong();
    }

    function playSong() {
        const song = songs[currentSongIndex];
        audioPlayer.src = song.src;
        audioPlayer.load();

        currTitle.innerText = song.title;
        currArtist.innerText = song.artist;
        currCover.src = song.cover;

        audioPlayer.play().catch(() => {
            updatePlayPauseUI(false);
            console.log("Autoplay blocked by browser. User must click play.");
        });

        updatePlayPauseUI(true);
        loadSongList();
    }

    playPauseBtn.addEventListener('click', () => {
        if (audioPlayer.paused) {
            if (!audioPlayer.src) {
                playSong();
            } else {
                audioPlayer.play().catch(() => {
                    console.log("Playback blocked until user interaction.");
                });
                updatePlayPauseUI(true);
            }
        } else {
            audioPlayer.pause();
            updatePlayPauseUI(false);
        }
    });

    document.getElementById('nextBtn').addEventListener('click', () => {
        currentSongIndex = (currentSongIndex + 1) % songs.length;
        playSong();
    });

    document.getElementById('prevBtn').addEventListener('click', () => {
        currentSongIndex = (currentSongIndex - 1 + songs.length) % songs.length;
        playSong();
    });

    progressBar.addEventListener('input', () => {
        if (!Number.isFinite(audioPlayer.duration) || audioPlayer.duration <= 0) return;
        const seekTime = (progressBar.value / 100) * audioPlayer.duration;
        audioPlayer.currentTime = seekTime;
    });

    audioPlayer.addEventListener('timeupdate', () => {
        if (!Number.isFinite(audioPlayer.duration) || audioPlayer.duration <= 0) return;

        const progressPercent = (audioPlayer.currentTime / audioPlayer.duration) * 100;
        progressBar.value = progressPercent;

        currentTimeEl.innerText = formatTime(audioPlayer.currentTime);
        totalDurationEl.innerText = formatTime(audioPlayer.duration);
    });

    audioPlayer.addEventListener('loadedmetadata', () => {
        totalDurationEl.innerText = formatTime(audioPlayer.duration);
    });

    audioPlayer.addEventListener('ended', () => {
        currentSongIndex = (currentSongIndex + 1) % songs.length;
        playSong();
    });

    audioPlayer.addEventListener('play', () => updatePlayPauseUI(true));
    audioPlayer.addEventListener('pause', () => updatePlayPauseUI(false));

    loadSongList()
    updatePlayPauseUI(false);
</script>
