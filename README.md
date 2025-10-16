# code-project
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CleanIndia - QR Waste Reporting System</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap');
        body { font-family: 'Inter', sans-serif; }
        
        .gradient-bg {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
        }
        
        .card-shadow {
            box-shadow: 0 10px 25px rgba(0,0,0,0.1);
        }
        
        .pulse-animation {
            animation: pulse 2s infinite;
        }
        
        @keyframes pulse {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.7; }
        }
        
        .success-animation {
            animation: successPulse 0.6s ease-out;
        }
        
        @keyframes successPulse {
            0% { transform: scale(0.8); opacity: 0; }
            100% { transform: scale(1); opacity: 1; }
        }
    </style>
</head>
<body class="bg-gray-50 min-h-screen">
    <!-- Header -->
    <div class="gradient-bg text-white p-4 text-center">
        <h1 class="text-2xl font-bold">🇮🇳 CleanIndia</h1>
        <p class="text-sm opacity-90 mt-1">QR Waste Reporting System</p>
    </div>

    <!-- Main Container -->
    <div class="max-w-md mx-auto bg-white min-h-screen">
        <!-- Welcome Screen -->
        <div id="welcomeScreen" class="p-6 text-center">
            <div class="mb-6">
                <div class="w-20 h-20 mx-auto bg-green-100 rounded-full flex items-center justify-center mb-4">
                    <span class="text-3xl">🗑️</span>
                </div>
                <h2 class="text-xl font-semibold text-gray-800 mb-2">Report Waste Dumps</h2>
                <p class="text-gray-600 text-sm">Help keep India clean by reporting waste dumps in your area</p>
            </div>

            <!-- QR Code Simulation -->
            <div class="bg-gray-100 p-6 rounded-lg mb-6">
                <div class="w-32 h-32 mx-auto bg-white border-2 border-gray-300 rounded-lg flex items-center justify-center mb-3">
                    <svg class="w-24 h-24" viewBox="0 0 100 100" fill="none">
                        <!-- QR Code Pattern -->
                        <rect x="10" y="10" width="15" height="15" fill="black"/>
                        <rect x="30" y="10" width="5" height="5" fill="black"/>
                        <rect x="40" y="10" width="5" height="5" fill="black"/>
                        <rect x="50" y="10" width="15" height="15" fill="black"/>
                        <rect x="75" y="10" width="15" height="15" fill="black"/>
                        
                        <rect x="10" y="30" width="5" height="5" fill="black"/>
                        <rect x="20" y="30" width="5" height="5" fill="black"/>
                        <rect x="35" y="30" width="10" height="5" fill="black"/>
                        <rect x="50" y="30" width="5" height="5" fill="black"/>
                        <rect x="75" y="30" width="5" height="5" fill="black"/>
                        <rect x="85" y="30" width="5" height="5" fill="black"/>
                        
                        <rect x="10" y="40" width="5" height="5" fill="black"/>
                        <rect x="25" y="40" width="10" height="5" fill="black"/>
                        <rect x="45" y="40" width="10" height="5" fill="black"/>
                        <rect x="65" y="40" width="5" height="5" fill="black"/>
                        <rect x="75" y="40" width="5" height="5" fill="black"/>
                        
                        <rect x="10" y="50" width="15" height="15" fill="black"/>
                        <rect x="30" y="50" width="5" height="5" fill="black"/>
                        <rect x="40" y="50" width="10" height="5" fill="black"/>
                        <rect x="55" y="50" width="5" height="5" fill="black"/>
                        <rect x="75" y="50" width="15" height="15" fill="black"/>
                        
                        <rect x="10" y="75" width="15" height="15" fill="black"/>
                        <rect x="35" y="75" width="5" height="5" fill="black"/>
                        <rect x="50" y="75" width="10" height="5" fill="black"/>
                        <rect x="75" y="75" width="15" height="15" fill="black"/>
                    </svg>
                </div>
                <p class="text-xs text-gray-500">Scan this QR code to report waste</p>
            </div>

            <button onclick="startReporting()" class="w-full bg-blue-600 text-white py-3 px-6 rounded-lg font-medium hover:bg-blue-700 transition-colors pulse-animation">
                📱 Scan QR Code
            </button>
            
            <div class="mt-4 text-xs text-gray-500">
                <p>Location: Near Arunachala College of Engineering</p>
                <p>QR ID: #QR001-ACE</p>
            </div>
        </div>

        <!-- Camera Screen -->
        <div id="cameraScreen" class="hidden p-4">
            <div class="mb-4">
                <button onclick="goBack()" class="text-blue-600 text-sm">← Back</button>
                <h3 class="text-lg font-semibold text-center">Take Photo of Waste</h3>
            </div>

            <!-- Camera Viewfinder -->
            <div class="relative bg-gray-900 rounded-lg overflow-hidden mb-4" style="aspect-ratio: 4/3;">
                <div class="absolute inset-0 bg-gradient-to-br from-gray-700 to-gray-900 flex items-center justify-center">
                    <div class="text-center text-white">
                        <div class="text-4xl mb-2">📷</div>
                        <p class="text-sm opacity-75">Camera View</p>
                        <p class="text-xs opacity-50 mt-1">Point camera at waste dump</p>
                    </div>
                </div>
                
                <!-- Camera overlay -->
                <div class="absolute inset-4 border-2 border-white border-dashed rounded-lg opacity-50"></div>
                
                <!-- Focus indicator -->
                <div class="absolute top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2 w-16 h-16 border-2 border-yellow-400 rounded-lg pulse-animation"></div>
            </div>

            <div class="flex justify-center space-x-4">
                <button onclick="capturePhoto()" class="bg-red-500 text-white w-16 h-16 rounded-full flex items-center justify-center text-2xl hover:bg-red-600 transition-colors">
                    📸
                </button>
            </div>
        </div>

        <!-- Photo Review Screen -->
        <div id="reviewScreen" class="hidden p-4">
            <div class="mb-4">
                <button onclick="retakePhoto()" class="text-blue-600 text-sm">← Retake</button>
                <h3 class="text-lg font-semibold text-center">Review Photo</h3>
            </div>

            <!-- Photo Preview -->
            <div class="bg-gray-200 rounded-lg mb-4 overflow-hidden" style="aspect-ratio: 4/3;">
                <div class="w-full h-full bg-gradient-to-br from-orange-200 to-brown-300 flex items-center justify-center relative">
                    <div class="text-center">
                        <div class="text-3xl mb-2">🗑️</div>
                        <p class="text-sm text-gray-700">Waste dump captured</p>
                    </div>
                    <!-- Simulated waste elements -->
                    <div class="absolute bottom-4 left-4 w-8 h-6 bg-gray-600 rounded-sm"></div>
                    <div class="absolute bottom-6 right-6 w-6 h-4 bg-green-600 rounded-sm"></div>
                    <div class="absolute top-8 right-8 w-4 h-8 bg-blue-400 rounded-sm"></div>
                </div>
            </div>

            <!-- Location Info -->
            <div class="bg-blue-50 p-3 rounded-lg mb-4">
                <div class="flex items-center text-sm text-blue-800">
                    <span class="mr-2">📍</span>
                    <span>Near Arunachala College of Engineering for Women</span>
                </div>
                <div class="text-xs text-blue-600 mt-1">Coordinates: 12.9716° N, 77.5946° E</div>
            </div>

            <!-- Additional Details -->
            <div class="mb-4">
                <label class="block text-sm font-medium text-gray-700 mb-2">Additional Details (Optional)</label>
                <textarea id="additionalDetails" class="w-full p-3 border border-gray-300 rounded-lg text-sm" rows="3" placeholder="Describe the waste type, size, or any other relevant information..."></textarea>
            </div>

            <button onclick="submitReport()" class="w-full bg-green-600 text-white py-3 px-6 rounded-lg font-medium hover:bg-green-700 transition-colors">
                ✅ Submit Report
            </button>
        </div>

        <!-- Success Screen -->
        <div id="successScreen" class="hidden p-6 text-center">
            <div class="success-animation">
                <div class="w-20 h-20 mx-auto bg-green-100 rounded-full flex items-center justify-center mb-4">
                    <span class="text-3xl">✅</span>
                </div>
                <h2 class="text-xl font-semibold text-gray-800 mb-2">Report Submitted!</h2>
                <p class="text-gray-600 text-sm mb-6">Thank you for helping keep India clean</p>
            </div>

            <!-- Reward Card -->
            <div class="bg-gradient-to-r from-purple-500 to-pink-500 text-white p-4 rounded-lg card-shadow mb-6">
                <div class="flex items-center justify-between mb-2">
                    <span class="text-sm font-medium">CleanIndia Reward</span>
                    <span class="text-xs opacity-75">#REW001</span>
                </div>
                <div class="text-2xl font-bold mb-1">₹50 Coupon</div>
                <div class="text-xs opacity-90">Valid at partner stores</div>
                <div class="mt-3 text-xs">
                    <div class="flex justify-between">
                        <span>Expires:</span>
                        <span>30 days from now</span>
                    </div>
                </div>
            </div>

            <!-- Status Update -->
            <div class="bg-yellow-50 border border-yellow-200 p-3 rounded-lg mb-4">
                <div class="flex items-center text-sm text-yellow-800">
                    <span class="mr-2">🚛</span>
                    <span>Cleaning crew has been notified</span>
                </div>
                <div class="text-xs text-yellow-600 mt-1">Expected cleanup time: 2-4 hours</div>
            </div>

            <!-- Action Buttons -->
            <div class="space-y-3">
                <button onclick="trackProgress()" class="w-full bg-blue-600 text-white py-2 px-4 rounded-lg text-sm hover:bg-blue-700 transition-colors">
                    📊 Track Cleanup Progress
                </button>
                <button onclick="reportAnother()" class="w-full bg-gray-200 text-gray-800 py-2 px-4 rounded-lg text-sm hover:bg-gray-300 transition-colors">
                    📱 Report Another Waste Dump
                </button>
            </div>

            <!-- Stats -->
            <div class="mt-6 grid grid-cols-3 gap-4 text-center">
                <div class="bg-white p-3 rounded-lg card-shadow">
                    <div class="text-lg font-bold text-green-600">12</div>
                    <div class="text-xs text-gray-500">Reports Made</div>
                </div>
                <div class="bg-white p-3 rounded-lg card-shadow">
                    <div class="text-lg font-bold text-blue-600">₹600</div>
                    <div class="text-xs text-gray-500">Rewards Earned</div>
                </div>
                <div class="bg-white p-3 rounded-lg card-shadow">
                    <div class="text-lg font-bold text-purple-600">8</div>
                    <div class="text-xs text-gray-500">Areas Cleaned</div>
                </div>
            </div>
        </div>

        <!-- Progress Tracking Screen -->
        <div id="progressScreen" class="hidden p-4">
            <div class="mb-4">
                <button onclick="goToSuccess()" class="text-blue-600 text-sm">← Back</button>
                <h3 class="text-lg font-semibold text-center">Cleanup Progress</h3>
            </div>

            <!-- Progress Timeline -->
            <div class="space-y-4">
                <div class="flex items-center">
                    <div class="w-8 h-8 bg-green-500 rounded-full flex items-center justify-center text-white text-sm font-bold mr-3">✓</div>
                    <div class="flex-1">
                        <div class="text-sm font-medium">Report Received</div>
                        <div class="text-xs text-gray-500">2 minutes ago</div>
                    </div>
                </div>
                
                <div class="flex items-center">
                    <div class="w-8 h-8 bg-green-500 rounded-full flex items-center justify-center text-white text-sm font-bold mr-3">✓</div>
                    <div class="flex-1">
                        <div class="text-sm font-medium">Cleaning Crew Assigned</div>
                        <div class="text-xs text-gray-500">1 minute ago</div>
                    </div>
                </div>
                
                <div class="flex items-center">
                    <div class="w-8 h-8 bg-blue-500 rounded-full flex items-center justify-center text-white text-sm font-bold mr-3 pulse-animation">🚛</div>
                    <div class="flex-1">
                        <div class="text-sm font-medium">Crew En Route</div>
                        <div class="text-xs text-gray-500">ETA: 45 minutes</div>
                    </div>
                </div>
                
                <div class="flex items-center opacity-50">
                    <div class="w-8 h-8 bg-gray-300 rounded-full flex items-center justify-center text-gray-500 text-sm font-bold mr-3">4</div>
                    <div class="flex-1">
                        <div class="text-sm font-medium">Cleanup in Progress</div>
                        <div class="text-xs text-gray-500">Pending</div>
                    </div>
                </div>
                
                <div class="flex items-center opacity-50">
                    <div class="w-8 h-8 bg-gray-300 rounded-full flex items-center justify-center text-gray-500 text-sm font-bold mr-3">5</div>
                    <div class="flex-1">
                        <div class="text-sm font-medium">Cleanup Complete</div>
                        <div class="text-xs text-gray-500">Pending</div>
                    </div>
                </div>
            </div>

            <!-- Live Updates -->
            <div class="mt-6 bg-blue-50 p-3 rounded-lg">
                <div class="text-sm font-medium text-blue-800 mb-1">Live Update</div>
                <div class="text-xs text-blue-600">Cleaning crew "Team Alpha" is 2.3 km away from the location</div>
            </div>
        </div>
    </div>

    <script>
        function startReporting() {
            document.getElementById('welcomeScreen').classList.add('hidden');
            document.getElementById('cameraScreen').classList.remove('hidden');
        }

        function goBack() {
            document.getElementById('cameraScreen').classList.add('hidden');
            document.getElementById('welcomeScreen').classList.remove('hidden');
        }

        function capturePhoto() {
            document.getElementById('cameraScreen').classList.add('hidden');
            document.getElementById('reviewScreen').classList.remove('hidden');
        }

        function retakePhoto() {
            document.getElementById('reviewScreen').classList.add('hidden');
            document.getElementById('cameraScreen').classList.remove('hidden');
        }

        function submitReport() {
            document.getElementById('reviewScreen').classList.add('hidden');
            document.getElementById('successScreen').classList.remove('hidden');
        }

        function trackProgress() {
            document.getElementById('successScreen').classList.add('hidden');
            document.getElementById('progressScreen').classList.remove('hidden');
        }

        function goToSuccess() {
            document.getElementById('progressScreen').classList.add('hidden');
            document.getElementById('successScreen').classList.remove('hidden');
        }

        function reportAnother() {
            document.getElementById('successScreen').classList.add('hidden');
            document.getElementById('welcomeScreen').classList.remove('hidden');
        }

        // Simulate real-time updates
        setTimeout(() => {
            const updates = document.querySelectorAll('.pulse-animation');
            updates.forEach(el => {
                el.style.animationDuration = '1s';
            });
        }, 3000);
    </script>
<script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'98f8336cc78917b2',t:'MTc2MDYyNDQ2OC4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script></body>
</html>
