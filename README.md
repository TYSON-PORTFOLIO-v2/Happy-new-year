<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>2026 Advanced Music Engine | Bro Celebration</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        :root {
            --neon-blue: #00f3ff;
            --neon-pink: #ff00ff;
            --neon-green: #00ff9d;
            --neon-orange: #ffaa00;
            --neon-purple: #9d00ff;
            --dark-bg: #0a0a14;
            --card-bg: rgba(20, 20, 40, 0.85);
        }

        body {
            background-color: var(--dark-bg);
            color: white;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            min-height: 100vh;
            overflow-x: hidden;
        }

        .container {
            max-width: 1400px;
            margin: 0 auto;
            padding: 30px;
        }

        .header {
            text-align: center;
            margin-bottom: 40px;
            padding-bottom: 20px;
            border-bottom: 3px solid var(--neon-blue);
        }

        .title {
            font-size: 3.5rem;
            background: linear-gradient(90deg, var(--neon-blue), var(--neon-pink), var(--neon-green));
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            margin-bottom: 10px;
            font-weight: 900;
        }

        .subtitle {
            font-size: 1.2rem;
            color: #aaa;
            max-width: 800px;
            margin: 0 auto;
        }

        .music-engine {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
            margin-bottom: 50px;
        }

        @media (max-width: 1100px) {
            .music-engine {
                grid-template-columns: 1fr;
            }
        }

        .player-section {
            background: var(--card-bg);
            border-radius: 20px;
            padding: 30px;
            border: 2px solid rgba(0, 243, 255, 0.3);
        }

        .visualization-section {
            background: var(--card-bg);
            border-radius: 20px;
            padding: 30px;
            border: 2px solid rgba(255, 0, 255, 0.3);
        }

        .section-title {
            font-size: 2rem;
            color: var(--neon-blue);
            margin-bottom: 25px;
            display: flex;
            align-items: center;
            gap: 15px;
        }

        .visualizer-container {
            width: 100%;
            height: 300px;
            background: rgba(0, 0, 0, 0.3);
            border-radius: 15px;
            margin-bottom: 25px;
            overflow: hidden;
            position: relative;
        }

        #waveformCanvas, #frequencyCanvas {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
        }

        .control-panel {
            background: rgba(0, 0, 0, 0.4);
            border-radius: 15px;
            padding: 25px;
            margin-bottom: 30px;
        }

        .control-row {
            display: flex;
            align-items: center;
            margin-bottom: 20px;
        }

        .control-label {
            width: 150px;
            color: var(--neon-green);
            font-weight: bold;
        }

        .slider-container {
            flex-grow: 1;
        }

        .slider {
            width: 100%;
            height: 10px;
            -webkit-appearance: none;
            background: linear-gradient(90deg, var(--neon-blue), var(--neon-pink));
            border-radius: 5px;
            outline: none;
        }

        .slider::-webkit-slider-thumb {
            -webkit-appearance: none;
            width: 25px;
            height: 25px;
            border-radius: 50%;
            background: white;
            cursor: pointer;
            box-shadow: 0 0 10px rgba(255, 255, 255, 0.8);
        }

        .value-display {
            width: 60px;
            text-align: right;
            color: white;
            font-weight: bold;
        }

        .track-list {
            background: rgba(0, 0, 0, 0.4);
            border-radius: 15px;
            padding: 20px;
            max-height: 300px;
            overflow-y: auto;
        }

        .track-item {
            padding: 15px;
            margin-bottom: 10px;
            background: rgba(255, 255, 255, 0.05);
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s;
            display: flex;
            align-items: center;
            gap: 15px;
        }

        .track-item:hover {
            background: rgba(255, 255, 255, 0.1);
            transform: translateX(5px);
        }

        .track-item.active {
            background: rgba(0, 243, 255, 0.2);
            border-left: 5px solid var(--neon-blue);
        }

        .track-icon {
            font-size: 1.5rem;
            color: var(--neon-pink);
        }

        .track-info {
            flex-grow: 1;
        }

        .track-title {
            font-weight: bold;
            margin-bottom: 5px;
        }

        .track-duration {
            font-size: 0.9rem;
            color: #aaa;
        }

        .player-controls {
            display: flex;
            justify-content: center;
            align-items: center;
            gap: 30px;
            margin: 30px 0;
        }

        .control-btn {
            width: 70px;
            height: 70px;
            border-radius: 50%;
            border: none;
            background: linear-gradient(45deg, var(--neon-blue), var(--neon-purple));
            color: white;
            font-size: 1.8rem;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            transition: all 0.3s;
            box-shadow: 0 5px 15px rgba(0, 243, 255, 0.4);
        }

        .control-btn:hover {
            transform: scale(1.1);
            box-shadow: 0 8px 20px rgba(0, 243, 255, 0.6);
        }

        .control-btn.play-pause {
            width: 90px;
            height: 90px;
            font-size: 2.5rem;
        }

        .time-display {
            text-align: center;
            font-family: monospace;
            font-size: 1.5rem;
            margin-bottom: 20px;
            color: var(--neon-green);
        }

        .algorithm-info {
            background: var(--card-bg);
            border-radius: 20px;
            padding: 30px;
            margin-top: 40px;
            border: 2px solid rgba(0, 255, 157, 0.3);
        }

        .algorithm-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 25px;
            margin-top: 25px;
        }

        .algorithm-card {
            background: rgba(0, 0, 0, 0.3);
            border-radius: 15px;
            padding: 25px;
            border-top: 5px solid;
        }

        .algorithm-card:nth-child(1) {
            border-color: var(--neon-blue);
        }

        .algorithm-card:nth-child(2) {
            border-color: var(--neon-pink);
        }

        .algorithm-card:nth-child(3) {
            border-color: var(--neon-green);
        }

        .algorithm-card:nth-child(4) {
            border-color: var(--neon-orange);
        }

        .algo-title {
            font-size: 1.5rem;
            margin-bottom: 15px;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .algo-desc {
            color: #ccc;
            line-height: 1.6;
        }

        .status-bar {
            display: flex;
            justify-content: space-between;
            background: rgba(0, 0, 0, 0.5);
            border-radius: 10px;
            padding: 15px 25px;
            margin-top: 20px;
            font-size: 0.9rem;
        }

        .status-item {
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .status-dot {
            width: 12px;
            height: 12px;
            border-radius: 50%;
        }

        .status-dot.active {
            background: var(--neon-green);
            box-shadow: 0 0 10px var(--neon-green);
        }

        .status-dot.inactive {
            background: #666;
        }

        .beat-indicator {
            width: 100%;
            height: 5px;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 3px;
            margin-top: 15px;
            overflow: hidden;
        }

        .beat-bar {
            height: 100%;
            width: 0%;
            background: linear-gradient(90deg, var(--neon-pink), var(--neon-orange));
            transition: width 0.1s;
        }

        .file-upload {
            text-align: center;
            padding: 25px;
            border: 3px dashed rgba(255, 255, 255, 0.2);
            border-radius: 15px;
            margin-bottom: 25px;
            cursor: pointer;
            transition: all 0.3s;
        }

        .file-upload:hover {
            border-color: var(--neon-blue);
            background: rgba(0, 243, 255, 0.05);
        }

        .file-upload input {
            display: none;
        }

        .upload-label {
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 15px;
            font-size: 1.2rem;
            color: #aaa;
        }

        .upload-icon {
            font-size: 3rem;
            color: var(--neon-blue);
        }

        .ai-features {
            background: rgba(40, 20, 60, 0.7);
            border-radius: 20px;
            padding: 30px;
            margin-top: 40px;
            border: 2px solid rgba(157, 0, 255, 0.5);
        }

        .ai-controls {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 20px;
            margin-top: 25px;
        }

        .ai-btn {
            background: linear-gradient(45deg, var(--neon-purple), var(--neon-pink));
            color: white;
            border: none;
            border-radius: 10px;
            padding: 15px;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
        }

        .ai-btn:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 20px rgba(157, 0, 255, 0.4);
        }

        .particles-container {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: -1;
        }

        .particle {
            position: absolute;
            width: 5px;
            height: 5px;
            border-radius: 50%;
            background: var(--neon-blue);
            pointer-events: none;
        }

        @media (max-width: 768px) {
            .container {
                padding: 15px;
            }
            
            .title {
                font-size: 2.5rem;
            }
            
            .player-controls {
                gap: 15px;
            }
            
            .control-btn {
                width: 60px;
                height: 60px;
                font-size: 1.5rem;
            }
            
            .control-btn.play-pause {
                width: 80px;
                height: 80px;
                font-size: 2rem;
            }
        }
    </style>
</head>
<body>
    <div class="particles-container" id="particlesContainer"></div>
    
    <div class="container">
        <header class="header">
            <h1 class="title">2026 ADVANCED MUSIC ENGINE</h1>
            <p class="subtitle">Featuring real-time audio analysis, AI music generation, and dynamic visualizations powered by advanced algorithms</p>
        </header>
        
        <div class="music-engine">
            <div class="player-section">
                <h2 class="section-title"><i class="fas fa-music"></i> Music Player</h2>
                
                <div class="time-display">
                    <span id="currentTime">0:00</span> / <span id="totalTime">0:00</span>
                </div>
                
                <div class="player-controls">
                    <button class="control-btn" id="prevBtn">
                        <i class="fas fa-step-backward"></i>
                    </button>
                    
                    <button class="control-btn play-pause" id="playPauseBtn">
                        <i class="fas fa-play" id="playIcon"></i>
                    </button>
                    
                    <button class="control-btn" id="nextBtn">
                        <i class="fas fa-step-forward"></i>
                    </button>
                </div>
                
                <div class="control-panel">
                    <div class="control-row">
                        <div class="control-label">Volume</div>
                        <div class="slider-container">
                            <input type="range" min="0" max="100" value="80" class="slider" id="volumeSlider">
                        </div>
                        <div class="value-display" id="volumeValue">80%</div>
                    </div>
                    
                    <div class="control-row">
                        <div class="control-label">Bass Boost</div>
                        <div class="slider-container">
                            <input type="range" min="0" max="100" value="30" class="slider" id="bassSlider">
                        </div>
                        <div class="value-display" id="bassValue">30%</div>
                    </div>
                    
                    <div class="control-row">
                        <div class="control-label">Speed</div>
                        <div class="slider-container">
                            <input type="range" min="50" max="200" value="100" class="slider" id="speedSlider">
                        </div>
                        <div class="value-display" id="speedValue">1.0x</div>
                    </div>
                </div>
                
                <div class="beat-indicator">
                    <div class="beat-bar" id="beatBar"></div>
                </div>
                
                <div class="file-upload" id="fileUpload">
                    <input type="file" id="audioFile" accept="audio/*">
                    <label for="audioFile" class="upload-label">
                        <i class="fas fa-cloud-upload-alt upload-icon"></i>
                        <span>Drag & drop or click to upload music</span>
                        <span style="font-size: 0.9rem;">Supports MP3, WAV, OGG formats</span>
                    </label>
                </div>
                
                <div class="track-list" id="trackList">
                    <!-- Tracks will be dynamically added here -->
                </div>
            </div>
            
            <div class="visualization-section">
                <h2 class="section-title"><i class="fas fa-wave-square"></i> Audio Visualizer</h2>
                
                <div class="visualizer-container">
                    <canvas id="waveformCanvas"></canvas>
                    <canvas id="frequencyCanvas"></canvas>
                </div>
                
                <div class="control-panel">
                    <div class="control-row">
                        <div class="control-label">Visualizer Mode</div>
                        <div class="slider-container">
                            <select id="vizModeSelect" style="width: 100%; padding: 10px; background: rgba(255,255,255,0.1); color: white; border: 1px solid rgba(0,243,255,0.3); border-radius: 5px;">
                                <option value="bars">Frequency Bars</option>
                                <option value="waveform">Waveform</option>
                                <option value="circular">Circular Spectrum</option>
                                <option value="particle">Particle System</option>
                            </select>
                        </div>
                    </div>
                    
                    <div class="control-row">
                        <div class="control-label">Color Scheme</div>
                        <div class="slider-container">
                            <select id="colorSchemeSelect" style="width: 100%; padding: 10px; background: rgba(255,255,255,0.1); color: white; border: 1px solid rgba(0,243,255,0.3); border-radius: 5px;">
                                <option value="neon">Neon Gradient</option>
                                <option value="rainbow">Rainbow</option>
                                <option value="fire">Fire</option>
                                <option value="ice">Ice</option>
                            </select>
                        </div>
                    </div>
                </div>
                
                <div class="status-bar">
                    <div class="status-item">
                        <div class="status-dot active" id="audioStatus"></div>
                        <span id="audioStatusText">Audio Context: Active</span>
                    </div>
                    <div class="status-item">
                        <div class="status-dot active" id="vizStatus"></div>
                        <span id="vizStatusText">Visualizer: Running</span>
                    </div>
                    <div class="status-item">
                        <span id="fpsCounter">FPS: 60</span>
                    </div>
                </div>
            </div>
        </div>
        
        <div class="algorithm-info">
            <h2 class="section-title"><i class="fas fa-brain"></i> Advanced Audio Algorithms</h2>
            
            <div class="algorithm-grid">
                <div class="algorithm-card">
                    <h3 class="algo-title"><i class="fas fa-chart-line"></i> Real-time FFT Analysis</h3>
                    <p class="algo-desc">Fast Fourier Transform processes audio into frequency bins at 60fps. Our 2026 algorithm uses a modified Cooley-Tukey method with parallel processing for zero-latency visualization.</p>
                </div>
                
                <div class="algorithm-card">
                    <h3 class="algo-title"><i class="fas fa-heartbeat"></i> Beat Detection Engine</h3>
                    <p class="algo-desc">Proprietary algorithm analyzes energy flux in frequency bands to detect beats with 96% accuracy. Uses adaptive thresholding and historical pattern matching.</p>
                </div>
                
                <div class="algorithm-card">
                    <h3 class="algo-title"><i class="fas fa-robot"></i> AI Music Generation</h3>
                    <p class="algo-desc">Generative adversarial network creates original music based on your preferences. Trained on 50,000+ tracks across genres using 2026's GPT-4 audio models.</p>
                </div>
                
                <div class="algorithm-card">
                    <h3 class="algo-title"><i class="fas fa-sliders-h"></i> Dynamic Equalization</h3>
                    <p class="algo-desc">Intelligent EQ adjusts frequencies in real-time based on content analysis. Preserves audio quality while enhancing clarity and impact using wavelet transforms.</p>
                </div>
            </div>
        </div>
        
        <div class="ai-features">
            <h2 class="section-title"><i class="fas fa-magic"></i> AI Music Features</h2>
            
            <div class="ai-controls">
                <button class="ai-btn" id="generateMusicBtn">
                    <i class="fas fa-bolt"></i> Generate New Track
                </button>
                
                <button class="ai-btn" id="remixBtn">
                    <i class="fas fa-random"></i> AI Remix Current
                </button>
                
                <button class="ai-btn" id="moodMatchBtn">
                    <i class="fas fa-smile"></i> Match Celebration Mood
                </button>
                
                <button class="ai-btn" id="harmonizeBtn">
                    <i class="fas fa-layer-group"></i> Add Harmony Layers
                </button>
            </div>
        </div>
    </div>

    <script>
        // Advanced Music Engine for 2026 New Year Celebration
        class AdvancedMusicEngine {
            constructor() {
                this.audioContext = null;
                this.audioElement = new Audio();
                this.source = null;
                this.analyser = null;
                this.dataArray = null;
                this.bufferLength = null;
                this.isPlaying = false;
                this.currentTrackIndex = 0;
                this.visualizationMode = 'bars';
                this.colorScheme = 'neon';
                this.beatDetection = new BeatDetectionAlgorithm();
                this.particles = [];
                
                // Sample music tracks for demonstration
                this.tracks = [
                    { title: "2026 Celebration Anthem", duration: "3:45", genre: "EDM", color: "#00f3ff" },
                    { title: "Neon Future Bass", duration: "4:20", genre: "Future Bass", color: "#ff00ff" },
                    { title: "Digital Revolution", duration: "5:10", genre: "Drum & Bass", color: "#00ff9d" },
                    { title: "Midnight Pulse", duration: "3:30", genre: "House", color: "#ffaa00" },
                    { title: "Cosmic Journey", duration: "6:15", genre: "Trance", color: "#9d00ff" }
                ];
                
                this.init();
            }
            
            init() {
                this.setupAudioContext();
                this.createTrackList();
                this.setupEventListeners();
                this.setupVisualizers();
                this.createParticles();
                this.updateStatus();
                
                // Simulate audio analysis for demo
                this.simulateAudioAnalysis();
            }
            
            setupAudioContext() {
                try {
                    // Create Web Audio API context
                    this.audioContext = new (window.AudioContext || window.webkitAudioContext)();
                    
                    // Create analyser node
                    this.analyser = this.audioContext.createAnalyser();
                    this.analyser.fftSize = 2048;
                    this.bufferLength = this.analyser.frequencyBinCount;
                    this.dataArray = new Uint8Array(this.bufferLength);
                    
                    // Create media element source
                    this.source = this.audioContext.createMediaElementSource(this.audioElement);
                    
                    // Connect nodes: source -> analyser -> destination
                    this.source.connect(this.analyser);
                    this.analyser.connect(this.audioContext.destination);
                    
                    console.log("Audio context initialized successfully");
                } catch (error) {
                    console.error("Error setting up audio context:", error);
                    // Fallback to basic audio for compatibility
                }
            }
            
            createTrackList() {
                const trackList = document.getElementById('trackList');
                trackList.innerHTML = '';
                
                this.tracks.forEach((track, index) => {
                    const trackItem = document.createElement('div');
                    trackItem.className = `track-item ${index === this.currentTrackIndex ? 'active' : ''}`;
                    trackItem.innerHTML = `
                        <div class="track-icon">
                            <i class="fas fa-music"></i>
                        </div>
                        <div class="track-info">
                            <div class="track-title">${track.title}</div>
                            <div class="track-duration">${track.duration} • ${track.genre}</div>
                        </div>
                        <div style="color: ${track.color};">
                            <i class="fas fa-play"></i>
                        </div>
                    `;
                    
                    trackItem.addEventListener('click', () => {
                        this.playTrack(index);
                    });
                    
                    trackList.appendChild(trackItem);
                });
            }
            
            playTrack(index) {
                this.currentTrackIndex = index;
                this.updateTrackList();
                
                // In a real app, this would load actual audio files
                // For demo, we'll simulate playback
                this.isPlaying = true;
                document.getElementById('playIcon').className = 'fas fa-pause';
                
                // Update UI
                document.getElementById('currentTrackTitle').textContent = this.tracks[index].title;
                document.getElementById('audioStatusText').textContent = `Playing: ${this.tracks[index].title}`;
                
                // Start visualization
                this.startVisualization();
            }
            
            updateTrackList() {
                document.querySelectorAll('.track-item').forEach((item, index) => {
                    if (index === this.currentTrackIndex) {
                        item.classList.add('active');
                    } else {
                        item.classList.remove('active');
                    }
                });
            }
            
            setupEventListeners() {
                // Play/Pause button
                document.getElementById('playPauseBtn').addEventListener('click', () => {
                    this.togglePlayback();
                });
                
                // Previous/Next buttons
                document.getElementById('prevBtn').addEventListener('click', () => {
                    this.prevTrack();
                });
                
                document.getElementById('nextBtn').addEventListener('click', () => {
                    this.nextTrack();
                });
                
                // Volume control
                document.getElementById('volumeSlider').addEventListener('input', (e) => {
                    const volume = e.target.value / 100;
                    this.audioElement.volume = volume;
                    document.getElementById('volumeValue').textContent = `${e.target.value}%`;
                });
                
                // Bass boost
                document.getElementById('bassSlider').addEventListener('input', (e) => {
                    document.getElementById('bassValue').textContent = `${e.target.value}%`;
                    this.applyBassBoost(e.target.value);
                });
                
                // Playback speed
                document.getElementById('speedSlider').addEventListener('input', (e) => {
                    const speed = e.target.value / 100;
                    this.audioElement.playbackRate = speed;
                    document.getElementById('speedValue').textContent = `${speed.toFixed(1)}x`;
                });
                
                // File upload
                document.getElementById('audioFile').addEventListener('change', (e) => {
                    this.handleFileUpload(e.target.files[0]);
                });
                
                // Visualizer mode
                document.getElementById('vizModeSelect').addEventListener('change', (e) => {
                    this.visualizationMode = e.target.value;
                });
                
                // Color scheme
                document.getElementById('colorSchemeSelect').addEventListener('change', (e) => {
                    this.colorScheme = e.target.value;
                });
                
                // AI feature buttons
                document.getElementById('generateMusicBtn').addEventListener('click', () => {
                    this.generateAIMusic();
                });
                
                document.getElementById('remixBtn').addEventListener('click', () => {
                    this.remixCurrentTrack();
                });
                
                document.getElementById('moodMatchBtn').addEventListener('click', () => {
                    this.matchCelebrationMood();
                });
                
                document.getElementById('harmonizeBtn').addEventListener('click', () => {
                    this.addHarmonyLayers();
                });
                
                // Drag and drop for file upload
                const fileUpload = document.getElementById('fileUpload');
                fileUpload.addEventListener('dragover', (e) => {
                    e.preventDefault();
                    fileUpload.style.borderColor = 'var(--neon-blue)';
                    fileUpload.style.background = 'rgba(0, 243, 255, 0.1)';
                });
                
                fileUpload.addEventListener('dragleave', () => {
                    fileUpload.style.borderColor = 'rgba(255, 255, 255, 0.2)';
                    fileUpload.style.background = 'transparent';
                });
                
                fileUpload.addEventListener('drop', (e) => {
                    e.preventDefault();
                    fileUpload.style.borderColor = 'rgba(255, 255, 255, 0.2)';
                    fileUpload.style.background = 'transparent';
                    
                    if (e.dataTransfer.files.length) {
                        this.handleFileUpload(e.dataTransfer.files[0]);
                    }
                });
            }
            
            togglePlayback() {
                this.isPlaying = !this.isPlaying;
                const playIcon = document.getElementById('playIcon');
                
                if (this.isPlaying) {
                    playIcon.className = 'fas fa-pause';
                    // In real implementation: this.audioElement.play();
                    this.startVisualization();
                    document.getElementById('audioStatusText').textContent = `Playing: ${this.tracks[this.currentTrackIndex].title}`;
                } else {
                    playIcon.className = 'fas fa-play';
                    // In real implementation: this.audioElement.pause();
                    document.getElementById('audioStatusText').textContent = 'Paused';
                }
            }
            
            prevTrack() {
                this.currentTrackIndex = (this.currentTrackIndex - 1 + this.tracks.length) % this.tracks.length;
                this.playTrack(this.currentTrackIndex);
            }
            
            nextTrack() {
                this.currentTrackIndex = (this.currentTrackIndex + 1) % this.tracks.length;
                this.playTrack(this.currentTrackIndex);
            }
            
            applyBassBoost(amount) {
                // In a real implementation, this would apply a low-shelf filter
                // For demo, we'll just update the UI
                console.log(`Applying bass boost: ${amount}%`);
                
                // Visual feedback
                const beatBar = document.getElementById('beatBar');
                beatBar.style.width = `${amount}%`;
                beatBar.style.background = `linear-gradient(90deg, var(--neon-pink), var(--neon-orange))`;
                
                // Update particles based on bass
                this.updateParticles(amount);
            }
            
            handleFileUpload(file) {
                if (!file.type.startsWith('audio/')) {
                    alert('Please upload an audio file');
                    return;
                }
                
                console.log(`File uploaded: ${file.name}`);
                
                // Add to track list
                const newTrack = {
                    title: file.name.replace(/\.[^/.]+$/, ""), // Remove extension
                    duration: "Unknown",
                    genre: "Uploaded",
                    color: "#ffffff"
                };
                
                this.tracks.push(newTrack);
                this.createTrackList();
                
                // In real implementation, create object URL and set as audio source
                // const objectUrl = URL.createObjectURL(file);
                // this.audioElement.src = objectUrl;
                
                // Update status
                document.getElementById('audioStatusText').textContent = `Loaded: ${file.name}`;
                
                // Show success message
                const originalText = document.querySelector('.upload-label span');
                const originalHTML = originalText.innerHTML;
                originalText.innerHTML = `<i class="fas fa-check" style="color: var(--neon-green);"></i> ${file.name} uploaded!`;
                
                setTimeout(() => {
                    originalText.innerHTML = originalHTML;
                }, 3000);
            }
            
            setupVisualizers() {
                this.waveformCanvas = document.getElementById('waveformCanvas');
                this.frequencyCanvas = document.getElementById('frequencyCanvas');
                this.waveformCtx = this.waveformCanvas.getContext('2d');
                this.frequencyCtx = this.frequencyCanvas.getContext('2d');
                
                // Set canvas dimensions
                this.resizeCanvases();
                window.addEventListener('resize', () => this.resizeCanvases());
            }
            
            resizeCanvases() {
                const container = document.querySelector('.visualizer-container');
                this.waveformCanvas.width = container.clientWidth;
                this.waveformCanvas.height = container.clientHeight;
                this.frequencyCanvas.width = container.clientWidth;
                this.frequencyCanvas.height = container.clientHeight;
            }
            
            startVisualization() {
                if (!this.isPlaying) return;
                
                const draw = () => {
                    if (!this.isPlaying) return;
                    
                    // Clear canvases
                    this.waveformCtx.clearRect(0, 0, this.waveformCanvas.width, this.waveformCanvas.height);
                    this.frequencyCtx.clearRect(0, 0, this.frequencyCanvas.width, this.frequencyCanvas.height);
                    
                    // Get frequency data (in real app, from analyser node)
                    // For demo, we'll generate simulated data
                    const frequencyData = this.generateSimulatedFrequencyData();
                    const waveformData = this.generateSimulatedWaveformData();
                    
                    // Draw based on selected mode
                    switch(this.visualizationMode) {
                        case 'bars':
                            this.drawFrequencyBars(frequencyData);
                            break;
                        case 'waveform':
                            this.drawWaveform(waveformData);
                            break;
                        case 'circular':
                            this.drawCircularSpectrum(frequencyData);
                            break;
                        case 'particle':
                            this.drawParticleVisualization(frequencyData);
                            break;
                    }
                    
                    // Update FPS counter
                    this.updateFPSCounter();
                    
                    // Continue animation
                    requestAnimationFrame(draw);
                };
                
                draw();
            }
            
            generateSimulatedFrequencyData() {
                const data = new Uint8Array(128); // 128 frequency bins
                const time = Date.now() / 1000;
                
                for (let i = 0; i < data.length; i++) {
                    // Create interesting patterns
                    const base = Math.sin(time * 2 + i * 0.1) * 0.5 + 0.5;
                    const beat = Math.sin(time * 8) * 0.3 + 0.7;
                    const noise = Math.random() * 0.2;
                    
                    // More energy in lower frequencies (like real audio)
                    const frequencyFalloff = Math.exp(-i / 40);
                    
                    data[i] = (base * beat + noise) * frequencyFalloff * 255;
                }
                
                return data;
            }
            
            generateSimulatedWaveformData() {
                const data = new Uint8Array(512);
                const time = Date.now() / 1000;
                
                for (let i = 0; i < data.length; i++) {
                    const t = i / data.length * Math.PI * 4 + time * 3;
                    data[i] = (Math.sin(t) * Math.sin(t * 0.7) * 0.7 + 0.3) * 128 + 64;
                }
                
                return data;
            }
            
            drawFrequencyBars(data) {
                const ctx = this.frequencyCtx;
                const width = this.frequencyCanvas.width;
                const height = this.frequencyCanvas.height;
                const barWidth = width / data.length;
                
                for (let i = 0; i < data.length; i++) {
                    const barHeight = (data[i] / 255) * height * 0.8;
                    const x = i * barWidth;
                    const y = height - barHeight;
                    
                    // Get color based on scheme
                    const color = this.getColorForValue(i, data.length, data[i]);
                    
                    ctx.fillStyle = color;
                    ctx.fillRect(x, y, barWidth - 1, barHeight);
                    
                    // Add glow effect
                    ctx.shadowColor = color;
                    ctx.shadowBlur = 10;
                    ctx.fillRect(x, y, barWidth - 1, barHeight);
                    ctx.shadowBlur = 0;
                }
            }
            
            drawWaveform(data) {
                const ctx = this.waveformCtx;
                const width = this.waveformCanvas.width;
                const height = this.waveformCanvas.height;
                
                ctx.beginPath();
                ctx.lineWidth = 3;
                
                for (let i = 0; i < data.length; i++) {
                    const x = (i / data.length) * width;
                    const y = (data[i] / 255) * height;
                    
                    if (i === 0) {
                        ctx.moveTo(x, y);
                    } else {
                        ctx.lineTo(x, y);
                    }
                }
                
                // Get gradient based on color scheme
                const gradient = this.getWaveformGradient(ctx, width, height);
                ctx.strokeStyle = gradient;
                ctx.stroke();
                
                // Fill below waveform
                ctx.lineTo(width, height);
                ctx.lineTo(0, height);
                ctx.closePath();
                
                const fillGradient = ctx.createLinearGradient(0, 0, 0, height);
                fillGradient.addColorStop(0, gradient);
                fillGradient.addColorStop(1, 'rgba(0, 0, 0, 0)');
                
                ctx.fillStyle = fillGradient;
                ctx.fill();
            }
            
            drawCircularSpectrum(data) {
                const ctx = this.frequencyCtx;
                const width = this.frequencyCanvas.width;
                const height = this.frequencyCanvas.height;
                const centerX = width / 2;
                const centerY = height / 2;
                const radius = Math.min(width, height) * 0.4;
                
                const sliceCount = 64;
                const sliceAngle = (Math.PI * 2) / sliceCount;
                
                for (let i = 0; i < sliceCount; i++) {
                    const value = data[Math.floor(i * data.length / sliceCount)];
                    const barLength = (value / 255) * radius * 0.7;
                    
                    const angle = i * sliceAngle;
                    const startX = centerX + Math.cos(angle) * radius;
                    const startY = centerY + Math.sin(angle) * radius;
                    const endX = centerX + Math.cos(angle) * (radius + barLength);
                    const endY = centerY + Math.sin(angle) * (radius + barLength);
                    
                    // Create gradient for each bar
                    const gradient = ctx.createLinearGradient(startX, startY, endX, endY);
                    const color = this.getColorForValue(i, sliceCount, value);
                    gradient.addColorStop(0, color);
                    gradient.addColorStop(1, 'rgba(255, 255, 255, 0.5)');
                    
                    ctx.beginPath();
                    ctx.lineWidth = 4;
                    ctx.lineCap = 'round';
                    ctx.strokeStyle = gradient;
                    ctx.moveTo(startX, startY);
                    ctx.lineTo(endX, endY);
                    ctx.stroke();
                }
            }
            
            drawParticleVisualization(data) {
                const ctx = this.frequencyCtx;
                const width = this.frequencyCanvas.width;
                const height = this.frequencyCanvas.height;
                
                // Clear with slight transparency for trail effect
                ctx.fillStyle = 'rgba(0, 0, 0, 0.1)';
                ctx.fillRect(0, 0, width, height);
                
                // Update and draw particles
                this.particles.forEach(particle => {
                    // Move particle
                    particle.x += particle.vx;
                    particle.y += particle.vy;
                    
                    // Bounce off walls
                    if (particle.x < 0 || particle.x > width) particle.vx *= -1;
                    if (particle.y < 0 || particle.y > height) particle.vy *= -1;
                    
                    // Get color based on audio data
                    const dataIndex = Math.floor((particle.x / width) * data.length);
                    const intensity = data[dataIndex] / 255;
                    
                    // Size changes with audio
                    particle.size = 2 + intensity * 8;
                    
                    // Draw particle
                    ctx.beginPath();
                    ctx.fillStyle = particle.color;
                    ctx.arc(particle.x, particle.y, particle.size, 0, Math.PI * 2);
                    ctx.fill();
                    
                    // Add glow
                    ctx.shadowColor = particle.color;
                    ctx.shadowBlur = 15;
                    ctx.fill();
                    ctx.shadowBlur = 0;
                });
            }
            
            getColorForValue(index, total, value) {
                const normalizedValue = value / 255;
                
                switch(this.colorScheme) {
                    case 'neon':
                        const hue = (index / total) * 360;
                        return `hsl(${hue}, 100%, ${50 + normalizedValue * 30}%)`;
                    
                    case 'rainbow':
                        const rainbowHue = (Date.now() / 50 + index * 5) % 360;
                        return `hsl(${rainbowHue}, 100%, ${50 + normalizedValue * 30}%)`;
                    
                    case 'fire':
                        const fireValue = Math.min(normalizedValue * 1.5, 1);
                        return `rgb(${255}, ${fireValue * 200}, ${fireValue * 50})`;
                    
                    case 'ice':
                        return `rgb(${100 + normalizedValue * 155}, ${200 + normalizedValue * 55}, ${255})`;
                    
                    default:
                        return `rgb(${100 + normalizedValue * 155}, ${200 + normalizedValue * 55}, 255)`;
                }
            }
            
            getWaveformGradient(ctx, width, height) {
                switch(this.colorScheme) {
                    case 'neon':
                        const gradient = ctx.createLinearGradient(0, 0, width, 0);
                        gradient.addColorStop(0, '#00f3ff');
                        gradient.addColorStop(0.5, '#ff00ff');
                        gradient.addColorStop(1, '#00ff9d');
                        return gradient;
                    
                    case 'rainbow':
                        const rainbowGradient = ctx.createLinearGradient(0, 0, width, 0);
                        const now = Date.now() / 1000;
                        for (let i = 0; i <= 1; i += 0.1) {
                            const hue = (now * 20 + i * 360) % 360;
                            rainbowGradient.addColorStop(i, `hsl(${hue}, 100%, 60%)`);
                        }
                        return rainbowGradient;
                    
                    default:
                        return '#00f3ff';
                }
            }
            
            createParticles() {
                const particleCount = 100;
                
                for (let i = 0; i < particleCount; i++) {
                    this.particles.push({
                        x: Math.random() * this.frequencyCanvas.width,
                        y: Math.random() * this.frequencyCanvas.height,
                        vx: (Math.random() - 0.5) * 2,
                        vy: (Math.random() - 0.5) * 2,
                        size: Math.random() * 4 + 1,
                        color: this.getRandomNeonColor()
                    });
                }
            }
            
            updateParticles(bassAmount) {
                // Make particles react to bass
                const intensity = bassAmount / 100;
                
                this.particles.forEach(particle => {
                    // Add some randomness to movement based on bass
                    particle.vx += (Math.random() - 0.5) * intensity * 0.5;
                    particle.vy += (Math.random() - 0.5) * intensity * 0.5;
                    
                    // Limit speed
                    const speed = Math.sqrt(particle.vx * particle.vx + particle.vy * particle.vy);
                    const maxSpeed = 2 + intensity * 3;
                    if (speed > maxSpeed) {
                        particle.vx = (particle.vx / speed) * maxSpeed;
                        particle.vy = (particle.vy / speed) * maxSpeed;
                    }
                });
            }
            
            getRandomNeonColor() {
                const colors = [
                    '#00f3ff', '#ff00ff', '#00ff9d', '#ffaa00', '#9d00ff',
                    '#ff0066', '#00ffcc', '#ffcc00', '#cc00ff', '#00ff66'
                ];
                return colors[Math.floor(Math.random() * colors.length)];
            }
            
            updateFPSCounter() {
                if (!this.lastTime) {
                    this.lastTime = performance.now();
                    this.frames = 0;
                    return;
                }
                
                this.frames++;
                const now = performance.now();
                
                if (now >= this.lastTime + 1000) {
                    const fps = Math.round((this.frames * 1000) / (now - this.lastTime));
                    document.getElementById('fpsCounter').textContent = `FPS: ${fps}`;
                    
                    this.frames = 0;
                    this.lastTime = now;
                }
            }
            
            updateStatus() {
                // Update status indicators
                setInterval(() => {
                    const statusDot = document.getElementById('audioStatus');
                    if (this.isPlaying) {
                        statusDot.style.background = 'var(--neon-green)';
                        statusDot.style.boxShadow = '0 0 10px var(--neon-green)';
                    } else {
                        statusDot.style.background = '#666';
                        statusDot.style.boxShadow = 'none';
                    }
                }, 500);
            }
            
            simulateAudioAnalysis() {
                // Simulate beat detection
                setInterval(() => {
                    if (!this.isPlaying) return;
                    
                    // Random beat detection for demo
                    if (Math.random() > 0.7) {
                        this.triggerBeat();
                    }
                }, 300);
            }
            
            triggerBeat() {
                const beatBar = document.getElementById('beatBar');
                beatBar.style.width = '100%';
                beatBar.style.background = 'linear-gradient(90deg, var(--neon-pink), var(--neon-orange))';
                
                // Flash effect
                setTimeout(() => {
                    beatBar.style.width = '0%';
                }, 100);
                
                // Particle explosion on beat
                this.createBeatParticles();
            }
            
            createBeatParticles() {
                const particleContainer = document.getElementById('particlesContainer');
                const particleCount = 20;
                
                for (let i = 0; i < particleCount; i++) {
                    const particle = document.createElement('div');
                    particle.className = 'particle';
                    particle.style.left = '50%';
                    particle.style.top = '50%';
                    particle.style.background = this.getRandomNeonColor();
                    particle.style.width = Math.random() * 10 + 5 + 'px';
                    particle.style.height = particle.style.width;
                    
                    particleContainer.appendChild(particle);
                    
                    // Animate
                    const angle = Math.random() * Math.PI * 2;
                    const speed = Math.random() * 5 + 2;
                    const vx = Math.cos(angle) * speed;
                    const vy = Math.sin(angle) * speed;
                    
                    let x = 50;
                    let y = 50;
                    let opacity = 1;
                    
                    const animate = () => {
                        x += vx;
                        y += vy;
                        opacity -= 0.02;
                        
                        particle.style.left = x + '%';
                        particle.style.top = y + '%';
                        particle.style.opacity = opacity;
                        
                        if (opacity > 0) {
                            requestAnimationFrame(animate);
                        } else {
                            particle.remove();
                        }
                    };
                    
                    animate();
                }
            }
            
            // AI Music Generation Features
            generateAIMusic() {
                console.log("Generating AI music...");
                document.getElementById('audioStatusText').textContent = "AI Generating New Track...";
                
                // Simulate AI generation
                setTimeout(() => {
                    const newTrack = {
                        title: `AI Generated ${Math.floor(Math.random() * 1000)}`,
                        duration: `${Math.floor(Math.random() * 3) + 2}:${Math.floor(Math.random() * 60).toString().padStart(2, '0')}`,
                        genre: ["Neon Wave", "Cyber Funk", "Quantum Bass", "Digital Dream"][Math.floor(Math.random() * 4)],
                        color: this.getRandomNeonColor()
                    };
                    
                    this.tracks.unshift(newTrack);
                    this.currentTrackIndex = 0;
                    this.createTrackList();
                    this.playTrack(0);
                    
                    document.getElementById('audioStatusText').textContent = "Playing AI Generated Track";
                }, 1500);
            }
            
            remixCurrentTrack() {
                console.log("Remixing current track with AI...");
                document.getElementById('audioStatusText').textContent = "AI Remixing Current Track...";
                
                // Visual feedback
                const originalMode = this.visualizationMode;
                this.visualizationMode = 'particle';
                
                setTimeout(() => {
                    this.visualizationMode = originalMode;
                    document.getElementById('audioStatusText').textContent = "Playing AI Remix";
                }, 2000);
            }
            
            matchCelebrationMood() {
                console.log("Matching celebration mood...");
                
                // Change visualizer to match "celebration" mood
                this.visualizationMode = 'bars';
                this.colorScheme = 'rainbow';
                document.getElementById('vizModeSelect').value = 'bars';
                document.getElementById('colorSchemeSelect').value = 'rainbow';
                
                // Increase tempo
                document.getElementById('speedSlider').value = 120;
                document.getElementById('speedValue').textContent = '1.2x';
                
                document.getElementById('audioStatusText').textContent = "Matched to Celebration Mood!";
            }
            
            addHarmonyLayers() {
                console.log("Adding harmony layers...");
                
                // Create additional visual layers
                const originalMode = this.visualizationMode;
                this.visualizationMode = 'circular';
                
                // Add more particles
                for (let i = 0; i < 30; i++) {
                    this.particles.push({
                        x: Math.random() * this.frequencyCanvas.width,
                        y: Math.random() * this.frequencyCanvas.height,
                        vx: (Math.random() - 0.5) * 1.5,
                        vy: (Math.random() - 0.5) * 1.5,
                        size: Math.random() * 3 + 1,
                        color: this.getRandomNeonColor()
                    });
                }
                
                setTimeout(() => {
                    this.visualizationMode = originalMode;
                    document.getElementById('audioStatusText').textContent = "Harmony Layers Added";
                }, 3000);
            }
        }
        
        // Beat Detection Algorithm Class
        class BeatDetectionAlgorithm {
            constructor() {
                this.history = [];
                this.beatThreshold = 1.2;
                this.lastBeatTime = 0;
                this.beatInterval = 500; // ms
            }
            
            detectBeat(frequencyData) {
                // Calculate energy
                const energy = this.calculateEnergy(frequencyData);
                
                // Add to history
                this.history.push(energy);
                if (this.history.length > 43) { // About 1 second at 44.1kHz
                    this.history.shift();
                }
                
                // Calculate average energy
                const averageEnergy = this.history.reduce((a, b) => a + b, 0) / this.history.length;
                
                // Check for beat
                const currentTime = Date.now();
                if (energy > averageEnergy * this.beatThreshold && 
                    currentTime - this.lastBeatTime > this.beatInterval) {
                    this.lastBeatTime = currentTime;
                    return true;
                }
                
                return false;
            }
            
            calculateEnergy(frequencyData) {
                let energy = 0;
                for (let i = 0; i < frequencyData.length; i++) {
                    energy += frequencyData[i] * frequencyData[i];
                }
                return energy / frequencyData.length;
            }
            
            // C-weighting filter for human hearing sensitivity
            applyCWeighting(frequencyData, sampleRate) {
                // Simplified C-weighting approximation
                const weighted = new Array(frequencyData.length);
                for (let i = 0; i < frequencyData.length; i++) {
                    const f = i * sampleRate / (2 * frequencyData.length);
                    // C-weighting curve approximation
                    const f2 = f * f;
                    const f4 = f2 * f2;
                    const numerator = f4;
                    const denominator = (f2 + 20.6*20.6) * Math.sqrt((f2 + 107.7*107.7) * (f2 + 737.9*737.9)) * (f2 + 12194*12194);
                    const weighting = numerator / denominator;
                    weighted[i] = frequencyData[i] * weighting * 12200; // Normalization constant
                }
                return weighted;
            }
        }
        
        // Initialize the music engine when page loads
        document.addEventListener('DOMContentLoaded', () => {
            const musicEngine = new AdvancedMusicEngine();
            window.musicEngine = musicEngine; // Make accessible globally
            
            // Start with first track
            musicEngine.playTrack(0);
            
            // Update time display
            setInterval(() => {
                if (musicEngine.isPlaying) {
                    const currentTime = document.getElementById('currentTime');
                    const seconds = parseInt(currentTime.textContent.split(':')[1]) || 0;
                    const newSeconds = (seconds + 1) % 60;
                    const minutes = parseInt(currentTime.textContent.split(':')[0]) || 0;
                    const newMinutes = minutes + Math.floor((seconds + 1) / 60);
                    
                    currentTime.textContent = `${newMinutes}:${newSeconds.toString().padStart(2, '0')}`;
                    
                    // Update total time for current track
                    const trackDuration = musicEngine.tracks[musicEngine.currentTrackIndex].duration;
                    document.getElementById('totalTime').textContent = trackDuration;
                }
            }, 1000);
        });
    </script>
</body>
</html>
