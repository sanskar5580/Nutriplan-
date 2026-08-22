# NutriPlan-
NutriPlan is a personalized diet recommendation web application that helps users make healthier food choices based on their age, weight, height, activity level, dietary preferences, and fitness goals. It calculates BMI and daily calorie requirements and provides suitable meal recommendations for breakfast, lunch, snacks, and dinner
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NutriPlan - Your Personal Diet Guide</title>
    <style>
        /* --- General Reset and Body Styles (From NutriPlan) --- */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            display: flex; /* Flexbox for centering */
            justify-content: center;
            align-items: center;
            padding: 20px;
            transition: all 0.5s ease; /* For smooth transition on login */
        }

        /* --- Auth Page Styles (Login & Signup) --- */
        .auth-container {
            background: white;
            padding: 40px 30px;
            border-radius: 12px;
            box-shadow: 0 8px 20px rgba(0,0,0,0.3);
            width: 350px;
            text-align: center;
            z-index: 10;
            animation: fadeInUp 0.8s ease;
        }

        .auth-container h2 {
            margin-bottom: 25px;
            color: #667eea;
            font-size: 2em;
        }

        .auth-container input {
            width: 100%;
            padding: 12px;
            margin: 10px 0;
            border: 2px solid #e0e0e0;
            border-radius: 10px;
            outline: none;
            font-size: 16px;
            transition: all 0.3s ease;
        }

        .auth-container input:focus {
            border-color: #667eea;
            box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.1);
        }

        .auth-btn {
            width: 100%;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 15px 40px;
            border: none;
            border-radius: 50px;
            font-size: 18px;
            font-weight: 600;
            cursor: pointer;
            margin-top: 20px;
            transition: all 0.3s ease;
        }

        .auth-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 30px rgba(102, 126, 234, 0.4);
        }

        .extra-links {
            margin-top: 15px;
            font-size: 14px;
        }

        .extra-links a {
            text-decoration: none;
            color: #764ba2;
            cursor: pointer;
            transition: color 0.3s ease;
        }

        .extra-links a:hover {
            color: #667eea;
        }
        
        /* Hidden class for toggling forms */
        .hidden {
            display: none !important;
        }

        /* --- NutriPlan Main App Styles --- */
        .container {
            max-width: 1200px;
            width: 100%;
        }

        header {
            text-align: center;
            color: white;
            margin-bottom: 40px;
            animation: fadeInDown 0.8s ease;
        }

        header h1 {
            font-size: 3em;
            margin-bottom: 10px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
        }

        header p {
            font-size: 1.2em;
            opacity: 0.9;
        }

        .card {
            background: white;
            border-radius: 20px;
            padding: 40px;
            box-shadow: 0 20px 60px rgba(0,0,0,0.3);
            animation: fadeInUp 0.8s ease;
        }

        .form-section {
            margin-bottom: 30px;
        }

        .form-section h2 {
            color: #667eea;
            margin-bottom: 20px;
            font-size: 1.8em;
        }

        .form-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin-bottom: 20px;
        }

        .form-group {
            display: flex;
            flex-direction: column;
        }

        label {
            margin-bottom: 8px;
            color: #333;
            font-weight: 600;
        }

        input:not(.auth-container input), select { /* Targeting main app inputs */
            padding: 12px;
            border: 2px solid #e0e0e0;
            border-radius: 10px;
            font-size: 16px;
            transition: all 0.3s ease;
        }

        input:not(.auth-container input):focus, select:focus {
            outline: none;
            border-color: #667eea;
            box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.1);
        }

        .checkbox-group {
            display: flex;
            flex-wrap: wrap;
            gap: 15px;
            margin-top: 10px;
        }

        .checkbox-item {
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .checkbox-item input[type="checkbox"] {
            width: 20px;
            height: 20px;
            cursor: pointer;
        }

        .btn {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 15px 40px;
            border: none;
            border-radius: 50px;
            font-size: 18px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            display: block;
            width: 100%;
            margin-top: 20px;
        }

        .btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 30px rgba(102, 126, 234, 0.4);
        }

        .results {
            display: none;
            margin-top: 30px;
            padding: 30px;
            background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
            border-radius: 15px;
            animation: fadeIn 0.5s ease;
        }

        .results h3 {
            color: #667eea;
            margin-bottom: 20px;
            font-size: 1.5em;
        }

        .meal-plan {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 20px;
            margin-top: 20px;
        }

        .meal-card {
            background: white;
            padding: 20px;
            border-radius: 15px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
            transition: transform 0.3s ease;
        }

        .meal-card:hover {
            transform: translateY(-5px);
        }

        .meal-card h4 {
            color: #764ba2;
            margin-bottom: 15px;
            font-size: 1.3em;
        }

        .meal-card ul {
            list-style: none;
            padding-left: 0;
        }

        .meal-card li {
            padding: 8px 0;
            border-bottom: 1px solid #f0f0f0;
        }

        .meal-card li:last-child {
            border-bottom: none;
        }

        .nutrition-info {
            background: white;
            padding: 20px;
            border-radius: 15px;
            margin-top: 20px;
        }

        .nutrition-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
            gap: 15px;
            margin-top: 15px;
        }

        .nutrition-item {
            text-align: center;
            padding: 15px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border-radius: 10px;
        }

        .nutrition-item .value {
            font-size: 1.8em;
            font-weight: bold;
        }

        .nutrition-item .label {
            font-size: 0.9em;
            opacity: 0.9;
        }

        /* --- Animation Keyframes --- */
        @keyframes fadeInDown {
            from { opacity: 0; transform: translateY(-20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        @keyframes fadeInUp {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }
    </style>
</head>
<body>

    <div class="auth-container" id="authContainer">
        
        <div id="loginView">
            <h2>Login to NutriPlan</h2>
            <form id="loginForm">
                <input type="text" id="loginUsername" placeholder="Username" required>
                <input type="password" id="loginPassword" placeholder="Password" required>
                <button type="submit" class="auth-btn">Login</button>
            </form>
            <div class="extra-links">
                <p>Don’t have an account? <a id="showSignup">Sign Up</a></p>
                <p><a href="#">Forgot Password?</a></p>
            </div>
        </div>

        <div id="signupView" class="hidden">
            <h2>Create New Account</h2>
            <form id="signupForm">
                <input type="text" id="signupUsername" placeholder="Choose Username" required>
                <input type="email" id="signupEmail" placeholder="Email Address" required>
                <input type="password" id="signupPassword" placeholder="Password (min 6 chars)" minlength="6" required>
                <button type="submit" class="auth-btn">Register</button>
            </form>
            <div class="extra-links">
                <p>Already have an account? <a id="showLogin">Log In</a></p>
            </div>
        </div>
    </div>

    <div class="container hidden" id="appContainer">
        <header>
            <h1>🥗 NutriPlan</h1>
            <p>Personalized Diet Recommendations for Your Goals</p>
        </header>

        <div class="card">
            <form id="dietForm">
                <div class="form-section">
                    <h2>Personal Information</h2>
                    <div class="form-grid">
                        <div class="form-group">
                            <label for="age">Age</label>
                            <input type="number" id="age" min="1" max="120" required>
                        </div>
                        <div class="form-group">
                            <label for="gender">Gender</label>
                            <select id="gender" required>
                                <option value="">Select</option>
                                <option value="male">Male</option>
                                <option value="female">Female</option>
                                <option value="other">Other</option>
                            </select>
                        </div>
                        <div class="form-group">
                            <label for="weight">Weight (kg)</label>
                            <input type="number" id="weight" min="1" step="0.1" required>
                        </div>
                        <div class="form-group">
                            <label for="height">Height (cm)</label>
                            <input type="number" id="height" min="1" required>
                        </div>
                    </div>
                </div>

                <div class="form-section">
                    <h2>Activity & Goals</h2>
                    <div class="form-grid">
                        <div class="form-group">
                            <label for="activity">Activity Level</label>
                            <select id="activity" required>
                                <option value="">Select</option>
                                <option value="sedentary">Sedentary (little/no exercise)</option>
                                <option value="light">Light (1-3 days/week)</option>
                                <option value="moderate">Moderate (3-5 days/week)</option>
                                <option value="active">Active (6-7 days/week)</option>
                                <option value="very-active">Very Active (athlete)</option>
                            </select>
                        </div>
                        <div class="form-group">
                            <label for="goal">Goal</label>
                            <select id="goal" required>
                                <option value="">Select</option>
                                <option value="lose">Lose Weight</option>
                                <option value="maintain">Maintain Weight</option>
                                <option value="gain">Gain Weight/Muscle</option>
                            </select>
                        </div>
                    </div>
                </div>

                <div class="form-section">
                    <h2>Dietary Preferences</h2>
                    <div class="form-group">
                        <label for="diet-type">Diet Type</label>
                        <select id="diet-type">
                            <option value="balanced">Balanced</option>
                            <option value="vegetarian">Vegetarian</option>
                            <option value="vegan">Vegan</option>
                            <option value="keto">Keto</option>
                            <option value="paleo">Paleo</option>
                            <option value="mediterranean">Mediterranean</option>
                        </select>
                    </div>
                    <div class="form-group">
                        <label>Allergies/Restrictions</label>
                        <div class="checkbox-group">
                            <div class="checkbox-item">
                                <input type="checkbox" id="dairy" value="dairy">
                                <label for="dairy">Dairy</label>
                            </div>
                            <div class="checkbox-item">
                                <input type="checkbox" id="nuts" value="nuts">
                                <label for="nuts">Nuts</label>
                            </div>
                            <div class="checkbox-item">
                                <input type="checkbox" id="gluten" value="gluten">
                                <label for="gluten">Gluten</label>
                            </div>
                            <div class="checkbox-item">
                                <input type="checkbox" id="shellfish" value="shellfish">
                                <label for="shellfish">Shellfish</label>
                            </div>
                        </div>
                    </div>
                </div>

                <button type="submit" class="btn">Get My Diet Plan</button>
            </form>

            <div class="results" id="results">
                <h3>Your Personalized Diet Plan</h3>
                <div class="nutrition-info">
                    <h4 style="color: #667eea; margin-bottom: 15px;">Daily Nutritional Targets</h4>
                    <div class="nutrition-grid" id="nutritionGrid"></div>
                </div>
                <div class="meal-plan" id="mealPlan"></div>
            </div>
        </div>
    </div>

    <script>
        // Store registered users (for demo)
        const users = new Map();
        users.set('user', 'password123'); // Default demo user

        // --- AUTH TOGGLE LOGIC ---
        document.getElementById('showSignup').addEventListener('click', () => {
            document.getElementById('loginView').classList.add('hidden');
            document.getElementById('signupView').classList.remove('hidden');
        });

        document.getElementById('showLogin').addEventListener('click', () => {
            document.getElementById('signupView').classList.add('hidden');
            document.getElementById('loginView').classList.remove('hidden');
        });

        // --- SIGNUP LOGIC (FIXED) ---
        document.getElementById('signupForm').addEventListener('submit', function(e) {
            e.preventDefault();
            
            const username = document.getElementById('signupUsername').value;
            const password = document.getElementById('signupPassword').value;

            if (users.has(username)) {
                // FIX: Using backticks (template literals) for correct variable interpolation
                alert(`🚫 Registration Failed: Username "${username}" is already taken.`);
            } else {
                users.set(username, password);
                // FIX: Using backticks (template literals) for correct variable interpolation
                alert(`✅ Account Created Successfully! You can now log in as "${username}".`);
                
                // Switch back to login view after successful registration
                document.getElementById('signupView').classList.add('hidden');
                document.getElementById('loginView').classList.remove('hidden');
                document.getElementById('loginUsername').value = username; // Pre-fill username
                document.getElementById('loginPassword').value = '';
            }
        });

        // --- LOGIN LOGIC (FIXED ALERT) ---
        document.getElementById('loginForm').addEventListener('submit', function(e) {
            e.preventDefault();
            
            const username = document.getElementById('loginUsername').value;
            const password = document.getElementById('loginPassword').value;

            if (users.has(username) && users.get(username) === password) {
                // Successful login
                // FIX: Using backticks (template literals) for correct variable interpolation
                alert(`👋 Welcome back, ${username}!`);
                document.getElementById('authContainer').classList.add('hidden');
                document.getElementById('appContainer').classList.remove('hidden');
                
                // Adjust body for main app layout
                document.body.style.alignItems = 'flex-start'; 
                document.body.style.justifyContent = 'flex-start';

            } else {
                alert('❌ Login Failed: Invalid Username or Password.');
            }
        });

        // --- DIET PLAN DATA ---
        const dietPlans = {
            balanced: {
                breakfast: ['Oatmeal with berries and almonds', 'Whole grain toast with avocado'],
                lunch: ['Grilled chicken salad', 'Quinoa bowl with vegetables'],
                dinner: ['Baked fish with steamed vegetables', 'Lean beef stir-fry'],
                snacks: ['Apple with peanut butter', 'Mixed nuts']
            },
            vegetarian: {
                breakfast: ['Veggie omelet', 'Avocado toast'],
                lunch: ['Lentil soup', 'Bean burrito bowl'],
                dinner: ['Eggplant parmesan', 'Mushroom risotto'],
                snacks: ['Greek yogurt', 'Trail mix']
            },
            vegan: {
                breakfast: ['Chia pudding with fruits', 'Tofu scramble'],
                lunch: ['Buddha bowl with tahini', 'Lentil salad'],
                dinner: ['Black bean tacos', 'Vegetable pad thai'],
                snacks: ['Almonds', 'Fruit salad']
            },
            keto: {
                breakfast: ['Eggs and bacon', 'Avocado with eggs'],
                lunch: ['Cobb salad', 'Grilled chicken thighs'],
                dinner: ['Salmon with asparagus', 'Pork chops with cauliflower'],
                snacks: ['Cheese cubes', 'Hard boiled eggs']
            },
            paleo: {
                breakfast: ['Sweet potato hash', 'Eggs with vegetables'],
                lunch: ['Grilled chicken salad', 'Beef patty with salad'],
                dinner: ['Grilled fish with vegetables', 'Grass-fed steak'],
                snacks: ['Fresh berries', 'Almonds']
            },
            mediterranean: {
                breakfast: ['Greek yogurt with honey', 'Whole grain bread with olive oil'],
                lunch: ['Greek salad with feta', 'Grilled fish'],
                dinner: ['Baked salmon with herbs', 'Grilled vegetables'],
                snacks: ['Olives', 'Nuts']
            }
        };

        // --- DIET FORM LOGIC ---
        document.getElementById('dietForm').addEventListener('submit', function(e) {
            e.preventDefault();
            generatePlan();
        });

        function calculateBMR(age, weight, height, gender) {
            // Harris-Benedict Equation
            let bmr;
            if (gender === 'male') {
                // BMR = 88.362 + (13.397 * weight in kg) + (4.799 * height in cm) - (5.677 * age in years)
                bmr = 88.362 + (13.397 * weight) + (4.799 * height) - (5.677 * age);
            } else if (gender === 'female') {
                // BMR = 447.593 + (9.247 * weight in kg) + (3.098 * height in cm) - (4.330 * age in years)
                bmr = 447.593 + (9.247 * weight) + (3.098 * height) - (4.330 * age);
            } else {
                // Simple average for 'other'
                bmr = 66 + (13.7 * weight) + (5 * height) - (6.8 * age);
            }
            return bmr;
        }

        function calculateTDEE(bmr, activityLevel) {
            const activityFactors = {
                sedentary: 1.2,
                light: 1.375,
                moderate: 1.55,
                active: 1.725,
                'very-active': 1.9
            };
            return bmr * (activityFactors[activityLevel] || 1.2);
        }

        function calculateDailyCalories(tdee, goal) {
            switch (goal) {
                case 'lose':
                    return tdee - 500; // Calorie deficit
                case 'gain':
                    return tdee + 500; // Calorie surplus
                case 'maintain':
                default:
                    return tdee;
            }
        }

        function generatePlan() {
            const age = parseFloat(document.getElementById('age').value);
            const gender = document.getElementById('gender').value;
            const weight = parseFloat(document.getElementById('weight').value);
            const height = parseFloat(document.getElementById('height').value);
            const activity = document.getElementById('activity').value;
            const goal = document.getElementById('goal').value;
            const dietType = document.getElementById('diet-type').value;

            // Calculate BMR and TDEE
            const bmr = calculateBMR(age, weight, height, gender);
            const tdee = calculateTDEE(bmr, activity);
            const dailyCalories = calculateDailyCalories(tdee, goal);

            // Macro Split (Example: 40/30/30 for Balanced/Weight Loss)
            const proteinGrams = Math.round((dailyCalories * 0.30) / 4); // 30% calories from protein, 4 cal/gram
            const carbGrams = Math.round((dailyCalories * 0.40) / 4); // 40% calories from carbs, 4 cal/gram
            const fatGrams = Math.round((dailyCalories * 0.30) / 9); // 30% calories from fat, 9 cal/gram

            // Display Nutrition Info
            const nutritionGrid = document.getElementById('nutritionGrid');
            nutritionGrid.innerHTML = `
                <div class="nutrition-item"><div class="value">${Math.round(dailyCalories)}</div><div class="label">Daily Calories</div></div>
                <div class="nutrition-item"><div class="value">${proteinGrams}g</div><div class="label">Protein</div></div>
                <div class="nutrition-item"><div class="value">${carbGrams}g</div><div class="label">Carbohydrates</div></div>
                <div class="nutrition-item"><div class="value">${fatGrams}g</div><div class="label">Fats</div></div>
                <div class="nutrition-item"><div class="value">${Math.round(tdee)}</div><div class="label">TDEE (Maintenance)</div></div>
            `;
            
            // Generate Meal Plan
            const mealPlanContainer = document.getElementById('mealPlan');
            const selectedDiet = dietPlans[dietType] || dietPlans.balanced;
            
            // Helper function to get a random meal
            const getRandomMeal = (meals) => meals[Math.floor(Math.random() * meals.length)];

            mealPlanContainer.innerHTML = `
                <div class="meal-card">
                    <h4>☀️ Breakfast</h4>
                    <ul><li>${getRandomMeal(selectedDiet.breakfast)}</li></ul>
                </div>
                <div class="meal-card">
                    <h4>🍎 Snack (Mid-Morning)</h4>
                    <ul><li>${getRandomMeal(selectedDiet.snacks)}</li></ul>
                </div>
                <div class="meal-card">
                    <h4>🥪 Lunch</h4>
                    <ul><li>${getRandomMeal(selectedDiet.lunch)}</li></ul>
                </div>
                <div class="meal-card">
                    <h4>🥜 Snack (Afternoon)</h4>
                    <ul><li>${getRandomMeal(selectedDiet.snacks)}</li></ul>
                </div>
                <div class="meal-card">
                    <h4>🌙 Dinner</h4>
                    <ul><li>${getRandomMeal(selectedDiet.dinner)}</li></ul>
                </div>
                <div class="meal-card">
                    <h4>💧 Hydration Tip</h4>
                    <ul><li>Drink a minimum of 8 glasses (2 liters) of water daily!</li></ul>
                </div>
            `;

            // Show Results
            document.getElementById('results').style.display = 'block';
            
            // Optional: Scroll to results for better UX on mobile/smaller screens
            document.getElementById('results').scrollIntoView({ behavior: 'smooth' });
        }
    </script>
</body>
</html>
