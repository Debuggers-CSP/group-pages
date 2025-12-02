---
layout: post
title: Character Creation
description: Let the user create character
permalink: /rpg/character-creation
comments: True
---

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>RPG Character Creation</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background-color: #1a1a2e;
            color: #e6e6e6;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            padding: 20px;
        }
        
        .container {
            max-width: 1200px;
            width: 100%;
            display: flex;
            flex-direction: column;
            gap: 30px;
        }
        
        header {
            text-align: center;
            padding: 20px;
            border-bottom: 2px solid #4cc9f0;
            margin-bottom: 20px;
        }
        
        h1 {
            font-size: 2.8rem;
            color: #4cc9f0;
            text-shadow: 0 0 10px rgba(76, 201, 240, 0.5);
            margin-bottom: 10px;
            letter-spacing: 1px;
        }
        
        .subtitle {
            font-size: 1.2rem;
            color: #a9a9b3;
            max-width: 600px;
            margin: 0 auto;
        }
        
        .main-content {
            display: flex;
            flex-wrap: wrap;
            gap: 40px;
        }
        
        .options-panel {
            flex: 1;
            min-width: 300px;
            background-color: #16213e;
            border-radius: 15px;
            padding: 25px;
            box-shadow: 0 8px 25px rgba(0, 0, 0, 0.4);
        }
        
        .preview-panel {
            flex: 1;
            min-width: 300px;
            background-color: #16213e;
            border-radius: 15px;
            padding: 25px;
            display: flex;
            flex-direction: column;
            align-items: center;
            box-shadow: 0 8px 25px rgba(0, 0, 0, 0.4);
        }
        
        .section-title {
            font-size: 1.5rem;
            color: #4cc9f0;
            margin-bottom: 20px;
            padding-bottom: 10px;
            border-bottom: 1px solid #2d374d;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .section-title i {
            font-size: 1.3rem;
        }
        
        .option-group {
            margin-bottom: 30px;
        }
        
        .option-label {
            display: block;
            font-size: 1.1rem;
            margin-bottom: 12px;
            color: #b8c1d9;
        }
        
        .class-selector {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(140px, 1fr));
            gap: 12px;
        }
        
        .class-option {
            background-color: #0f3460;
            border: 2px solid #2d374d;
            border-radius: 10px;
            padding: 15px 10px;
            text-align: center;
            cursor: pointer;
            transition: all 0.3s ease;
        }
        
        .class-option:hover {
            transform: translateY(-5px);
            border-color: #4cc9f0;
            box-shadow: 0 5px 15px rgba(76, 201, 240, 0.2);
        }
        
        .class-option.selected {
            border-color: #4cc9f0;
            background-color: rgba(76, 201, 240, 0.1);
            box-shadow: 0 0 15px rgba(76, 201, 240, 0.3);
        }
        
        .class-icon {
            font-size: 2rem;
            margin-bottom: 8px;
            color: #4cc9f0;
        }
        
        .class-name {
            font-weight: 600;
            font-size: 1.1rem;
        }
        
        .color-selector {
            display: flex;
            flex-wrap: wrap;
            gap: 15px;
        }
        
        .color-option {
            width: 50px;
            height: 50px;
            border-radius: 50%;
            cursor: pointer;
            border: 3px solid transparent;
            transition: all 0.2s ease;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.3);
        }
        
        .color-option:hover {
            transform: scale(1.1);
        }
        
        .color-option.selected {
            border-color: white;
            transform: scale(1.1);
            box-shadow: 0 0 15px rgba(255, 255, 255, 0.5);
        }
        
        .color-label {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 15px;
        }
        
        .selected-color-hex {
            background-color: #0f3460;
            padding: 5px 12px;
            border-radius: 20px;
            font-family: monospace;
            font-size: 1rem;
            color: #e6e6e6;
        }
        
        .pixel-canvas-container {
            background-color: #0f3460;
            border-radius: 10px;
            padding: 20px;
            margin-bottom: 25px;
            width: 100%;
            display: flex;
            justify-content: center;
            align-items: center;
        }
        
        .pixel-canvas {
            image-rendering: pixelated;
            image-rendering: crisp-edges;
            width: 200px;
            height: 200px;
            background-color: #1a1a2e;
            border-radius: 5px;
        }
        
        .character-details {
            width: 100%;
            background-color: #0f3460;
            border-radius: 10px;
            padding: 20px;
            margin-top: 10px;
        }
        
        .detail-row {
            display: flex;
            justify-content: space-between;
            margin-bottom: 10px;
            padding-bottom: 10px;
            border-bottom: 1px solid #2d374d;
        }
        
        .detail-label {
            color: #b8c1d9;
        }
        
        .detail-value {
            font-weight: 600;
            color: #4cc9f0;
        }
        
        .action-buttons {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin-top: 30px;
            flex-wrap: wrap;
        }
        
        .btn {
            padding: 15px 30px;
            border: none;
            border-radius: 10px;
            font-size: 1.1rem;
            font-weight: 600;
            cursor: pointer;
            display: flex;
            align-items: center;
            gap: 10px;
            transition: all 0.3s ease;
        }
        
        .btn-reset {
            background-color: #7a7a8c;
            color: white;
        }
        
        .btn-reset:hover {
            background-color: #5a5a6c;
            transform: translateY(-3px);
        }
        
        .btn-confirm {
            background-color: #4cc9f0;
            color: #1a1a2e;
        }
        
        .btn-confirm:hover {
            background-color: #3aa8d8;
            transform: translateY(-3px);
            box-shadow: 0 5px 15px rgba(76, 201, 240, 0.4);
        }
        
        footer {
            margin-top: 30px;
            text-align: center;
            color: #7a7a8c;
            font-size: 0.9rem;
            padding: 20px;
            border-top: 1px solid #2d374d;
            width: 100%;
        }
        
        @media (max-width: 768px) {
            .main-content {
                flex-direction: column;
            }
            
            h1 {
                font-size: 2.2rem;
            }
            
            .class-selector {
                grid-template-columns: repeat(2, 1fr);
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>Character Creation</h1>
            <p class="subtitle">Choose your character's class and customize their appearance. Your pixel art character will update in real-time.</p>
        </header>
        
        <div class="main-content">
            <div class="options-panel">
                <div class="option-group">
                    <h2 class="section-title"><i class="fas fa-helmet-battle"></i> Character Class</h2>
                    <div class="class-selector" id="classSelector">
                        <!-- Class options will be generated by JavaScript -->
                    </div>
                </div>
                
                <div class="option-group">
                    <div class="color-label">
                        <h2 class="section-title"><i class="fas fa-palette"></i> Hair Color</h2>
                        <div class="selected-color-hex" id="hairColorHex">#D4A017</div>
                    </div>
                    <div class="color-selector" id="hairColorSelector">
                        <!-- Hair color options will be generated by JavaScript -->
                    </div>
                </div>
                
                <div class="option-group">
                    <div class="color-label">
                        <h2 class="section-title"><i class="fas fa-tshirt"></i> Clothing Color</h2>
                        <div class="selected-color-hex" id="clothingColorHex">#4361EE</div>
                    </div>
                    <div class="color-selector" id="clothingColorSelector">
                        <!-- Clothing color options will be generated by JavaScript -->
                    </div>
                </div>
            </div>
            
            <div class="preview-panel">
                <h2 class="section-title"><i class="fas fa-eye"></i> Character Preview</h2>
                
                <div class="pixel-canvas-container">
                    <canvas id="characterCanvas" class="pixel-canvas" width="16" height="16"></canvas>
                </div>
                
                <div class="character-details">
                    <div class="detail-row">
                        <span class="detail-label">Class:</span>
                        <span class="detail-value" id="previewClass">Warrior</span>
                    </div>
                    <div class="detail-row">
                        <span class="detail-label">Hair Color:</span>
                        <span class="detail-value" id="previewHairColor">Golden</span>
                    </div>
                    <div class="detail-row">
                        <span class="detail-label">Clothing Color:</span>
                        <span class="detail-value" id="previewClothingColor">Royal Blue</span>
                    </div>
                </div>
            </div>
        </div>
        
        <div class="action-buttons">
            <button class="btn btn-reset" id="resetButton">
                <i class="fas fa-redo"></i> Reset
            </button>
            <button class="btn btn-confirm" id="confirmButton">
                <i class="fas fa-check-circle"></i> Confirm Character
            </button>
        </div>
        
        <footer>
            <p>RPG Character Creator | Use your created character in your next adventure!</p>
        </footer>
    </div>

    <script>
        // Character class data
        const characterClasses = [
            { id: 'warrior', name: 'Warrior', icon: 'fas fa-shield-alt', color: '#4361ee', defaultHair: '#D4A017', defaultClothing: '#4361EE' },
            { id: 'mage', name: 'Mage', icon: 'fas fa-hat-wizard', color: '#9d4edd', defaultHair: '#F77F00', defaultClothing: '#9D4EDD' },
            { id: 'archer', name: 'Archer', icon: 'fas fa-bow-arrow', color: '#2a9d8f', defaultHair: '#A8DADC', defaultClothing: '#2A9D8F' },
            { id: 'rogue', name: 'Rogue', icon: 'fas fa-user-ninja', color: '#e63946', defaultHair: '#1D3557', defaultClothing: '#E63946' },
            { id: 'cleric', name: 'Cleric', icon: 'fas fa-pray', color: '#ff9e00', defaultHair: '#F1FAEE', defaultClothing: '#FF9E00' },
            { id: 'monk', name: 'Monk', icon: 'fas fa-fist-raised', color: '#588157', defaultHair: '#8D99AE', defaultClothing: '#588157' }
        ];

        // Color palettes
        const hairColors = [
            { name: 'Golden', value: '#D4A017' },
            { name: 'Blonde', value: '#F6DCAC' },
            { name: 'Brown', value: '#8B4513' },
            { name: 'Black', value: '#1D1D1D' },
            { name: 'Red', value: '#A41623' },
            { name: 'White', value: '#F8F9FA' },
            { name: 'Silver', value: '#C0C0C0' },
            { name: 'Blue', value: '#4A90E2' }
        ];

        const clothingColors = [
            { name: 'Royal Blue', value: '#4361EE' },
            { name: 'Crimson', value: '#A41623' },
            { name: 'Forest Green', value: '#2A9D8F' },
            { name: 'Deep Purple', value: '#7209B7' },
            { name: 'Shadow Black', value: '#212529' },
            { name: 'Steel Gray', value: '#6C757D' },
            { name: 'Gold', value: '#FF9E00' },
            { name: 'White', value: '#F8F9FA' }
        ];

        // Current selections
        let currentClass = 'warrior';
        let currentHairColor = '#D4A017';
        let currentClothingColor = '#4361EE';

        // Initialize the page
        document.addEventListener('DOMContentLoaded', function() {
            initializeClassSelector();
            initializeColorSelectors();
            updateCharacterPreview();
            setupEventListeners();
        });

        // Initialize class selection options
        function initializeClassSelector() {
            const classSelector = document.getElementById('classSelector');
            
            characterClasses.forEach(cls => {
                const classOption = document.createElement('div');
                classOption.className = `class-option ${cls.id === currentClass ? 'selected' : ''}`;
                classOption.dataset.classId = cls.id;
                
                classOption.innerHTML = `
                    <div class="class-icon"><i class="${cls.icon}"></i></div>
                    <div class="class-name">${cls.name}</div>
                `;
                
                classOption.addEventListener('click', () => {
                    document.querySelectorAll('.class-option').forEach(opt => opt.classList.remove('selected'));
                    classOption.classList.add('selected');
                    
                    currentClass = cls.id;
                    // Update default colors for this class
                    const selectedClass = characterClasses.find(c => c.id === currentClass);
                    currentHairColor = selectedClass.defaultHair;
                    currentClothingColor = selectedClass.defaultClothing;
                    
                    updateColorSelections();
                    updateCharacterPreview();
                });
                
                classSelector.appendChild(classOption);
            });
        }

        // Initialize color selection options
        function initializeColorSelectors() {
            const hairColorSelector = document.getElementById('hairColorSelector');
            const clothingColorSelector = document.getElementById('clothingColorSelector');
            
            // Hair colors
            hairColors.forEach(color => {
                const colorOption = document.createElement('div');
                colorOption.className = `color-option ${color.value === currentHairColor ? 'selected' : ''}`;
                colorOption.style.backgroundColor = color.value;
                colorOption.dataset.colorValue = color.value;
                colorOption.dataset.colorName = color.name;
                
                colorOption.addEventListener('click', () => {
                    document.querySelectorAll('#hairColorSelector .color-option').forEach(opt => opt.classList.remove('selected'));
                    colorOption.classList.add('selected');
                    
                    currentHairColor = color.value;
                    document.getElementById('hairColorHex').textContent = color.value;
                    updateCharacterPreview();
                });
                
                hairColorSelector.appendChild(colorOption);
            });
            
            // Clothing colors
            clothingColors.forEach(color => {
                const colorOption = document.createElement('div');
                colorOption.className = `color-option ${color.value === currentClothingColor ? 'selected' : ''}`;
                colorOption.style.backgroundColor = color.value;
                colorOption.dataset.colorValue = color.value;
                colorOption.dataset.colorName = color.name;
                
                colorOption.addEventListener('click', () => {
                    document.querySelectorAll('#clothingColorSelector .color-option').forEach(opt => opt.classList.remove('selected'));
                    colorOption.classList.add('selected');
                    
                    currentClothingColor = color.value;
                    document.getElementById('clothingColorHex').textContent = color.value;
                    updateCharacterPreview();
                });
                
                clothingColorSelector.appendChild(colorOption);
            });
        }

        // Update color selections after class change
        function updateColorSelections() {
            // Update hair color selection
            document.querySelectorAll('#hairColorSelector .color-option').forEach(opt => {
                opt.classList.toggle('selected', opt.dataset.colorValue === currentHairColor);
            });
            document.getElementById('hairColorHex').textContent = currentHairColor;
            
            // Update clothing color selection
            document.querySelectorAll('#clothingColorSelector .color-option').forEach(opt => {
                opt.classList.toggle('selected', opt.dataset.colorValue === currentClothingColor);
            });
            document.getElementById('clothingColorHex').textContent = currentClothingColor;
        }

        // Update character preview canvas
        function updateCharacterPreview() {
            const canvas = document.getElementById('characterCanvas');
            const ctx = canvas.getContext('2d');
            
            // Clear canvas
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            
            // Get selected class data
            const selectedClass = characterClasses.find(c => c.id === currentClass);
            
            // Update text details
            document.getElementById('previewClass').textContent = selectedClass.name;
            document.getElementById('previewHairColor').textContent = 
                hairColors.find(c => c.value === currentHairColor)?.name || 'Custom';
            document.getElementById('previewClothingColor').textContent = 
                clothingColors.find(c => c.value === currentClothingColor)?.name || 'Custom';
            
            // Draw pixel art character based on class
            drawPixelCharacter(ctx, selectedClass.id);
        }

        // Draw pixel character based on class
        function drawPixelCharacter(ctx, classId) {
            // Base character shape (same for all classes)
            const skinColor = '#F8C8B0';
            const pantsColor = '#2D1B00';
            const bootColor = '#1A1A1A';
            
            // Draw skin (body)
            ctx.fillStyle = skinColor;
            // Head
            ctx.fillRect(6, 1, 4, 3);
            // Body
            ctx.fillRect(5, 4, 6, 5);
            
            // Draw hair
            ctx.fillStyle = currentHairColor;
            ctx.fillRect(5, 0, 6, 2);
            ctx.fillRect(4, 1, 8, 2);
            ctx.fillRect(5, 3, 6, 1);
            
            // Draw clothing (class-specific)
            ctx.fillStyle = currentClothingColor;
            
            // Class-specific clothing patterns
            if (classId === 'warrior') {
                // Warrior armor
                ctx.fillRect(5, 4, 6, 2);
                // Shoulder pads
                ctx.fillRect(3, 5, 2, 2);
                ctx.fillRect(11, 5, 2, 2);
            } else if (classId === 'mage') {
                // Mage robe
                ctx.fillRect(5, 4, 6, 5);
                // Robe triangle bottom
                ctx.fillRect(6, 9, 4, 1);
                ctx.fillRect(7, 10, 2, 1);
            } else if (classId === 'archer') {
                // Archer tunic
                ctx.fillRect(5, 4, 6, 3);
                // Quiver
                ctx.fillRect(12, 4, 2, 4);
            } else if (classId === 'rogue') {
                // Rogue hood and torso
                ctx.fillRect(5, 2, 6, 1);
                ctx.fillRect(5, 4, 6, 3);
            } else if (classId === 'cleric') {
                // Cleric robe with cross
                ctx.fillRect(5, 4, 6, 5);
                // Cross symbol
                ctx.fillStyle = '#FFD700';
                ctx.fillRect(7, 5, 2, 3);
                ctx.fillRect(6, 6, 4, 1);
            } else if (classId === 'monk') {
                // Monk simple robe
                ctx.fillRect(5, 4, 6, 5);
                // Belt
                ctx.fillStyle = '#8B4513';
                ctx.fillRect(5, 7, 6, 1);
            }
            
            // Draw pants
            ctx.fillStyle = pantsColor;
            ctx.fillRect(5, 9, 6, 3);
            
            // Draw boots
            ctx.fillStyle = bootColor;
            ctx.fillRect(4, 12, 3, 2);
            ctx.fillRect(9, 12, 3, 2);
            
            // Draw class-specific equipment
            ctx.fillStyle = '#FFFFFF';
            if (classId === 'warrior') {
                // Sword
                ctx.fillRect(1, 5, 3, 1);
                ctx.fillRect(2, 4, 1, 3);
            } else if (classId === 'mage') {
                // Staff
                ctx.fillRect(1, 3, 1, 10);
                ctx.fillRect(0, 3, 3, 1);
            } else if (classId === 'archer') {
                // Bow
                ctx.fillRect(1, 6, 4, 1);
                ctx.fillRect(2, 5, 2, 3);
            } else if (classId === 'rogue') {
                // Dagger
                ctx.fillRect(1, 7, 2, 1);
                ctx.fillRect(2, 6, 1, 3);
            }
        }

        // Set up event listeners for buttons
        function setupEventListeners() {
            // Reset button
            document.getElementById('resetButton').addEventListener('click', function() {
                // Reset to default warrior
                document.querySelectorAll('.class-option').forEach(opt => opt.classList.remove('selected'));
                document.querySelector('.class-option[data-class-id="warrior"]').classList.add('selected');
                
                currentClass = 'warrior';
                const warriorClass = characterClasses.find(c => c.id === 'warrior');
                currentHairColor = warriorClass.defaultHair;
                currentClothingColor = warriorClass.defaultClothing;
                
                updateColorSelections();
                updateCharacterPreview();
            });
            
            // Confirm button
            document.getElementById('confirmButton').addEventListener('click', function() {
                const selectedClass = characterClasses.find(c => c.id === currentClass);
                const hairColorName = hairColors.find(c => c.value === currentHairColor)?.name || 'Custom';
                const clothingColorName = clothingColors.find(c => c.value === currentClothingColor)?.name || 'Custom';
                
                alert(`Character Created!\n\nClass: ${selectedClass.name}\nHair Color: ${hairColorName}\nClothing Color: ${clothingColorName}\n\nYour character is ready for adventure!`);
            });
        }
    </script>
</body>
</html>