<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Compact CNN Smart Mirror</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Arial', sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
        }

        .mirror {
            width: 90%;
            max-width: 800px;
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(15px);
            border-radius: 20px;
            padding: 30px;
            border: 1px solid rgba(255, 255, 255, 0.2);
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.1);
        }

        .title {
            text-align: center;
            font-size: 2rem;
            margin-bottom: 30px;
            text-shadow: 0 2px 4px rgba(0, 0, 0, 0.3);
        }

        .sections {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
            gap: 20px;
            margin-bottom: 25px;
        }

        .section {
            background: rgba(255, 255, 255, 0.15);
            border-radius: 12px;
            padding: 20px;
            text-align: center;
            transition: transform 0.3s ease;
        }

        .section:hover {
            transform: translateY(-3px);
        }

        .section-title {
            font-size: 1.2rem;
            margin-bottom: 15px;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
        }

        .metric {
            display: flex;
            justify-content: space-between;
            margin: 8px 0;
            padding: 8px;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 6px;
        }

        .score {
            font-size: 2.5rem;
            font-weight: bold;
            color: #4ecdc4;
            margin: 15px 0;
            text-shadow: 0 2px 4px rgba(0, 0, 0, 0.3);
        }

        .mood-emoji {
            font-size: 3rem;
            margin: 10px 0;
            animation: bounce 2s infinite;
        }

        @keyframes bounce {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-5px); }
        }

        .controls {
            display: flex;
            justify-content: center;
            gap: 15px;
            flex-wrap: wrap;
        }

        .btn {
            padding: 10px 20px;
            background: linear-gradient(135deg, #4ecdc4, #44a08d);
            border: none;
            border-radius: 20px;
            color: white;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
        }

        .progress {
            width: 100%;
            height: 6px;
            background: rgba(255, 255, 255, 0.2);
            border-radius: 3px;
            overflow: hidden;
            margin-top: 8px;
        }

        .progress-bar {
            height: 100%;
            background: linear-gradient(90deg, #ff6b6b, #4ecdc4);
            transition: width 1s ease;
        }

        .timestamp {
            text-align: center;
            margin-top: 20px;
            opacity: 0.7;
            font-size: 0.9rem;
        }

        @media (max-width: 600px) {
            .sections {
                grid-template-columns: 1fr;
            }
            .controls {
                flex-direction: column;
                align-items: center;
            }
        }
    </style>
</head>
<body>
    <div class="mirror">
        <h1 class="title">🪞 CNN Smart Mirror</h1>
        
        <div class="sections">
            <!-- Skin Analysis -->
            <div class="section">
                <div class="section-title">🧴 Skin Analysis</div>
                <div class="metric">
                    <span>Acne:</span>
                    <span id="acne">2</span>
                </div>
                <div class="progress">
                    <div class="progress-bar" id="acne-bar" style="width: 40%"></div>
                </div>
                
                <div class="metric">
                    <span>Wrinkles:</span>
                    <span id="wrinkles">1</span>
                </div>
                <div class="progress">
                    <div class="progress-bar" id="wrinkles-bar" style="width: 20%"></div>
                </div>
                
                <div class="metric">
                    <span>Dark Spots:</span>
                    <span id="dark-spots">3</span>
                </div>
                <div class="progress">
                    <div class="progress-bar" id="spots-bar" style="width: 60%"></div>
                </div>
                
                <div class="score" id="skin-score">7.33</div>
            </div>

            <!-- Outfit Matching -->
            <div class="section">
                <div class="section-title">👔 Outfit Match</div>
                <div class="metric">
                    <span>Formal:</span>
                    <span>80%</span>
                </div>
                <div class="progress">
                    <div class="progress-bar" style="width: 80%"></div>
                </div>
                
                <div class="metric">
                    <span>Sporty:</span>
                    <span>10%</span>
                </div>
                <div class="progress">
                    <div class="progress-bar" style="width: 10%"></div>
                </div>
                
                <div class="metric">
                    <span>Casual:</span>
                    <span>10%</span>
                </div>
                <div class="progress">
                    <div class="progress-bar" style="width: 10%"></div>
                </div>
                
                <div class="score" id="best-outfit">Outfit #3</div>
            </div>

            <!-- Mood Detection -->
            <div class="section">
                <div class="section-title">😊 Mood Detection</div>
                <div class="metric">
                    <span>Happy:</span>
                    <span id="happy">20%</span>
                </div>
                <div class="progress">
                    <div class="progress-bar" id="happy-bar" style="width: 20%"></div>
                </div>
                
                <div class="metric">
                    <span>Tired:</span>
                    <span id="tired">70%</span>
                </div>
                <div class="progress">
                    <div class="progress-bar" id="tired-bar" style="width: 70%"></div>
                </div>
                
                <div class="metric">
                    <span>Stressed:</span>
                    <span id="stressed">10%</span>
                </div>
                <div class="progress">
                    <div class="progress-bar" id="stressed-bar" style="width: 10%"></div>
                </div>
                
                <div class="mood-emoji" id="mood-emoji">😴</div>
                <div id="mood-text">TIRED</div>
            </div>
        </div>

        <div class="controls">
            <button class="btn" onclick="analyzeSkin()">Analyze Skin</button>
            <button class="btn" onclick="matchOutfit()">Match Outfit</button>
            <button class="btn" onclick="detectMood()">Detect Mood</button>
            <button class="btn" onclick="runAll()">Full Scan</button>
        </div>

        <div class="timestamp">
            Last scan: <span id="time"></span>
        </div>
    </div>

    <script>
        class SmartMirror {
            constructor() {
                this.skinData = { acne: 2, wrinkles: 1, darkSpots: 3 };
                this.moodData = { happy: 0.2, tired: 0.7, stressed: 0.1 };
                this.outfitVectors = [[0.7, 0.2, 0.1], [0.3, 0.6, 0.1], [0.9, 0.05, 0.05]];
                this.updateTime();
            }

            // Skin Score Calculation
            calculateSkinScore() {
                const { acne, wrinkles, darkSpots } = this.skinData;
                const score = 10 - (acne * 1.5 + wrinkles * 1.2 + darkSpots * 1.0);
                const finalScore = Math.max(0, Math.min(10, score));
                
                this.animateValue('skin-score', finalScore.toFixed(2));
                return finalScore;
            }

            // Outfit Matching with Cosine Similarity
            matchOutfit() {
                const eventVector = [0.8, 0.1, 0.1]; // Formal event
                let bestMatch = 0;
                let highestSim = -1;

                this.outfitVectors.forEach((outfit, i) => {
                    const similarity = this.cosineSimilarity(eventVector, outfit);
                    if (similarity > highestSim) {
                        highestSim = similarity;
                        bestMatch = i;
                    }
                });

                document.getElementById('best-outfit').textContent = `Outfit #${bestMatch + 1}`;
                return bestMatch;
            }

            // Cosine Similarity
            cosineSimilarity(a, b) {
                const dot = a.reduce((sum, ai, i) => sum + ai * b[i], 0);
                const magA = Math.sqrt(a.reduce((sum, ai) => sum + ai * ai, 0));
                const magB = Math.sqrt(b.reduce((sum, bi) => sum + bi * bi, 0));
                return dot / (magA * magB);
            }

            // Mood Detection
            detectMood() {
                const dominant = Object.keys(this.moodData).reduce((a, b) => 
                    this.moodData[a] > this.moodData[b] ? a : b
                );

                const emojis = { happy: '😊', tired: '😴', stressed: '😰' };
                document.getElementById('mood-emoji').textContent = emojis[dominant];
                document.getElementById('mood-text').textContent = dominant.toUpperCase();
                
                return dominant;
            }

            // Generate random data for demo
            randomizeData() {
                this.skinData.acne = Math.floor(Math.random() * 5);
                this.skinData.wrinkles = Math.floor(Math.random() * 4);
                this.skinData.darkSpots = Math.floor(Math.random() * 5);

                // Randomize mood (ensure they sum to 1)
                const values = [Math.random(), Math.random(), Math.random()];
                const sum = values.reduce((a, b) => a + b, 0);
                this.moodData.happy = values[0] / sum;
                this.moodData.tired = values[1] / sum;
                this.moodData.stressed = values[2] / sum;
            }

            // Update UI elements
            updateSkinUI() {
                document.getElementById('acne').textContent = this.skinData.acne;
                document.getElementById('wrinkles').textContent = this.skinData.wrinkles;
                document.getElementById('dark-spots').textContent = this.skinData.darkSpots;
                
                document.getElementById('acne-bar').style.width = (this.skinData.acne * 20) + '%';
                document.getElementById('wrinkles-bar').style.width = (this.skinData.wrinkles * 25) + '%';
                document.getElementById('spots-bar').style.width = (this.skinData.darkSpots * 20) + '%';
            }

            updateMoodUI() {
                document.getElementById('happy').textContent = Math.round(this.moodData.happy * 100) + '%';
                document.getElementById('tired').textContent = Math.round(this.moodData.tired * 100) + '%';
                document.getElementById('stressed').textContent = Math.round(this.moodData.stressed * 100) + '%';
                
                document.getElementById('happy-bar').style.width = (this.moodData.happy * 100) + '%';
                document.getElementById('tired-bar').style.width = (this.moodData.tired * 100) + '%';
                document.getElementById('stressed-bar').style.width = (this.moodData.stressed * 100) + '%';
            }

            // Animation helper
            animateValue(id, value) {
                const element = document.getElementById(id);
                element.style.transform = 'scale(1.1)';
                setTimeout(() => {
                    element.textContent = value;
                    element.style.transform = 'scale(1)';
                }, 200);
            }

            updateTime() {
                document.getElementById('time').textContent = new Date().toLocaleTimeString();
            }
        }

        // Initialize mirror
        const mirror = new SmartMirror();

        // Button functions
        function analyzeSkin() {
            mirror.randomizeData();
            mirror.updateSkinUI();
            mirror.calculateSkinScore();
            mirror.updateTime();
        }

        function matchOutfit() {
            mirror.matchOutfit();
            mirror.updateTime();
        }

        function detectMood() {
            mirror.randomizeData();
            mirror.updateMoodUI(); 
            mirror.detectMood();
            mirror.updateTime();
        }

        function runAll() {
            analyzeSkin();
            setTimeout(matchOutfit, 300);
            setTimeout(detectMood, 600);
        }
    </script>
</body>
</html>
