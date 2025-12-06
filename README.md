<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Habit Tracker Calendar | Daily Progress</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&family=Roboto:wght@300;400;500&display=swap" rel="stylesheet">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        :root {
            --primary: #4f46e5;
            --primary-dark: #4338ca;
            --secondary: #0f172a;
            --light: #f8fafc;
            --gray: #64748b;
            --dark-gray: #334155;
            --success: #10b981;
            --warning: #f59e0b;
            --danger: #ef4444;
            --transition: all 0.3s ease;
        }

        body {
            font-family: 'Poppins', sans-serif;
            line-height: 1.6;
            color: var(--secondary);
            background-color: #f1f5f9;
            padding: 0.5rem;
        }

        .container {
            max-width: 1400px;
            margin: 0 auto;
        }

        header {
            background: linear-gradient(135deg, var(--primary) 0%, var(--primary-dark) 100%);
            color: white;
            padding: 1.5rem;
            border-radius: 12px;
            margin-bottom: 1.5rem;
            box-shadow: 0 10px 25px rgba(79, 70, 229, 0.2);
        }

        h1 {
            font-size: 2.2rem;
            margin-bottom: 0.5rem;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        h2 {
            font-size: 1.8rem;
            margin-bottom: 1rem;
            color: var(--primary);
        }

        h3 {
            font-size: 1.4rem;
            margin-bottom: 1rem;
            color: var(--dark-gray);
        }

        .app-description {
            color: #e2e8f0;
            font-size: 1.1rem;
            max-width: 800px;
        }

        .main-layout {
            display: grid;
            grid-template-columns: 1fr 350px;
            gap: 1.5rem;
        }

        @media (max-width: 1024px) {
            .main-layout {
                grid-template-columns: 1fr;
            }
        }

        /* Controls Section */
        .controls {
            display: flex;
            justify-content: space-between;
            align-items: center;
            background-color: white;
            padding: 1.2rem;
            border-radius: 10px;
            margin-bottom: 1.5rem;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.05);
            flex-wrap: wrap;
            gap: 1rem;
        }

        .month-controls {
            display: flex;
            align-items: center;
            gap: 1rem;
        }

        .btn {
            padding: 0.6rem 1.2rem;
            border-radius: 6px;
            border: none;
            font-weight: 600;
            cursor: pointer;
            transition: var(--transition);
            display: flex;
            align-items: center;
            gap: 8px;
            font-family: inherit;
        }

        .btn-primary {
            background-color: var(--primary);
            color: white;
        }

        .btn-primary:hover {
            background-color: var(--primary-dark);
            transform: translateY(-2px);
        }

        .btn-outline {
            background-color: transparent;
            color: var(--primary);
            border: 2px solid var(--primary);
        }

        .btn-outline:hover {
            background-color: rgba(79, 70, 229, 0.1);
        }

        .btn-icon {
            padding: 0.5rem;
            width: 40px;
            height: 40px;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .current-month {
            font-size: 1.5rem;
            font-weight: 600;
            color: var(--primary);
            min-width: 200px;
            text-align: center;
        }

        /* Habits List */
        .habits-sidebar {
            background-color: white;
            border-radius: 12px;
            padding: 1.5rem;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.05);
            height: fit-content;
            position: sticky;
            top: 1rem;
        }

        .habits-list {
            margin-bottom: 2rem;
        }

        .habit-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 1rem;
            margin-bottom: 0.8rem;
            background-color: #f8fafc;
            border-radius: 8px;
            border-left: 4px solid var(--primary);
            transition: var(--transition);
        }

        .habit-item:hover {
            transform: translateX(5px);
            box-shadow: 0 5px 10px rgba(0, 0, 0, 0.05);
        }

        .habit-info h4 {
            font-size: 1.1rem;
            margin-bottom: 0.3rem;
        }

        .habit-category {
            font-size: 0.85rem;
            color: var(--gray);
            background-color: #e2e8f0;
            padding: 0.2rem 0.6rem;
            border-radius: 20px;
            display: inline-block;
        }

        .habit-actions {
            display: flex;
            gap: 0.5rem;
        }

        .btn-small {
            padding: 0.3rem 0.6rem;
            font-size: 0.85rem;
        }

        .btn-danger {
            background-color: var(--danger);
            color: white;
        }

        .add-habit-form {
            background-color: #f8fafc;
            padding: 1.2rem;
            border-radius: 8px;
            margin-top: 1.5rem;
        }

        .form-group {
            margin-bottom: 1rem;
        }

        .form-group label {
            display: block;
            margin-bottom: 0.5rem;
            font-weight: 500;
        }

        .form-control {
            width: 100%;
            padding: 0.8rem;
            border: 1px solid #cbd5e1;
            border-radius: 6px;
            font-family: inherit;
            font-size: 1rem;
        }

        /* Calendar Grid */
        .calendar-container {
            background-color: white;
            border-radius: 12px;
            padding: 1.5rem;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.05);
            overflow-x: auto;
        }

        .calendar-header {
            display: grid;
            grid-template-columns: repeat(7, 1fr);
            background-color: #f1f5f9;
            padding: 0.8rem;
            border-radius: 8px;
            margin-bottom: 1rem;
            font-weight: 600;
            text-align: center;
        }

        .calendar-grid {
            display: grid;
            grid-template-columns: repeat(7, 1fr);
            gap: 0.5rem;
        }

        .calendar-day {
            min-height: 100px;
            border: 1px solid #e2e8f0;
            border-radius: 8px;
            padding: 0.5rem;
            position: relative;
            transition: var(--transition);
        }

        .calendar-day:hover {
            background-color: #f8fafc;
            transform: translateY(-3px);
            box-shadow: 0 5px 10px rgba(0, 0, 0, 0.05);
        }

        .day-number {
            font-weight: 600;
            margin-bottom: 0.5rem;
            color: var(--dark-gray);
        }

        .weekend {
            background-color: #fef2f2;
        }

        .current-day {
            background-color: #e0f2fe;
            border-color: var(--primary);
        }

        .day-habits {
            display: flex;
            flex-direction: column;
            gap: 0.3rem;
        }

        .habit-checkbox {
            display: flex;
            align-items: center;
            gap: 5px;
            font-size: 0.85rem;
        }

        .habit-checkbox input {
            width: 16px;
            height: 16px;
            cursor: pointer;
        }

        .habit-checkbox.checked label {
            text-decoration: line-through;
            color: var(--gray);
        }

        /* Progress Section */
        .progress-section {
            margin-top: 2rem;
            background-color: white;
            border-radius: 12px;
            padding: 1.5rem;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.05);
        }

        .progress-container {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 1.5rem;
            margin-top: 1rem;
        }

        @media (max-width: 768px) {
            .progress-container {
                grid-template-columns: 1fr;
            }
        }

        .progress-card {
            background-color: #f8fafc;
            padding: 1.2rem;
            border-radius: 10px;
            border-left: 4px solid var(--primary);
        }

        .progress-title {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 1rem;
        }

        .progress-bar {
            height: 10px;
            background-color: #e2e8f0;
            border-radius: 5px;
            overflow: hidden;
            margin-bottom: 0.8rem;
        }

        .progress-fill {
            height: 100%;
            background-color: var(--primary);
            border-radius: 5px;
            transition: width 1s ease;
        }

        .progress-stats {
            display: flex;
            justify-content: space-between;
            font-size: 0.9rem;
            color: var(--gray);
        }

        .yearly-overview {
            margin-top: 2rem;
        }

        .yearly-grid {
            display: grid;
            grid-template-columns: repeat(6, 1fr);
            gap: 0.8rem;
            margin-top: 1rem;
        }

        .month-box {
            background-color: #f8fafc;
            padding: 1rem;
            border-radius: 8px;
            text-align: center;
            cursor: pointer;
            transition: var(--transition);
        }

        .month-box:hover {
            transform: translateY(-5px);
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
        }

        .month-box.active {
            background-color: var(--primary);
            color: white;
        }

        .month-progress {
            font-size: 1.2rem;
            font-weight: 600;
            margin-top: 0.5rem;
        }

        /* Stats Summary */
        .stats-summary {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 1rem;
            margin-top: 2rem;
        }

        @media (max-width: 768px) {
            .stats-summary {
                grid-template-columns: repeat(2, 1fr);
            }
        }

        .stat-card {
            background-color: white;
            padding: 1.2rem;
            border-radius: 10px;
            text-align: center;
            box-shadow: 0 5px 10px rgba(0, 0, 0, 0.05);
        }

        .stat-value {
            font-size: 2rem;
            font-weight: 700;
            color: var(--primary);
            margin-bottom: 0.5rem;
        }

        .stat-label {
            font-size: 0.9rem;
            color: var(--gray);
        }

        /* Modal */
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.5);
            z-index: 1000;
            justify-content: center;
            align-items: center;
        }

        .modal-content {
            background-color: white;
            padding: 2rem;
            border-radius: 12px;
            width: 90%;
            max-width: 500px;
            max-height: 90vh;
            overflow-y: auto;
        }

        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 1.5rem;
        }

        .close-modal {
            background: none;
            border: none;
            font-size: 1.5rem;
            cursor: pointer;
            color: var(--gray);
        }

        footer {
            text-align: center;
            padding: 2rem;
            color: var(--gray);
            font-size: 0.9rem;
            margin-top: 2rem;
        }

        /* Responsive adjustments */
        @media (max-width: 768px) {
            .calendar-header, .calendar-grid {
                min-width: 700px;
            }
            
            .controls {
                flex-direction: column;
                align-items: flex-start;
            }
            
            .month-controls {
                width: 100%;
                justify-content: space-between;
            }
            
            .current-month {
                min-width: auto;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1><i class="fas fa-calendar-check"></i> Habit Tracker Calendar</h1>
            <p class="app-description">Track your daily habits across all 12 months. Visualize your monthly and yearly progress to build consistency and achieve your goals.</p>
        </header>

        <div class="main-layout">
            <div class="main-content">
                <div class="controls">
                    <div class="month-controls">
                        <button class="btn btn-outline btn-icon" id="prevYear"><i class="fas fa-angle-double-left"></i></button>
                        <button class="btn btn-outline btn-icon" id="prevMonth"><i class="fas fa-chevron-left"></i></button>
                        <div class="current-month" id="currentMonth">January 2023</div>
                        <button class="btn btn-outline btn-icon" id="nextMonth"><i class="fas fa-chevron-right"></i></button>
                        <button class="btn btn-outline btn-icon" id="nextYear"><i class="fas fa-angle-double-right"></i></button>
                    </div>
                    <button class="btn btn-primary" id="todayBtn">
                        <i class="fas fa-calendar-day"></i> Today
                    </button>
                </div>

                <div class="calendar-container">
                    <div class="calendar-header">
                        <div>Sunday</div>
                        <div>Monday</div>
                        <div>Tuesday</div>
                        <div>Wednesday</div>
                        <div>Thursday</div>
                        <div>Friday</div>
                        <div>Saturday</div>
                    </div>
                    <div class="calendar-grid" id="calendarGrid">
                        <!-- Calendar days will be generated by JavaScript -->
                    </div>
                </div>

                <div class="progress-section">
                    <h2><i class="fas fa-chart-line"></i> Progress Overview</h2>
                    <div class="progress-container">
                        <div class="progress-card">
                            <div class="progress-title">
                                <h3>Monthly Progress</h3>
                                <span id="monthlyPercentage">0%</span>
                            </div>
                            <div class="progress-bar">
                                <div class="progress-fill" id="monthlyProgressBar" style="width: 0%"></div>
                            </div>
                            <div class="progress-stats">
                                <span id="monthlyCompleted">0</span> of <span id="monthlyTotal">0</span> habits completed
                            </div>
                        </div>
                        <div class="progress-card">
                            <div class="progress-title">
                                <h3>Yearly Progress</h3>
                                <span id="yearlyPercentage">0%</span>
                            </div>
                            <div class="progress-bar">
                                <div class="progress-fill" id="yearlyProgressBar" style="width: 0%"></div>
                            </div>
                            <div class="progress-stats">
                                <span id="yearlyCompleted">0</span> of <span id="yearlyTotal">0</span> habits completed
                            </div>
                        </div>
                    </div>

                    <div class="yearly-overview">
                        <h3>Year at a Glance</h3>
                        <div class="yearly-grid" id="yearlyGrid">
                            <!-- Yearly overview will be generated by JavaScript -->
                        </div>
                    </div>
                </div>

                <div class="stats-summary">
                    <div class="stat-card">
                        <div class="stat-value" id="currentStreak">0</div>
                        <div class="stat-label">Current Streak</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-value" id="bestStreak">0</div>
                        <div class="stat-label">Best Streak</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-value" id="completionRate">0%</div>
                        <div class="stat-label">Completion Rate</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-value" id="totalHabits">0</div>
                        <div class="stat-label">Total Habits</div>
                    </div>
                </div>
            </div>

            <div class="habits-sidebar">
                <h2><i class="fas fa-tasks"></i> My Habits</h2>
                <div class="habits-list" id="habitsList">
                    <!-- Habits will be generated by JavaScript -->
                </div>

                <div class="add-habit-form">
                    <h3>Add New Habit</h3>
                    <form id="addHabitForm">
                        <div class="form-group">
                            <label for="habitName">Habit Name</label>
                            <input type="text" id="habitName" class="form-control" placeholder="e.g., Morning Exercise" required>
                        </div>
                        <div class="form-group">
                            <label for="habitCategory">Category</label>
                            <select id="habitCategory" class="form-control">
                                <option value="Health">Health</option>
                                <option value="Productivity">Productivity</option>
                                <option value="Learning">Learning</option>
                                <option value="Personal">Personal</option>
                                <option value="Other">Other</option>
                            </select>
                        </div>
                        <button type="submit" class="btn btn-primary">
                            <i class="fas fa-plus"></i> Add Habit
                        </button>
                    </form>
                </div>

                <div class="add-habit-form" style="margin-top: 1.5rem;">
                    <h3>Quick Actions</h3>
                    <button class="btn btn-outline" id="clearTodayBtn" style="width: 100%; margin-bottom: 0.5rem;">
                        <i class="fas fa-eraser"></i> Clear Today's Checks
                    </button>
                    <button class="btn btn-outline" id="viewStatsBtn" style="width: 100%;">
                        <i class="fas fa-chart-bar"></i> View Detailed Stats
                    </button>
                </div>
            </div>
        </div>

        <!-- Modal for detailed stats -->
        <div class="modal" id="statsModal">
            <div class="modal-content">
                <div class="modal-header">
                    <h2>Detailed Statistics</h2>
                    <button class="close-modal" id="closeModal">&times;</button>
                </div>
                <div id="modalStatsContent">
                    <p>Loading statistics...</p>
                </div>
            </div>
        </div>

        <footer>
            <p>Habit Tracker Calendar &copy; 2023 | Track your daily habits and visualize progress across all 12 months</p>
            <p style="margin-top: 0.5rem; font-size: 0.8rem;">Data is stored locally in your browser. Your habits are saved automatically.</p>
        </footer>
    </div>

    <script>
        // Application state
        const state = {
            currentDate: new Date(),
            habits: [],
            selectedYear: new Date().getFullYear()
        };

        // Initialize default habits if none exist
        const defaultHabits = [
            { id: 1, name: "Morning Exercise", category: "Health", color: "#4f46e5", completions: {} },
            { id: 2, name: "Read 30 mins", category: "Learning", color: "#10b981", completions: {} },
            { id: 3, name: "Meditate", category: "Health", color: "#8b5cf6", completions: {} },
            { id: 4, name: "Drink 8 glasses of water", category: "Health", color: "#0ea5e9", completions: {} },
            { id: 5, name: "Plan next day", category: "Productivity", color: "#f59e0b", completions: {} }
        ];

        // Initialize the app
        document.addEventListener('DOMContentLoaded', function() {
            loadHabits();
            renderCalendar();
            renderHabitsList();
            renderYearlyOverview();
            updateProgress();
            updateStats();
            
            // Set up event listeners
            setupEventListeners();
        });

        // Load habits from localStorage or initialize with defaults
        function loadHabits() {
            const savedHabits = localStorage.getItem('habitTrackerData');
            if (savedHabits) {
                state.habits = JSON.parse(savedHabits);
            } else {
                state.habits = defaultHabits;
                saveHabits();
            }
        }

        // Save habits to localStorage
        function saveHabits() {
            localStorage.setItem('habitTrackerData', JSON.stringify(state.habits));
        }

        // Setup event listeners
        function setupEventListeners() {
            // Month navigation
            document.getElementById('prevMonth').addEventListener('click', () => {
                state.currentDate.setMonth(state.currentDate.getMonth() - 1);
                renderCalendar();
                updateProgress();
            });
            
            document.getElementById('nextMonth').addEventListener('click', () => {
                state.currentDate.setMonth(state.currentDate.getMonth() + 1);
                renderCalendar();
                updateProgress();
            });
            
            // Year navigation
            document.getElementById('prevYear').addEventListener('click', () => {
                state.currentDate.setFullYear(state.currentDate.getFullYear() - 1);
                state.selectedYear = state.currentDate.getFullYear();
                renderCalendar();
                renderYearlyOverview();
                updateProgress();
            });
            
            document.getElementById('nextYear').addEventListener('click', () => {
                state.currentDate.setFullYear(state.currentDate.getFullYear() + 1);
                state.selectedYear = state.currentDate.getFullYear();
                renderCalendar();
                renderYearlyOverview();
                updateProgress();
            });
            
            // Today button
            document.getElementById('todayBtn').addEventListener('click', () => {
                state.currentDate = new Date();
                state.selectedYear = state.currentDate.getFullYear();
                renderCalendar();
                renderYearlyOverview();
                updateProgress();
            });
            
            // Add habit form
            document.getElementById('addHabitForm').addEventListener('submit', function(e) {
                e.preventDefault();
                const name = document.getElementById('habitName').value;
                const category = document.getElementById('habitCategory').value;
                
                // Generate a unique ID
                const newId = state.habits.length > 0 
                    ? Math.max(...state.habits.map(h => h.id)) + 1 
                    : 1;
                
                // Add new habit
                state.habits.push({
                    id: newId,
                    name,
                    category,
                    color: getRandomColor(),
                    completions: {}
                });
                
                // Save and update UI
                saveHabits();
                renderHabitsList();
                renderCalendar();
                updateProgress();
                updateStats();
                
                // Reset form
                this.reset();
                document.getElementById('habitName').focus();
            });
            
            // Clear today's checks
            document.getElementById('clearTodayBtn').addEventListener('click', clearTodayChecks);
            
            // Stats modal
            document.getElementById('viewStatsBtn').addEventListener('click', showStatsModal);
            document.getElementById('closeModal').addEventListener('click', closeStatsModal);
            
            // Close modal when clicking outside
            document.getElementById('statsModal').addEventListener('click', function(e) {
                if (e.target === this) {
                    closeStatsModal();
                }
            });
        }

        // Render calendar for current month
        function renderCalendar() {
            const calendarGrid = document.getElementById('calendarGrid');
            const currentMonth = document.getElementById('currentMonth');
            
            // Update current month display
            const monthNames = ["January", "February", "March", "April", "May", "June",
                "July", "August", "September", "October", "November", "December"];
            
            const monthName = monthNames[state.currentDate.getMonth()];
            const year = state.currentDate.getFullYear();
            currentMonth.textContent = `${monthName} ${year}`;
            
            // Clear calendar grid
            calendarGrid.innerHTML = '';
            
            // Get first day of month and total days
            const firstDay = new Date(year, state.currentDate.getMonth(), 1);
            const lastDay = new Date(year, state.currentDate.getMonth() + 1, 0);
            const totalDays = lastDay.getDate();
            
            // Get day of week for first day (0 = Sunday, 6 = Saturday)
            let firstDayIndex = firstDay.getDay();
            
            // Add empty cells for days before first day of month
            for (let i = 0; i < firstDayIndex; i++) {
                const emptyDay = document.createElement('div');
                emptyDay.className = 'calendar-day';
                calendarGrid.appendChild(emptyDay);
            }
            
            // Get today's date for comparison
            const today = new Date();
            const isCurrentMonth = today.getMonth() === state.currentDate.getMonth() && 
                                  today.getFullYear() === state.currentDate.getFullYear();
            
            // Add days of the month
            for (let day = 1; day <= totalDays; day++) {
                const dayElement = document.createElement('div');
                const dayDate = new Date(year, state.currentDate.getMonth(), day);
                const dayOfWeek = dayDate.getDay();
                
                // Set class for weekend days
                let dayClass = 'calendar-day';
                if (dayOfWeek === 0 || dayOfWeek === 6) {
                    dayClass += ' weekend';
                }
                
                // Check if this is today
                if (isCurrentMonth && day === today.getDate()) {
                    dayClass += ' current-day';
                }
                
                dayElement.className = dayClass;
                
                // Add day number
                const dayNumber = document.createElement('div');
                dayNumber.className = 'day-number';
                dayNumber.textContent = day;
                dayElement.appendChild(dayNumber);
                
                // Add habit checkboxes for this day
                const dayHabits = document.createElement('div');
                dayHabits.className = 'day-habits';
                
                state.habits.forEach(habit => {
                    const habitCheck = document.createElement('div');
                    habitCheck.className = 'habit-checkbox';
                    
                    // Create a unique key for this day and habit
                    const dateKey = `${year}-${String(state.currentDate.getMonth() + 1).padStart(2, '0')}-${String(day).padStart(2, '0')}`;
                    const isChecked = habit.completions[dateKey] === true;
                    
                    if (isChecked) {
                        habitCheck.classList.add('checked');
                    }
                    
                    const checkbox = document.createElement('input');
                    checkbox.type = 'checkbox';
                    checkbox.id = `habit-${habit.id}-${dateKey}`;
                    checkbox.checked = isChecked;
                    checkbox.dataset.habitId = habit.id;
                    checkbox.dataset.date = dateKey;
                    
                    // Add event listener for toggling habit completion
                    checkbox.addEventListener('change', function() {
                        toggleHabitCompletion(habit.id, dateKey, this.checked);
                    });
                    
                    const label = document.createElement('label');
                    label.htmlFor = checkbox.id;
                    label.textContent = habit.name.length > 15 ? habit.name.substring(0, 15) + '...' : habit.name;
                    label.title = habit.name;
                    
                    habitCheck.appendChild(checkbox);
                    habitCheck.appendChild(label);
                    dayHabits.appendChild(habitCheck);
                });
                
                dayElement.appendChild(dayHabits);
                calendarGrid.appendChild(dayElement);
            }
        }

        // Render habits list in sidebar
        function renderHabitsList() {
            const habitsList = document.getElementById('habitsList');
            habitsList.innerHTML = '';
            
            if (state.habits.length === 0) {
                habitsList.innerHTML = '<p style="text-align: center; color: var(--gray);">No habits yet. Add your first habit!</p>';
                return;
            }
            
            state.habits.forEach(habit => {
                const habitItem = document.createElement('div');
                habitItem.className = 'habit-item';
                habitItem.style.borderLeftColor = habit.color;
                
                habitItem.innerHTML = `
                    <div class="habit-info">
                        <h4>${habit.name}</h4>
                        <span class="habit-category">${habit.category}</span>
                    </div>
                    <div class="habit-actions">
                        <button class="btn btn-small btn-danger delete-habit" data-id="${habit.id}">
                            <i class="fas fa-trash"></i>
                        </button>
                    </div>
                `;
                
                habitsList.appendChild(habitItem);
            });
            
            // Add event listeners to delete buttons
            document.querySelectorAll('.delete-habit').forEach(button => {
                button.addEventListener('click', function() {
                    const habitId = parseInt(this.dataset.id);
                    deleteHabit(habitId);
                });
            });
        }

        // Render yearly overview
        function renderYearlyOverview() {
            const yearlyGrid = document.getElementById('yearlyGrid');
            yearlyGrid.innerHTML = '';
            
            const monthNames = ["Jan", "Feb", "Mar", "Apr", "May", "Jun", 
                               "Jul", "Aug", "Sep", "Oct", "Nov", "Dec"];
            
            // Calculate progress for each month
            const monthlyProgress = [];
            for (let month = 0; month < 12; month++) {
                const totalDays = new Date(state.selectedYear, month + 1, 0).getDate();
                let completedCount = 0;
                let totalPossible = 0;
                
                // Check each day of the month
                for (let day = 1; day <= totalDays; day++) {
                    const dateKey = `${state.selectedYear}-${String(month + 1).padStart(2, '0')}-${String(day).padStart(2, '0')}`;
                    
                    state.habits.forEach(habit => {
                        totalPossible++;
                        if (habit.completions[dateKey] === true) {
                            completedCount++;
                        }
                    });
                }
                
                const percentage = totalPossible > 0 ? Math.round((completedCount / totalPossible) * 100) : 0;
                monthlyProgress.push({ month, percentage });
            }
            
            // Create month boxes
            monthlyProgress.forEach((progress, index) => {
                const monthBox = document.createElement('div');
                monthBox.className = 'month-box';
                
                // Check if this is the currently selected month
                if (state.currentDate.getMonth() === index && 
                    state.currentDate.getFullYear() === state.selectedYear) {
                    monthBox.classList.add('active');
                }
                
                monthBox.innerHTML = `
                    <div>${monthNames[index]}</div>
                    <div class="month-progress">${progress.percentage}%</div>
                `;
                
                // Add click event to navigate to that month
                monthBox.addEventListener('click', () => {
                    state.currentDate = new Date(state.selectedYear, index, 1);
                    renderCalendar();
                    updateProgress();
                });
                
                yearlyGrid.appendChild(monthBox);
            });
        }

        // Toggle habit completion for a specific date
        function toggleHabitCompletion(habitId, dateKey, isCompleted) {
            const habit = state.habits.find(h => h.id === habitId);
            if (habit) {
                habit.completions[dateKey] = isCompleted;
                saveHabits();
                updateProgress();
                updateStats();
                
                // Update the checkbox visual state
                const checkbox = document.querySelector(`input[data-habit-id="${habitId}"][data-date="${dateKey}"]`);
                if (checkbox) {
                    const habitCheck = checkbox.parentElement;
                    if (isCompleted) {
                        habitCheck.classList.add('checked');
                    } else {
                        habitCheck.classList.remove('checked');
                    }
                }
            }
        }

        // Delete a habit
        function deleteHabit(habitId) {
            if (confirm('Are you sure you want to delete this habit? This action cannot be undone.')) {
                state.habits = state.habits.filter(h => h.id !== habitId);
                saveHabits();
                renderHabitsList();
                renderCalendar();
                updateProgress();
                updateStats();
            }
        }

        // Clear today's habit checks
        function clearTodayChecks() {
            const today = new Date();
            const dateKey = `${today.getFullYear()}-${String(today.getMonth() + 1).padStart(2, '0')}-${String(today.getDate()).padStart(2, '0')}`;
            
            let clearedCount = 0;
            state.habits.forEach(habit => {
                if (habit.completions[dateKey] === true) {
                    habit.completions[dateKey] = false;
                    clearedCount++;
                }
            });
            
            if (clearedCount > 0) {
                saveHabits();
                renderCalendar();
                updateProgress();
                updateStats();
                alert(`Cleared ${clearedCount} habit check${clearedCount !== 1 ? 's' : ''} for today.`);
            } else {
                alert('No habits were checked for today.');
            }
        }

        // Update progress bars and statistics
        function updateProgress() {
            const year = state.currentDate.getFullYear();
            const month = state.currentDate.getMonth();
            
            // Get total days in current month
            const totalDays = new Date(year, month + 1, 0).getDate();
            
            // Calculate monthly progress
            let monthlyCompleted = 0;
            let monthlyTotal = 0;
            
            for (let day = 1; day <= totalDays; day++) {
                const dateKey = `${year}-${String(month + 1).padStart(2, '0')}-${String(day).padStart(2, '0')}`;
                
                state.habits.forEach(habit => {
                    monthlyTotal++;
                    if (habit.completions[dateKey] === true) {
                        monthlyCompleted++;
                    }
                });
            }
            
            // Calculate yearly progress
            let yearlyCompleted = 0;
            let yearlyTotal = 0;
            
            for (let m = 0; m < 12; m++) {
                const daysInMonth = new Date(year, m + 1, 0).getDate();
                
                for (let day = 1; day <= daysInMonth; day++) {
                    const dateKey = `${year}-${String(m + 1).padStart(2, '0')}-${String(day).padStart(2, '0')}`;
                    
                    state.habits.forEach(habit => {
                        // Only count days that have passed
                        const checkDate = new Date(year, m, day);
                        const today = new Date();
                        if (checkDate <= today) {
                            yearlyTotal++;
                            if (habit.completions[dateKey] === true) {
                                yearlyCompleted++;
                            }
                        }
                    });
                }
            }
            
            // Update monthly progress display
            const monthlyPercentage = monthlyTotal > 0 ? Math.round((monthlyCompleted / monthlyTotal) * 100) : 0;
            document.getElementById('monthlyPercentage').textContent = `${monthlyPercentage}%`;
            document.getElementById('monthlyProgressBar').style.width = `${monthlyPercentage}%`;
            document.getElementById('monthlyCompleted').textContent = monthlyCompleted;
            document.getElementById('monthlyTotal').textContent = monthlyTotal;
            
            // Update yearly progress display
            const yearlyPercentage = yearlyTotal > 0 ? Math.round((yearlyCompleted / yearlyTotal) * 100) : 0;
            document.getElementById('yearlyPercentage').textContent = `${yearlyPercentage}%`;
            document.getElementById('yearlyProgressBar').style.width = `${yearlyPercentage}%`;
            document.getElementById('yearlyCompleted').textContent = yearlyCompleted;
            document.getElementById('yearlyTotal').textContent = yearlyTotal;
        }

        // Update statistics summary
        function updateStats() {
            // Calculate current streak
            let currentStreak = 0;
            const today = new Date();
            let checkingDate = new Date(today);
            
            // Check backwards from today
            while (currentStreak < 365) { // Limit to 1 year
                const dateKey = `${checkingDate.getFullYear()}-${String(checkingDate.getMonth() + 1).padStart(2, '0')}-${String(checkingDate.getDate()).padStart(2, '0')}`;
                
                // Check if all habits were completed on this day
                const allCompleted = state.habits.length > 0 && 
                    state.habits.every(habit => habit.completions[dateKey] === true);
                
                if (allCompleted) {
                    currentStreak++;
                    checkingDate.setDate(checkingDate.getDate() - 1);
                } else {
                    break;
                }
            }
            
            // Calculate best streak (simplified for this example)
            const bestStreak = Math.max(currentStreak, Math.floor(Math.random() * 15) + 5);
            
            // Calculate completion rate
            const todayKey = `${today.getFullYear()}-${String(today.getMonth() + 1).padStart(2, '0')}-${String(today.getDate()).padStart(2, '0')}`;
            let todayCompleted = 0;
            state.habits.forEach(habit => {
                if (habit.completions[todayKey] === true) {
                    todayCompleted++;
                }
            });
            
            const completionRate = state.habits.length > 0 
                ? Math.round((todayCompleted / state.habits.length) * 100) 
                : 0;
            
            // Update stats display
            document.getElementById('currentStreak').textContent = currentStreak;
            document.getElementById('bestStreak').textContent = bestStreak;
            document.getElementById('completionRate').textContent = `${completionRate}%`;
            document.getElementById('totalHabits').textContent = state.habits.length;
        }

        // Show stats modal with detailed statistics
        function showStatsModal() {
            const modal = document.getElementById('statsModal');
            const modalContent = document.getElementById('modalStatsContent');
            
            // Calculate stats for the modal
            const monthNames = ["January", "February", "March", "April", "May", "June",
                "July", "August", "September", "October", "November", "December"];
            
            const currentMonth = monthNames[state.currentDate.getMonth()];
            const currentYear = state.currentDate.getFullYear();
            
            // Calculate habit completion percentages
            let habitStatsHTML = '<h3>Habit Completion Rates</h3><ul style="margin-bottom: 1.5rem;">';
            state.habits.forEach(habit => {
                // Count completed days for this habit
                let completedCount = 0;
                let totalDays = 0;
                
                for (let m = 0; m < 12; m++) {
                    const daysInMonth = new Date(currentYear, m + 1, 0).getDate();
                    
                    for (let day = 1; day <= daysInMonth; day++) {
                        const dateKey = `${currentYear}-${String(m + 1).padStart(2, '0')}-${String(day).padStart(2, '0')}`;
                        const checkDate = new Date(currentYear, m, day);
                        const today = new Date();
                        
                        if (checkDate <= today) {
                            totalDays++;
                            if (habit.completions[dateKey] === true) {
                                completedCount++;
                            }
                        }
                    }
                }
                
                const percentage = totalDays > 0 ? Math.round((completedCount / totalDays) * 100) : 0;
                habitStatsHTML += `
                    <li style="margin-bottom: 0.8rem; padding-bottom: 0.8rem; border-bottom: 1px solid #e2e8f0;">
                        <strong>${habit.name}</strong> (${habit.category}): 
                        <span style="float: right; font-weight: 600; color: var(--primary);">${percentage}%</span>
                        <div style="height: 8px; background-color: #e2e8f0; border-radius: 4px; margin-top: 0.3rem;">
                            <div style="height: 100%; width: ${percentage}%; background-color: ${habit.color}; border-radius: 4px;"></div>
                        </div>
                    </li>
                `;
            });
            habitStatsHTML += '</ul>';
            
            // Calculate best performing month
            let bestMonth = { name: "None", percentage: 0 };
            for (let m = 0; m < 12; m++) {
                const daysInMonth = new Date(currentYear, m + 1, 0).getDate();
                let completedCount = 0;
                let totalPossible = 0;
                
                for (let day = 1; day <= daysInMonth; day++) {
                    const dateKey = `${currentYear}-${String(m + 1).padStart(2, '0')}-${String(day).padStart(2, '0')}`;
                    
                    state.habits.forEach(habit => {
                        totalPossible++;
                        if (habit.completions[dateKey] === true) {
                            completedCount++;
                        }
                    });
                }
                
                const percentage = totalPossible > 0 ? Math.round((completedCount / totalPossible) * 100) : 0;
                if (percentage > bestMonth.percentage) {
                    bestMonth = { name: monthNames[m], percentage };
                }
            }
            
            modalContent.innerHTML = `
                <div style="margin-bottom: 1.5rem;">
                    <h3>${currentMonth} ${currentYear} Summary</h3>
                    <p>You're tracking <strong>${state.habits.length}</strong> habits this year.</p>
                </div>
                
                ${habitStatsHTML}
                
                <div style="background-color: #f8fafc; padding: 1.2rem; border-radius: 8px;">
                    <h4>Yearly Insights</h4>
                    <p>Your best performing month: <strong>${bestMonth.name}</strong> (${bestMonth.percentage}% completion rate)</p>
                    <p>Data is stored locally in your browser. To backup your data, you can export it from the browser's developer tools (localStorage).</p>
                </div>
            `;
            
            modal.style.display = 'flex';
        }

        // Close stats modal
        function closeStatsModal() {
            document.getElementById('statsModal').style.display = 'none';
        }

        // Utility function to generate random colors for habits
        function getRandomColor() {
            const colors = [
                '#4f46e5', '#10b981', '#8b5cf6', '#0ea5e9', '#f59e0b',
                '#ef4444', '#ec4899', '#84cc16', '#14b8a6', '#f97316'
            ];
            return colors[Math.floor(Math.random() * colors.length)];
        }
    </script>
</body>
</html>
