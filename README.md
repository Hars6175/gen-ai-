<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sahara AI - Your Mental Wellness Companion</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        'brand-primary': '#4A90E2',
                        'brand-secondary': '#50E3C2',
                        'brand-dark': '#2C3E50',
                        'brand-light': '#ECF0F1',
                        'brand-accent': '#F5A623',
                    },
                    fontFamily: {
                        sans: ['Inter', 'sans-serif'],
                    },
                    animation: {
                        'fade-in': 'fadeIn 0.5s ease-in-out',
                        'slide-in-left': 'slideInLeft 0.5s ease-in-out',
                        'pulse-subtle': 'pulseSubtle 2s infinite',
                    },
                    keyframes: {
                        fadeIn: {
                            '0%': { opacity: 0 },
                            '100%': { opacity: 1 },
                        },
                        slideInLeft: {
                            '0%': { transform: 'translateX(-100%)', opacity: 0 },
                            '100%': { transform: 'translateX(0)', opacity: 1 },
                        },
                        pulseSubtle: {
                            '0%, 100%': { transform: 'scale(1)' },
                            '50%': { transform: 'scale(1.02)' },
                        }
                    }
                }
            }
        }
    </script>
    <link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap">
    <script src="https://unpkg.com/lucide@latest"></script>
    <style>
        /* Custom scrollbar for a cleaner look */
        ::-webkit-scrollbar { width: 8px; }
        ::-webkit-scrollbar-track { background: #f1f1f1; }
        ::-webkit-scrollbar-thumb { background: #4A90E2; border-radius: 10px; }
        ::-webkit-scrollbar-thumb:hover { background: #3a75c4; }
        .sidebar-icon {
            stroke-width: 1.5;
        }
    </style>
</head>
<body class="bg-brand-light font-sans antialiased">

    <!-- App Root Container -->
    <div id="app-root">

        <!-- Initial Loading Screen -->
        <div id="loading-screen" class="min-h-screen flex items-center justify-center bg-gray-100">
            <div class="flex flex-col items-center">
                <div class="animate-spin rounded-full h-12 w-12 border-b-2 border-brand-primary"></div>
                <p class="mt-4 text-gray-600">Initializing Sahara AI...</p>
            </div>
        </div>

        <!-- Auth Screen (Login/Signup) -->
        <div id="auth-screen" class="hidden min-h-screen flex items-center justify-center bg-gray-100 p-4 animate-fade-in">
            <div class="w-full max-w-md">
                <div class="bg-white shadow-2xl rounded-2xl p-8 space-y-6">
                    <div class="text-center">
                        <h1 class="text-3xl font-bold text-brand-dark">Welcome to Sahara AI</h1>
                        <p class="text-gray-500 mt-2">Your confidential mental wellness companion.</p>
                    </div>
                    
                    <!-- Auth Forms Container -->
                    <div id="auth-forms">
                        <!-- Login Form -->
                        <form id="login-form" class="space-y-4">
                            <h2 class="text-xl font-semibold text-center text-brand-dark">Log In</h2>
                            <div>
                                <label for="login-email" class="text-sm font-medium text-gray-700">Email</label>
                                <input id="login-email" type="email" required class="mt-1 block w-full px-3 py-2 bg-white border border-gray-300 rounded-md shadow-sm placeholder-gray-400 focus:outline-none focus:ring-brand-primary focus:border-brand-primary">
                            </div>
                            <div>
                                <label for="login-password" class="text-sm font-medium text-gray-700">Password</label>
                                <input id="login-password" type="password" required class="mt-1 block w-full px-3 py-2 bg-white border border-gray-300 rounded-md shadow-sm placeholder-gray-400 focus:outline-none focus:ring-brand-primary focus:border-brand-primary">
                            </div>
                            <button type="submit" class="w-full flex justify-center py-3 px-4 border border-transparent rounded-md shadow-sm text-sm font-medium text-white bg-brand-primary hover:bg-opacity-90 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-brand-primary transition-transform transform hover:scale-105">Log In</button>
                        </form>

                        <!-- Signup Form (hidden by default) -->
                        <form id="signup-form" class="hidden space-y-4">
                            <h2 class="text-xl font-semibold text-center text-brand-dark">Sign Up</h2>
                            <div>
                                <label for="signup-email" class="text-sm font-medium text-gray-700">Email</label>
                                <input id="signup-email" type="email" required class="mt-1 block w-full px-3 py-2 bg-white border border-gray-300 rounded-md shadow-sm placeholder-gray-400 focus:outline-none focus:ring-brand-primary focus:border-brand-primary">
                            </div>
                            <div>
                                <label for="signup-password" class="text-sm font-medium text-gray-700">Password</label>
                                <input id="signup-password" type="password" required minlength="6" class="mt-1 block w-full px-3 py-2 bg-white border border-gray-300 rounded-md shadow-sm placeholder-gray-400 focus:outline-none focus:ring-brand-primary focus:border-brand-primary">
                            </div>
                            <button type="submit" class="w-full flex justify-center py-3 px-4 border border-transparent rounded-md shadow-sm text-sm font-medium text-white bg-brand-primary hover:bg-opacity-90 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-brand-primary transition-transform transform hover:scale-105">Create Account</button>
                        </form>
                    </div>

                    <p id="auth-error" class="text-red-500 text-sm text-center"></p>

                    <div class="text-center">
                        <button id="toggle-auth" class="text-sm text-brand-primary hover:underline">Don't have an account? Sign Up</button>
                    </div>
                    <div class="relative flex py-3 items-center">
                        <div class="flex-grow border-t border-gray-300"></div>
                        <span class="flex-shrink mx-4 text-gray-400">Or</span>
                        <div class="flex-grow border-t border-gray-300"></div>
                    </div>
                    <button id="anonymous-login" class="w-full flex justify-center py-3 px-4 border border-gray-300 rounded-md shadow-sm text-sm font-medium text-brand-dark bg-white hover:bg-gray-50 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-brand-primary transition-transform transform hover:scale-105">Continue as Guest</button>
                </div>
            </div>
        </div>

        <!-- Main App Screen (hidden by default) -->
        <div id="main-app" class="hidden h-screen w-screen flex animate-fade-in">
            <!-- Sidebar Navigation -->
            <nav id="sidebar" class="bg-brand-dark text-white w-64 p-4 flex flex-col space-y-2 transform transition-transform duration-300 ease-in-out -translate-x-full md:translate-x-0 md:relative absolute z-30 h-full">
                <div class="flex items-center space-x-2 p-2 mb-4">
                    <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="text-brand-secondary"><path d="M12 2a10 10 0 1 0 10 10A10 10 0 0 0 12 2z"/><path d="M12 18a6 6 0 0 0 0-12v0a6 6 0 0 1 0 12z"/></svg>
                    <span class="text-xl font-bold">Sahara AI</span>
                </div>
                
                <a href="#" data-view="dashboard" class="nav-link bg-gray-700 flex items-center p-3 rounded-lg hover:bg-gray-700">
                    <i data-lucide="layout-dashboard" class="sidebar-icon mr-3"></i> Dashboard
                </a>
                <a href="#" data-view="chat" class="nav-link flex items-center p-3 rounded-lg hover:bg-gray-700">
                    <i data-lucide="message-circle" class="sidebar-icon mr-3"></i> AI Chat
                </a>
                <a href="#" data-view="journal" class="nav-link flex items-center p-3 rounded-lg hover:bg-gray-700">
                    <i data-lucide="book-open" class="sidebar-icon mr-3"></i> Journal
                </a>
                <a href="#" data-view="goals" class="nav-link flex items-center p-3 rounded-lg hover:bg-gray-700">
                    <i data-lucide="target" class="sidebar-icon mr-3"></i> Goals
                </a>
                <a href="#" data-view="exercises" class="nav-link flex items-center p-3 rounded-lg hover:bg-gray-700">
                    <i data-lucide="heart-pulse" class="sidebar-icon mr-3"></i> Exercises
                </a>
                <a href="#" data-view="resources" class="nav-link flex items-center p-3 rounded-lg hover:bg-gray-700">
                    <i data-lucide="folder-kanban" class="sidebar-icon mr-3"></i> Resources
                </a>

                <div class="flex-grow"></div>

                <div id="user-profile" class="p-2 border-t border-gray-700">
                    <p class="text-sm truncate" id="user-email-display">user@example.com</p>
                    <button id="logout-button" class="w-full mt-2 flex items-center justify-center p-2 rounded-lg text-sm text-red-400 hover:bg-red-500 hover:text-white">
                        <i data-lucide="log-out" class="sidebar-icon mr-2 h-4 w-4"></i> Logout
                    </button>
                </div>
            </nav>

            <!-- Main Content Area -->
            <main class="flex-1 flex flex-col bg-gray-100 overflow-y-auto">
                <!-- Header -->
                <header class="bg-white shadow-sm p-4 flex items-center justify-between z-10">
                    <div class="flex items-center">
                        <button id="menu-toggle" class="md:hidden text-brand-dark">
                            <i data-lucide="menu" class="h-6 w-6"></i>
                        </button>
                        <h1 id="view-title" class="text-2xl font-bold text-brand-dark ml-4 md:ml-0">Dashboard</h1>
                    </div>
                    <div id="header-actions"></div> <!-- Actions specific to view -->
                </header>

                <!-- Content Views -->
                <div id="content-views" class="flex-1 p-4 md:p-8">
                    <!-- Dashboard View -->
                    <div id="view-dashboard" class="view animate-fade-in">
                        <h2 class="text-3xl font-semibold text-gray-700 mb-2">Welcome back, <span id="username-display"></span>!</h2>
                        <p class="text-gray-500 mb-8">How are you feeling today?</p>
                        
                        <!-- Mood Tracker -->
                        <div class="bg-white p-6 rounded-2xl shadow-lg mb-8">
                            <h3 class="font-semibold text-lg mb-4 text-brand-dark">Track Your Mood</h3>
                            <div class="flex justify-around items-center flex-wrap">
                                <button class="mood-btn p-2" data-mood="Happy">
                                    <span class="text-5xl transition-transform transform hover:scale-125">😊</span>
                                    <p class="text-sm text-gray-600">Happy</p>
                                </button>
                                <button class="mood-btn p-2" data-mood="Calm">
                                    <span class="text-5xl transition-transform transform hover:scale-125">😌</span>
                                    <p class="text-sm text-gray-600">Calm</p>
                                </button>
                                <button class="mood-btn p-2" data-mood="Okay">
                                    <span class="text-5xl transition-transform transform hover:scale-125">😐</span>
                                    <p class="text-sm text-gray-600">Okay</p>
                                </button>
                                <button class="mood-btn p-2" data-mood="Sad">
                                    <span class="text-5xl transition-transform transform hover:scale-125">😔</span>
                                    <p class="text-sm text-gray-600">Sad</p>
                                </button>
                                <button class="mood-btn p-2" data-mood="Anxious">
                                    <span class="text-5xl transition-transform transform hover:scale-125">😟</span>
                                    <p class="text-sm text-gray-600">Anxious</p>
                                </button>
                            </div>
                        </div>

                        <!-- AI Mood Suggestion -->
                        <div id="mood-suggestion-container" class="hidden bg-white/50 border border-brand-primary/20 p-4 rounded-lg mb-8 animate-fade-in">
                            <p id="mood-suggestion-text" class="text-brand-dark"></p>
                        </div>


                        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
                            <!-- Quick Start Chat -->
                            <div class="bg-brand-primary text-white p-6 rounded-2xl shadow-lg flex flex-col justify-between animate-pulse-subtle cursor-pointer" onclick="navigateTo('chat')">
                                <i data-lucide="message-circle" class="h-10 w-10 mb-4 text-brand-secondary"></i>
                                <h3 class="font-bold text-xl">Talk to Sahara</h3>
                                <p class="opacity-80">Need to talk? Your AI companion is here to listen, 24/7.</p>
                            </div>
                            <!-- New Journal Entry -->
                            <div class="bg-white p-6 rounded-2xl shadow-lg cursor-pointer" id="new-journal-shortcut">
                                <i data-lucide="plus-circle" class="h-10 w-10 mb-4 text-brand-accent"></i>
                                <h3 class="font-bold text-xl text-brand-dark">New Journal Entry</h3>
                                <p class="text-gray-500">Reflect on your day and clear your mind.</p>
                            </div>
                            <!-- Suggested Exercise -->
                            <div class="bg-white p-6 rounded-2xl shadow-lg cursor-pointer" onclick="navigateTo('exercises')">
                                <i data-lucide="brain-circuit" class="h-10 w-10 mb-4 text-brand-secondary"></i>
                                <h3 class="font-bold text-xl text-brand-dark">Try a Breathing Exercise</h3>
                                <p class="text-gray-500">Find calm and focus with a guided session.</p>
                            </div>
                        </div>
                    </div>

                    <!-- AI Chat View -->
                    <div id="view-chat" class="view hidden animate-fade-in h-full flex flex-col">
                        <div id="chat-container" class="flex-1 bg-white rounded-2xl shadow-lg p-4 overflow-y-auto mb-4">
                            <!-- Messages will be injected here -->
                            <div class="text-center text-gray-500 p-8">
                                <p>This is a safe space. Feel free to share what's on your mind.</p>
                                <p class="text-xs mt-2">Sahara AI is not a therapist. In a crisis, please contact a professional.</p>
                            </div>
                        </div>
                        <div id="chat-loading" class="hidden flex items-center p-4">
                            <div class="animate-spin rounded-full h-5 w-5 border-b-2 border-brand-primary"></div>
                            <p class="ml-2 text-gray-600">Sahara AI is thinking...</p>
                        </div>
                        <form id="chat-form" class="flex items-center space-x-2">
                            <input id="chat-input" type="text" placeholder="Type your message..." autocomplete="off" class="flex-1 w-full px-4 py-3 bg-white border border-gray-300 rounded-full shadow-sm focus:outline-none focus:ring-2 focus:ring-brand-primary">
                            <button type="submit" class="bg-brand-primary text-white p-3 rounded-full hover:bg-opacity-90 transition-transform transform hover:scale-110">
                                <i data-lucide="send" class="h-6 w-6"></i>
                            </button>
                        </form>
                    </div>

                    <!-- Journal View -->
                    <div id="view-journal" class="view hidden animate-fade-in">
                        <button id="add-journal-btn" class="mb-6 inline-flex items-center px-4 py-2 bg-brand-primary text-white rounded-lg shadow hover:bg-opacity-90">
                            <i data-lucide="plus" class="h-5 w-5 mr-2"></i> New Entry
                        </button>
                        <div id="journal-list" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
                           <!-- Journal entries will be injected here -->
                           <div id="journal-placeholder" class="text-gray-500 col-span-full text-center p-8">Your journal is empty. Write your first entry to get started!</div>
                        </div>
                    </div>

                    <!-- Goals View -->
                    <div id="view-goals" class="view hidden animate-fade-in">
                        <form id="add-goal-form" class="mb-8 flex items-center space-x-2">
                             <input id="goal-input" type="text" placeholder="What's a wellness goal you have?" required class="flex-1 w-full px-4 py-3 bg-white border border-gray-300 rounded-lg shadow-sm focus:outline-none focus:ring-2 focus:ring-brand-primary">
                             <button type="submit" class="px-4 py-3 bg-brand-primary text-white rounded-lg shadow hover:bg-opacity-90">Add Goal</button>
                        </form>
                        <div id="goal-list" class="space-y-4">
                           <!-- Goals will be injected here -->
                           <p id="goal-placeholder" class="text-gray-500 text-center p-8">Set a goal to start your journey, like "practice mindfulness for 5 minutes daily".</p>
                        </div>
                    </div>

                    <!-- Exercises View -->
                    <div id="view-exercises" class="view hidden animate-fade-in">
                         <!-- AI Custom Exercise Generator -->
                        <div class="bg-white p-6 rounded-2xl shadow-lg mb-8">
                            <h3 class="font-semibold text-lg mb-2 text-brand-dark">✨ Create a Custom Exercise</h3>
                            <p class="text-gray-500 mb-4">Feeling a certain way? Describe it below to get a personalized mindfulness exercise.</p>
                            <form id="custom-exercise-form" class="flex items-center space-x-2">
                                <input id="custom-exercise-prompt" type="text" placeholder="e.g., I'm feeling stressed about an exam" required class="flex-1 w-full px-4 py-2 bg-white border border-gray-300 rounded-lg shadow-sm focus:outline-none focus:ring-2 focus:ring-brand-primary">
                                <button type="submit" class="px-4 py-2 bg-brand-accent text-white rounded-lg shadow hover:bg-opacity-90">Generate</button>
                            </form>
                            <div id="custom-exercise-result" class="mt-4 hidden p-4 bg-gray-50 rounded-lg"></div>
                        </div>

                        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
                           <!-- Exercise cards -->
                           <div class="exercise-card bg-white p-6 rounded-2xl shadow-lg cursor-pointer hover:shadow-xl transition-shadow" data-exercise="breathing">
                               <h3 class="font-bold text-xl text-brand-dark mb-2">Box Breathing</h3>
                               <p class="text-gray-500">A simple technique to calm your nervous system. Inhale 4s, hold 4s, exhale 4s, hold 4s.</p>
                           </div>
                           <div class="exercise-card bg-white p-6 rounded-2xl shadow-lg cursor-pointer hover:shadow-xl transition-shadow" data-exercise="mindfulness">
                               <h3 class="font-bold text-xl text-brand-dark mb-2">5-Sense Mindfulness</h3>
                               <p class="text-gray-500">Focus on your senses to ground yourself in the present moment. What do you see, hear, feel?</p>
                           </div>
                           <div class="exercise-card bg-white p-6 rounded-2xl shadow-lg cursor-pointer hover:shadow-xl transition-shadow" data-exercise="gratitude">
                               <h3 class="font-bold text-xl text-brand-dark mb-2">Gratitude Practice</h3>
                               <p class="text-gray-500">List three things you are grateful for today. Cultivate a positive mindset.</p>
                           </div>
                        </div>
                    </div>
                    
                    <!-- Resources View -->
                    <div id="view-resources" class="view hidden animate-fade-in">
                        <div class="space-y-6">
                            <div>
                                <h3 class="text-2xl font-semibold text-brand-dark mb-3">Understanding Anxiety</h3>
                                <ul class="list-disc list-inside space-y-2 text-gray-700">
                                    <li><a href="#" class="text-brand-primary hover:underline">Article: What is an Anxiety Attack?</a></li>
                                    <li><a href="#" class="text-brand-primary hover:underline">Video: Grounding Techniques for Anxiety</a></li>
                                </ul>
                            </div>
                            <div>
                                <h3 class="text-2xl font-semibold text-brand-dark mb-3">Managing Stress</h3>
                                <ul class="list-disc list-inside space-y-2 text-gray-700">
                                    <li><a href="#" class="text-brand-primary hover:underline">Article: Healthy Ways to Cope with Exam Stress</a></li>
                                    <li><a href="#" class="text-brand-primary hover:underline">Podcast: Mindfulness for Stress Reduction</a></li>
                                </ul>
                            </div>
                             <div>
                                <h3 class="text-2xl font-semibold text-brand-dark mb-3">Building Resilience</h3>
                                <ul class="list-disc list-inside space-y-2 text-gray-700">
                                    <li><a href="#" class="text-brand-primary hover:underline">Article: How to Build Your Mental Resilience</a></li>
                                </ul>
                            </div>
                        </div>
                    </div>

                </div>
            </main>
        </div>
    </div>

    <!-- Modal for Journal Entry / Exercise -->
    <div id="modal-container" class="hidden fixed inset-0 bg-black bg-opacity-50 z-50 flex items-center justify-center p-4">
        <div id="modal-content" class="bg-white rounded-2xl shadow-2xl p-8 w-full max-w-2xl max-h-[90vh] flex flex-col animate-fade-in">
            <!-- Modal content will be injected here -->
        </div>
    </div>
    
    <!-- Toast Notification -->
    <div id="toast" class="hidden fixed bottom-5 right-5 bg-brand-dark text-white py-2 px-5 rounded-lg shadow-xl animate-fade-in">
        <p id="toast-message"></p>
    </div>

    <!-- Firebase SDK -->
    <script type="module">
        // --- Firebase Imports ---
        import { initializeApp } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-app.js";
        import { 
            getAuth, 
            onAuthStateChanged,
            createUserWithEmailAndPassword,
            signInWithEmailAndPassword,
            signInAnonymously,
            signOut,
            signInWithCustomToken
        } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-auth.js";
        import { 
            getFirestore,
            collection,
            doc,
            addDoc,
            onSnapshot,
            query,
            deleteDoc,
            updateDoc,
            serverTimestamp,
            where
        } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-firestore.js";
        
        // --- App ID and Firebase Config ---
        const appId = typeof __app_id !== 'undefined' ? __app_id : 'sahara-ai-app';
        let firebaseConfig;
        try {
            firebaseConfig = typeof __firebase_config !== 'undefined' ? JSON.parse(__firebase_config) : {};
        } catch (e) {
            console.error("Firebase config is not valid JSON:", __firebase_config);
            firebaseConfig = {}; // Fallback
        }
        
        // --- Firebase Initialization ---
        let app, auth, db;
        try {
            app = initializeApp(firebaseConfig);
            auth = getAuth(app);
            db = getFirestore(app);
        } catch (e) {
            console.error("Error initializing Firebase:", e);
            document.body.innerHTML = '<div class="text-center p-8 text-red-600">Could not initialize the application. Firebase configuration is missing or invalid.</div>';
        }

        // --- App State ---
        let currentUser = null;
        let currentView = 'dashboard';
        let unsubscribeListeners = [];
        
        // --- DOM Elements ---
        const loadingScreen = document.getElementById('loading-screen');
        const authScreen = document.getElementById('auth-screen');
        const mainApp = document.getElementById('main-app');
        const loginForm = document.getElementById('login-form');
        const signupForm = document.getElementById('signup-form');
        const toggleAuthBtn = document.getElementById('toggle-auth');
        const anonymousLoginBtn = document.getElementById('anonymous-login');
        const logoutButton = document.getElementById('logout-button');
        const authError = document.getElementById('auth-error');
        const navLinks = document.querySelectorAll('.nav-link');
        const viewTitle = document.getElementById('view-title');
        const contentViews = document.querySelectorAll('.view');
        const menuToggle = document.getElementById('menu-toggle');
        const sidebar = document.getElementById('sidebar');
        const headerActions = document.getElementById('header-actions');

        const modalContainer = document.getElementById('modal-container');
        const modalContent = document.getElementById('modal-content');

        // --- UI Helper Functions ---
        const showToast = (message) => {
            const toast = document.getElementById('toast');
            const toastMessage = document.getElementById('toast-message');
            toastMessage.textContent = message;
            toast.classList.remove('hidden');
            setTimeout(() => {
                toast.classList.add('hidden');
            }, 3000);
        };

        function showConfirmationModal(title, message, onConfirm) {
            modalContent.innerHTML = `
                <h2 class="text-2xl font-bold text-brand-dark mb-4">${title}</h2>
                <p class="text-gray-600 mb-6">${message}</p>
                <div class="flex justify-end space-x-4">
                    <button id="confirm-cancel-btn" class="px-4 py-2 bg-gray-200 text-gray-800 rounded-lg hover:bg-gray-300">Cancel</button>
                    <button id="confirm-ok-btn" class="px-4 py-2 bg-red-500 text-white rounded-lg hover:bg-red-600">Confirm</button>
                </div>
            `;
            modalContainer.classList.remove('hidden');

            const cancelBtn = document.getElementById('confirm-cancel-btn');
            const okBtn = document.getElementById('confirm-ok-btn');

            const closeModal = () => {
                modalContainer.classList.add('hidden');
            };
            
            const handleConfirm = () => {
                onConfirm();
                closeModal();
            };

            cancelBtn.addEventListener('click', closeModal, { once: true });
            okBtn.addEventListener('click', handleConfirm, { once: true });
        }

        const navigateTo = (view) => {
            currentView = view;
            viewTitle.textContent = view.charAt(0).toUpperCase() + view.slice(1);
            contentViews.forEach(v => v.classList.add('hidden'));
            document.getElementById(`view-${view}`).classList.remove('hidden');

            navLinks.forEach(link => {
                link.classList.toggle('bg-gray-700', link.dataset.view === view);
            });
            
            // Handle header actions
            headerActions.innerHTML = '';
            if (view === 'chat') {
                 const summarizeBtn = document.createElement('button');
                 summarizeBtn.id = 'summarize-chat-btn';
                 summarizeBtn.className = 'hidden items-center px-3 py-1.5 bg-brand-accent text-white rounded-lg shadow hover:bg-opacity-90 text-sm';
                 summarizeBtn.innerHTML = 'Summarize ✨';
                 summarizeBtn.onclick = summarizeChat;
                 headerActions.appendChild(summarizeBtn);
            }

            if (sidebar.classList.contains('translate-x-0')) {
               sidebar.classList.remove('translate-x-0');
               sidebar.classList.add('-translate-x-full');
            }
        };

        // --- Auth Logic ---
        onAuthStateChanged(auth, async (user) => {
            loadingScreen.classList.add('hidden');
            if (user) {
                currentUser = user;
                authScreen.classList.add('hidden');
                mainApp.classList.remove('hidden');
                
                document.getElementById('user-email-display').textContent = user.isAnonymous ? 'Guest User' : user.email;
                document.getElementById('username-display').textContent = user.isAnonymous ? 'there' : user.email.split('@')[0];

                navigateTo('dashboard');
                setupFirestoreListeners();
            } else {
                currentUser = null;
                authScreen.classList.remove('hidden');
                mainApp.classList.add('hidden');
                
                unsubscribeListeners.forEach(unsub => unsub());
                unsubscribeListeners = [];
            }
        });

        loginForm.addEventListener('submit', (e) => { e.preventDefault(); signInWithEmailAndPassword(auth, loginForm['login-email'].value, loginForm['login-password'].value).catch(err => authError.textContent = err.message); });
        signupForm.addEventListener('submit', (e) => { e.preventDefault(); createUserWithEmailAndPassword(auth, signupForm['signup-email'].value, signupForm['signup-password'].value).catch(err => authError.textContent = err.message); });
        anonymousLoginBtn.addEventListener('click', () => { signInAnonymously(auth).catch(err => authError.textContent = err.message); });
        toggleAuthBtn.addEventListener('click', () => {
            loginForm.classList.toggle('hidden');
            signupForm.classList.toggle('hidden');
            toggleAuthBtn.textContent = loginForm.classList.contains('hidden') ? 'Already have an account? Log In' : "Don't have an account? Sign Up";
            authError.textContent = '';
        });
        logoutButton.addEventListener('click', () => signOut(auth));

        // --- Navigation ---
        navLinks.forEach(link => link.addEventListener('click', (e) => { e.preventDefault(); navigateTo(link.dataset.view); }));
        menuToggle.addEventListener('click', () => { sidebar.classList.toggle('-translate-x-full'); sidebar.classList.toggle('translate-x-0'); });

        // --- Firestore Listeners Setup ---
        function setupFirestoreListeners() {
            if (!currentUser) return;
            unsubscribeListeners.forEach(unsub => unsub()); // Clear old listeners
            unsubscribeListeners = [];
            
            const collectionsToListen = ['journalEntries', 'chatMessages', 'goals'];
            collectionsToListen.forEach(name => {
                const q = query(collection(db, 'artifacts', appId, 'users', currentUser.uid, name));
                const unsub = onSnapshot(q, (snapshot) => {
                    if (name === 'journalEntries') renderJournal(snapshot);
                    if (name === 'chatMessages') renderChat(snapshot);
                    if (name === 'goals') renderGoals(snapshot);
                }, (error) => console.error(`Error listening to ${name}:`, error));
                unsubscribeListeners.push(unsub);
            });
        }
        
        // --- Journal ---
        const addJournalBtn = document.getElementById('add-journal-btn');
        const newJournalShortcut = document.getElementById('new-journal-shortcut');
        addJournalBtn.addEventListener('click', () => showJournalModal());
        newJournalShortcut.addEventListener('click', () => showJournalModal());

        function renderJournal(snapshot) {
            const journalList = document.getElementById('journal-list');
            const placeholder = document.getElementById('journal-placeholder');
            journalList.innerHTML = '';
            journalList.appendChild(placeholder);
            if (snapshot.empty) {
                placeholder.style.display = 'block';
            } else {
                placeholder.style.display = 'none';
                snapshot.docs.sort((a,b) => b.data().createdAt - a.data().createdAt).forEach(doc => renderJournalCard(doc));
            }
        }

        function renderJournalCard(doc) {
            const data = doc.data();
            const card = document.createElement('div');
            card.className = 'bg-white p-6 rounded-2xl shadow-lg flex flex-col justify-between';
            card.innerHTML = `
                <div>
                    <h3 class="font-bold text-lg text-brand-dark truncate">${data.title}</h3>
                    <p class="text-sm text-gray-400 mb-3">${new Date(data.createdAt?.toDate()).toLocaleDateString()}</p>
                    <p class="text-gray-600 line-clamp-3">${data.content}</p>
                    ${data.insight ? `<p class="mt-4 pt-3 border-t text-sm text-brand-primary italic">✨ AI Insight: ${data.insight}</p>` : ''}
                </div>
                <div class="flex items-center justify-end space-x-2 mt-4">
                    <button class="p-2 text-gray-500 hover:text-brand-primary"><i data-lucide="edit" class="h-4 w-4"></i></button>
                    <button class="p-2 text-gray-500 hover:text-red-500"><i data-lucide="trash-2" class="h-4 w-4"></i></button>
                </div>
            `;
            card.querySelector('[data-lucide="edit"]').parentElement.addEventListener('click', () => showJournalModal(doc));
            card.querySelector('[data-lucide="trash-2"]').parentElement.addEventListener('click', () => {
                showConfirmationModal('Delete Entry', 'Are you sure you want to permanently delete this journal entry?', async () => {
                    await deleteDoc(doc.ref);
                    showToast("Entry deleted.");
                });
            });
            document.getElementById('journal-list').appendChild(card);
            lucide.createIcons();
        }

        async function showJournalModal(docToEdit = null) {
            const isEditing = !!docToEdit;
            const data = isEditing ? docToEdit.data() : { title: '', content: '' };
            modalContent.innerHTML = `
                <h2 class="text-2xl font-bold text-brand-dark mb-4">${isEditing ? 'Edit Entry' : 'New Journal Entry'}</h2>
                <form id="journal-form" class="flex-1 flex flex-col">
                    <input id="journal-title" type="text" placeholder="Title" value="${data.title}" required class="w-full px-3 py-2 mb-4 bg-white border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-brand-primary focus:border-brand-primary">
                    <textarea id="journal-content" placeholder="Write what's on your mind..." required class="flex-1 w-full px-3 py-2 bg-white border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-brand-primary focus:border-brand-primary resize-none">${data.content}</textarea>
                    <div class="flex justify-end space-x-4 mt-6">
                        <button type="button" id="cancel-modal-btn" class="px-4 py-2 bg-gray-200 text-gray-800 rounded-lg hover:bg-gray-300">Cancel</button>
                        <button type="submit" class="px-4 py-2 bg-brand-primary text-white rounded-lg hover:bg-opacity-90">Save Entry</button>
                    </div>
                </form>
            `;
            modalContainer.classList.remove('hidden');
            document.getElementById('cancel-modal-btn').addEventListener('click', () => modalContainer.classList.add('hidden'), { once: true });
            document.getElementById('journal-form').addEventListener('submit', async (e) => {
                e.preventDefault();
                const title = document.getElementById('journal-title').value;
                const content = document.getElementById('journal-content').value;
                if (isEditing) {
                    await updateDoc(docToEdit.ref, { title, content });
                    showToast('Entry updated!');
                } else {
                    const newEntryRef = await addDoc(collection(db, 'artifacts', appId, 'users', currentUser.uid, 'journalEntries'), { title, content, createdAt: serverTimestamp() });
                    showToast('Entry saved!');
                    const insight = await getAIInsight(content);
                    if(insight) await updateDoc(newEntryRef, { insight });
                }
                modalContainer.classList.add('hidden');
            });
        }
        
        // --- Gemini AI ---
        const API_KEY = ""; // Leave empty, Canvas will handle it
        const API_URL = `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-05-20:generateContent?key=${API_KEY}`;
        
        async function callGeminiAPI(systemPrompt, userPrompt, loadingElement = null) {
            if(loadingElement) loadingElement.style.display = 'block';
            try {
                const payload = {
                    contents: [{ parts: [{ text: userPrompt }] }],
                    systemInstruction: { parts: [{ text: systemPrompt }] },
                };
                const response = await fetch(API_URL, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify(payload)
                });
                if (!response.ok) throw new Error(`API Error: ${response.status}`);
                const result = await response.json();
                return result.candidates?.[0]?.content?.parts?.[0]?.text || "I'm not sure how to respond to that.";
            } catch (error) {
                console.error("Gemini API Error:", error);
                return "Sorry, an error occurred. Please try again.";
            } finally {
                if(loadingElement) loadingElement.style.display = 'none';
            }
        }
        
        async function getAIInsight(journalText) {
            const systemPrompt = "Analyze the following journal entry and provide a single, gentle, and encouraging sentence of insight. Focus on acknowledging feelings without being diagnostic.";
            return await callGeminiAPI(systemPrompt, journalText);
        }

        // --- AI Chat ---
        const chatForm = document.getElementById('chat-form');
        const chatInput = document.getElementById('chat-input');
        const chatContainer = document.getElementById('chat-container');
        let chatHistory = [];

        function renderChat(snapshot) {
            const chatContainer = document.getElementById('chat-container');
            chatContainer.innerHTML = `<div class="text-center text-gray-500 p-8"><p>This is a safe space. Feel free to share what's on your mind.</p><p class="text-xs mt-2">Sahara AI is not a therapist. In a crisis, please contact a professional.</p></div>`;
            chatHistory = [];
            snapshot.docs.sort((a, b) => a.data().timestamp - b.data().timestamp).forEach(doc => {
                const message = doc.data();
                renderChatMessage(message.role, message.text);
                chatHistory.push(`${message.role}: ${message.text}`);
            });
            chatContainer.scrollTop = chatContainer.scrollHeight;
            
            const summarizeBtn = document.getElementById('summarize-chat-btn');
            if(summarizeBtn) summarizeBtn.classList.toggle('hidden', chatHistory.length < 4);
        }

        function renderChatMessage(role, text) {
            const messageDiv = document.createElement('div');
            messageDiv.className = `flex mb-4 ${role === 'user' ? 'justify-end' : 'justify-start'}`;
            messageDiv.innerHTML = `<div class="max-w-xs md:max-w-md p-3 rounded-2xl ${role === 'user' ? 'bg-brand-primary text-white' : 'bg-gray-200 text-brand-dark'}"><p>${text}</p></div>`;
            const placeholder = chatContainer.querySelector('.text-center');
            if (placeholder) placeholder.remove();
            chatContainer.appendChild(messageDiv);
        }

        chatForm.addEventListener('submit', async (e) => {
            e.preventDefault();
            const userInput = chatInput.value.trim();
            if (!userInput || !currentUser) return;
            chatInput.value = '';
            
            await addDoc(collection(db, 'artifacts', appId, 'users', currentUser.uid, 'chatMessages'), { role: 'user', text: userInput, timestamp: serverTimestamp() });
            const chatLoading = document.getElementById('chat-loading');
            chatLoading.classList.remove('hidden');

            const systemPrompt = "You are Sahara, an empathetic AI mental wellness companion for Indian youth. Be warm, supportive, and use simple language. If you detect a crisis (suicide, self-harm), you MUST immediately provide the AASRA helpline number (+91-9820466726) and advise seeking professional help.";
            const aiResponse = await callGeminiAPI(systemPrompt, userInput);
            
            await addDoc(collection(db, 'artifacts', appId, 'users', currentUser.uid, 'chatMessages'), { role: 'model', text: aiResponse, timestamp: serverTimestamp() });
            chatLoading.classList.add('hidden');
        });
        
        async function summarizeChat() {
            if (chatHistory.length < 2) {
                showToast("Not enough conversation to summarize.");
                return;
            }
            const fullChat = chatHistory.join('\n');
            const systemPrompt = "You are a helpful assistant. Summarize the key themes and feelings from the following conversation in 2-3 brief bullet points.";
            const summary = await callGeminiAPI(systemPrompt, fullChat);
            modalContent.innerHTML = `
                <h2 class="text-2xl font-bold text-brand-dark mb-4">Conversation Summary</h2>
                <div class="text-gray-700 whitespace-pre-wrap">${summary}</div>
                <div class="flex justify-end mt-6"><button id="close-modal-btn" class="px-4 py-2 bg-gray-200 rounded-lg">Close</button></div>
            `;
            modalContainer.classList.remove('hidden');
            document.getElementById('close-modal-btn').addEventListener('click', () => modalContainer.classList.add('hidden'), {once: true});
        }
        
        // --- Goals ---
        const addGoalForm = document.getElementById('add-goal-form');
        const goalInput = document.getElementById('goal-input');

        addGoalForm.addEventListener('submit', async (e) => {
            e.preventDefault();
            const goalText = goalInput.value.trim();
            if(!goalText) return;
            await addDoc(collection(db, 'artifacts', appId, 'users', currentUser.uid, 'goals'), { text: goalText, completed: false, createdAt: serverTimestamp() });
            goalInput.value = '';
            showToast('Goal added!');
        });

        function renderGoals(snapshot) {
            const goalList = document.getElementById('goal-list');
            const placeholder = document.getElementById('goal-placeholder');
            goalList.innerHTML = '';
            goalList.appendChild(placeholder);
            if (snapshot.empty) {
                placeholder.style.display = 'block';
            } else {
                placeholder.style.display = 'none';
                snapshot.docs.sort((a,b) => a.data().completed - b.data().completed || a.data().createdAt - b.data().createdAt).forEach(doc => {
                    const goal = doc.data();
                    const goalEl = document.createElement('div');
                    goalEl.className = 'bg-white p-4 rounded-lg shadow-sm flex items-center justify-between';
                    goalEl.innerHTML = `
                        <div class="flex items-center">
                            <input type="checkbox" class="h-5 w-5 rounded text-brand-primary focus:ring-brand-primary" ${goal.completed ? 'checked' : ''}>
                            <p class="ml-4 ${goal.completed ? 'line-through text-gray-400' : 'text-brand-dark'}">${goal.text}</p>
                        </div>
                        <div class="flex items-center space-x-2">
                           <button class="breakdown-goal-btn px-2 py-1 bg-brand-accent/20 text-brand-accent text-xs rounded-md hover:bg-brand-accent/30">Break Down Goal ✨</button>
                           <button class="delete-goal-btn p-2 text-gray-400 hover:text-red-500"><i data-lucide="trash-2" class="h-4 w-4"></i></button>
                        </div>
                    `;
                    goalEl.querySelector('input[type="checkbox"]').addEventListener('change', (e) => updateDoc(doc.ref, { completed: e.target.checked }));
                    goalEl.querySelector('.delete-goal-btn').addEventListener('click', () => deleteDoc(doc.ref));
                    goalEl.querySelector('.breakdown-goal-btn').addEventListener('click', () => breakDownGoal(goal.text));
                    goalList.appendChild(goalEl);
                });
                lucide.createIcons();
            }
        }
        
        async function breakDownGoal(goalText) {
            const systemPrompt = "You are a supportive coach. A user wants to achieve a wellness goal. Break down the following goal into 3-4 small, actionable, and encouraging steps. Present it as a numbered list.";
            const steps = await callGeminiAPI(systemPrompt, `My goal is: "${goalText}"`);
             modalContent.innerHTML = `
                <h2 class="text-2xl font-bold text-brand-dark mb-4">Steps for: ${goalText}</h2>
                <div class="text-gray-700 whitespace-pre-wrap">${steps}</div>
                <div class="flex justify-end mt-6"><button id="close-modal-btn" class="px-4 py-2 bg-gray-200 rounded-lg">Close</button></div>
            `;
            modalContainer.classList.remove('hidden');
            document.getElementById('close-modal-btn').addEventListener('click', () => modalContainer.classList.add('hidden'), {once: true});
        }

        // --- Dashboard & Exercises ---
        document.querySelectorAll('.mood-btn').forEach(btn => {
            btn.addEventListener('click', async () => {
                const mood = btn.dataset.mood;
                showToast(`Mood logged: ${mood}`);
                const systemPrompt = "A user just logged their mood. Provide a single, short, empathetic sentence of encouragement or a gentle suggestion based on their mood.";
                const suggestion = await callGeminiAPI(systemPrompt, `The user is feeling: ${mood}`);
                const container = document.getElementById('mood-suggestion-container');
                document.getElementById('mood-suggestion-text').textContent = suggestion;
                container.classList.remove('hidden');
            });
        });
        
        document.getElementById('custom-exercise-form').addEventListener('submit', async (e) => {
            e.preventDefault();
            const prompt = document.getElementById('custom-exercise-prompt').value;
            const resultContainer = document.getElementById('custom-exercise-result');
            const systemPrompt = "You create short, guided mindfulness/meditation scripts (2-3 paragraphs). Based on the user's situation, generate a calming and supportive script. Format it with paragraphs.";
            const exerciseScript = await callGeminiAPI(systemPrompt, prompt, resultContainer);
            resultContainer.innerText = exerciseScript;
            resultContainer.classList.remove('hidden');
        });

        document.querySelectorAll('.exercise-card').forEach(card => card.addEventListener('click', () => { /* ... existing logic ... */ }));
        function showExerciseModal(title, content, type) { /* ... existing logic ... */ }
        function startBreathingAnimation() { /* ... existing logic ... */ }
        
        // --- Initial Sign-In ---
        async function initialSignIn() {
            try {
                if (typeof __initial_auth_token !== 'undefined' && __initial_auth_token) {
                    await signInWithCustomToken(auth, __initial_auth_token);
                } else {
                   // No token, wait for user action on the auth screen.
                   loadingScreen.classList.add('hidden');
                   authScreen.classList.remove('hidden');
                }
            } catch (error) {
                console.error("Error during initial sign-in:", error);
                loadingScreen.classList.add('hidden');
                authScreen.classList.remove('hidden');
                authError.textContent = "Automatic sign-in failed. Please log in manually.";
            }
        }

        // --- Final Setup ---
        window.navigateTo = navigateTo;
        lucide.createIcons();
        initialSignIn();

    </script>
</body>
</html>


