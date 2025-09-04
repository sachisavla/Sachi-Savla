
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sachi Savla | Interactive Resume</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/3.7.0/chart.min.js"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <!-- Chosen Palette: Cool Blues & Grays -->
    <!-- Application Structure Plan: A single-page, vertically scrolling layout is chosen for its narrative-like flow, mimicking the way a person would read a traditional resume but enhanced with interactivity. The structure is as follows: 1. Hero Section: Immediate impact with name, title, and key contacts. 2. Navigation Bar: Sticky navigation for easy access to different sections (Career Journey, Skills, Education, Achievements). This allows users to jump to sections of interest, supporting both linear and non-linear exploration. 3. Career Journey: An interactive timeline to showcase professional experience. Users can click on each role to expand and view details. This is more engaging than a static list and visually represents career progression over time. 4. Skills & Expertise: A dedicated section with an interactive radar chart to visually quantify skill proficiency and categorized lists for clarity. This provides a quick, data-driven overview of capabilities. 5. Education & Certifications: A clean, card-based layout to present academic background and professional development credentials. 6. Achievements: Highlights key accomplishments to reinforce qualifications. This structure was chosen to guide the user through a compelling story of professional and academic growth, while interactive elements provide depth on demand, respecting the user's time and focus. -->
    <!-- Visualization & Content Choices: 1. Professional Experience -> Goal: Show change and organize -> Viz/Method: Interactive vertical timeline (HTML/CSS/JS). Interaction: Clicking on a timeline entry reveals detailed descriptions of the role and responsibilities. Justification: A timeline is more visually engaging than a list and effectively shows career progression. It allows users to get a high-level view first, then dive into details they care about, improving usability. Method: Custom JS to toggle visibility of details. 2. Core Skills -> Goal: Compare and Inform -> Viz/Method: Radar Chart (Chart.js). Interaction: Hovering over points on the chart shows the skill name and a self-assessed proficiency level. Justification: A radar chart provides a quick, holistic visual summary of diverse skills, making it easier to grasp strengths at a glance compared to a simple list. Library: Chart.js for its simplicity and canvas-based rendering. 3. Certifications/Achievements/Education -> Goal: Inform and Organize -> Viz/Method: Styled Cards (HTML/CSS/Tailwind). Interaction: None, simple information display. Justification: For straightforward information, clean, well-organized cards are highly readable and maintain a professional aesthetic without unnecessary complexity. Method: Tailwind CSS for styling. -->
    <!-- CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #F0F4F8;
            color: #31363F;
        }
        .nav-link {
            transition: color 0.3s, border-bottom-color 0.3s;
            border-bottom: 2px solid transparent;
        }
        .nav-link:hover, .nav-link.active {
            color: #4A90E2;
            border-bottom-color: #4A90E2;
        }
        .timeline-item .icon {
            transition: transform 0.3s;
        }
        .timeline-item:hover .icon {
            transform: scale(1.2);
        }
        .details-content {
            max-height: 0;
            overflow: hidden;
            transition: max-height 0.5s ease-in-out, opacity 0.5s ease-in-out;
            opacity: 0;
        }
        .details-content.open {
            max-height: 500px;
            opacity: 1;
        }
        .chart-container {
            position: relative;
            width: 100%;
            max-width: 600px;
            margin-left: auto;
            margin-right: auto;
            height: 300px;
            max-height: 400px;
        }
        @media (min-width: 768px) {
            .chart-container {
                height: 400px;
            }
        }
    </style>
</head>
<body class="antialiased">

    <header id="header" class="bg-[#F0F4F8]/80 backdrop-blur-md sticky top-0 z-50 transition-shadow shadow-sm">
        <div class="container mx-auto px-6 py-4 flex justify-between items-center">
            <h1 class="text-xl font-bold text-[#31363F]">Sachi Savla</h1>
            <nav class="hidden md:flex space-x-8">
                <a href="#journey" class="nav-link font-medium pb-1">Career Journey</a>
                <a href="#skills" class="nav-link font-medium pb-1">Skills & Expertise</a>
                <a href="#education" class="nav-link font-medium pb-1">Education</a>
                <a href="#achievements" class="nav-link font-medium pb-1">Achievements</a>
            </nav>
            <button id="mobile-menu-button" class="md:hidden focus:outline-none">
                <div class="w-6 h-0.5 bg-[#31363F] mb-1.5"></div>
                <div class="w-6 h-0.5 bg-[#31363F]"></div>
            </button>
        </div>
        <div id="mobile-menu" class="hidden md:hidden px-6 pb-4">
            <a href="#journey" class="block py-2 nav-link">Career Journey</a>
            <a href="#skills" class="block py-2 nav-link">Skills & Expertise</a>
            <a href="#education" class="block py-2 nav-link">Education</a>
            <a href="#achievements" class="block py-2 nav-link">Achievements</a>
        </div>
    </header>

    <main class="container mx-auto px-6 py-12">
        <section id="hero" class="text-center py-16">
            <h2 class="text-4xl md:text-6xl font-extrabold text-[#31363F] leading-tight">Sachi Savla</h2>
            <p class="mt-4 text-lg md:text-xl text-[#6B778D]">BBA LLB (Hons.) Candidate</p>
            <p class="mt-2 text-[#6B778D]">Passionate about the intersection of law, technology, and business.</p>
            <div class="mt-8 flex justify-center items-center space-x-6 text-[#6B778D]">
                <a href="mailto:sachi.savla29@gmail.com" class="hover:text-[#4A90E2] transition-colors">sachi.savla29@gmail.com</a>
                <span class="text-[#D4E2F0]">|</span>
                <a href="tel:+918369254195" class="hover:text-[#4A90E2] transition-colors">+91-8369254195</a>
                <span class="text-[#D4E2F0]">|</span>
                <span>Mumbai, India</span>
            </div>
             <div class="mt-10">
                <p class="max-w-3xl mx-auto text-center text-[#6B778D]">
                    A driven and detail-oriented law student with extensive internship experience in litigation, corporate law, and regulatory compliance. My background includes hands-on work in legal research, contract drafting, and case management, complemented by a strong academic record and leadership in extracurricular activities. I am passionate about leveraging my skills to contribute meaningfully to the legal field.
                </p>
            </div>
        </section>

        <section id="journey" class="py-16">
            <h3 class="text-3xl font-bold text-center mb-12 text-[#31363F] flex items-center justify-center">💼 <span class="ml-4">Career Journey</span></h3>
            <div class="relative max-w-2xl mx-auto">
                <div class="absolute left-1/2 top-0 h-full w-0.5 bg-[#D4E2F0]"></div>
                <div id="timeline-container" class="space-y-12">
                </div>
            </div>
        </section>

        <section id="skills" class="py-16 bg-[#F8FBFD] rounded-2xl">
            <h3 class="text-3xl font-bold text-center mb-4 text-[#31363F] flex items-center justify-center">✨ <span class="ml-4">Skills & Expertise</span></h3>
             <p class="text-center text-[#6B778D] mb-12 max-w-2xl mx-auto">This section provides a visual and categorized overview of my core competencies. The chart interactively displays my proficiency across key legal and technical domains, while the lists below detail my specific skills. This combination offers a quick yet comprehensive understanding of my capabilities.</p>
            <div class="grid md:grid-cols-2 gap-12 items-center">
                <div class="chart-container">
                    <canvas id="skillsChart"></canvas>
                </div>
                <div class="space-y-6">
                    <div>
                        <h4 class="font-semibold text-lg mb-2 text-[#4A90E2]">Core Legal Skills</h4>
                        <ul class="list-disc list-inside text-[#6B778D] space-y-1">
                            <li>Legal Research & Analysis</li>
                            <li>Contract Drafting & Vetting</li>
                            <li>Regulatory Compliance (SEBI)</li>
                            <li>Litigation Support & Case Management</li>
                            <li>Arbitration & Mediation Preparation</li>
                        </ul>
                    </div>
                    <div>
                        <h4 class="font-semibold text-lg mb-2 text-[#4A90E2]">Technical & Soft Skills</h4>
                        <ul class="list-disc list-inside text-[#6B778D] space-y-1">
                            <li>AI Prompt Engineering</li>
                            <li>Client Relations & Consultation</li>
                            <li>Google Cybersecurity Certified</li>
                            <li>GDPR & Data Protection Knowledge</li>
                            <li>Public Speaking & Presentation</li>
                        </ul>
                    </div>
                </div>
            </div>
        </section>

        <section id="education" class="py-16">
            <h3 class="text-3xl font-bold text-center mb-12 text-[#31363F] flex items-center justify-center">🎓 <span class="ml-4">Education & Certifications</span></h3>
             <p class="text-center text-[#6B778D] mb-12 max-w-2xl mx-auto">My academic foundation is rooted in a rigorous legal and business curriculum, supplemented by specialized certifications in high-growth areas like cybersecurity and data privacy. This section outlines the formal training that underpins my practical skills and professional experience.</p>
            <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-8">
                <div class="bg-white p-6 rounded-lg shadow-sm border border-[#D4E2F0]">
                    <h4 class="font-bold text-lg">BBA LLB (Hons.)</h4>
                    <p class="text-[#4A90E2]">NMIMS School of Law</p>
                    <p class="text-sm text-[#6B778D] mt-2">Expected 2026 | CGPA: 3.37</p>
                </div>
                <div class="bg-white p-6 rounded-lg shadow-sm border border-[#D4E2F0]">
                    <h4 class="font-bold text-lg">Higher Secondary (XII)</h4>
                    <p class="text-[#4A90E2]">St. Xavier's College, Mumbai</p>
                    <p class="text-sm text-[#6B778D] mt-2">2021 | 85%</p>
                </div>
                <div class="bg-white p-6 rounded-lg shadow-sm border border-[#D4E2F0] md:col-span-2 lg:col-span-1">
                    <h4 class="font-bold text-lg">Certifications</h4>
                     <ul class="list-disc list-inside text-sm text-[#6B778D] mt-2 space-y-1">
                         <li>Google Cybersecurity Certificate</li>
                         <li>GDPR & Data Protection (Udemy)</li>
                         <li>Cyber Security: Ethical Hacking (Udemy)</li>
                     </ul>
                </div>
            </div>
        </section>

         <section id="achievements" class="py-16">
            <h3 class="text-3xl font-bold text-center mb-12 text-[#31363F] flex items-center justify-center">🏆 <span class="ml-4">Key Achievements</span></h3>
            <p class="text-center text-[#6B778D] mb-12 max-w-2xl mx-auto">Beyond my academic and professional roles, I have actively pursued opportunities to test and refine my skills in competitive and leadership settings. This area highlights significant accomplishments that demonstrate my commitment to excellence and my ability to perform under pressure.</p>
            <div class="max-w-3xl mx-auto space-y-4">
                <div class="bg-white p-4 rounded-lg shadow-sm border border-[#D4E2F0] flex items-center">
                    <span class="text-xl text-[#4A90E2] mr-4">🥇</span>
                    <p>Runner-up, IMC Annual ADR Moot Court Competition with ICC, Paris (2024)</p>
                </div>
                <div class="bg-white p-4 rounded-lg shadow-sm border border-[#D4E2F0] flex items-center">
                    <span class="text-xl text-[#4A90E2] mr-4">🗣️</span>
                    <p>3rd Best Speaker, Intra-Moot Court Competition (2022)</p>
                </div>
                <div class="bg-white p-4 rounded-lg shadow-sm border border-[#D4E2F0] flex items-center">
                    <span class="text-xl text-[#4A90E2] mr-4">📝</span>
                     <p>Campus Topper in Economics, Semester III (2023)</p>
                </div>
                 <div class="bg-white p-4 rounded-lg shadow-sm border border-[#D4E2F0] flex items-center">
                    <span class="text-xl text-[#4A90E2] mr-4">🤝</span>
                    <p>Executive Member, Placement Committee (2021-2023)</p>
                </div>
            </div>
        </section>

    </main>

    <footer class="bg-white border-t border-[#D4E2F0] mt-12">
        <div class="container mx-auto px-6 py-6 text-center text-[#6B778D]">
            <p>&copy; 2025 Sachi Savla. All Rights Reserved.</p>
        </div>
    </footer>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            const mobileMenuButton = document.getElementById('mobile-menu-button');
            const mobileMenu = document.getElementById('mobile-menu');
            mobileMenuButton.addEventListener('click', () => {
                mobileMenu.classList.toggle('hidden');
            });

            const navLinks = document.querySelectorAll('.nav-link');
            navLinks.forEach(link => {
                link.addEventListener('click', () => {
                    if (!mobileMenu.classList.contains('hidden')) {
                         mobileMenu.classList.add('hidden');
                    }
                });
            });
            
            const sections = document.querySelectorAll('main section');
            const headerNavLinks = document.querySelectorAll('header nav a');

            const observerOptions = {
                root: null,
                rootMargin: '0px',
                threshold: 0.4
            };

            const observer = new IntersectionObserver((entries, observer) => {
                entries.forEach(entry => {
                    if (entry.isIntersecting) {
                        headerNavLinks.forEach(link => {
                            link.classList.remove('active');
                            if (link.getAttribute('href').substring(1) === entry.target.id) {
                                link.classList.add('active');
                            }
                        });
                    }
                });
            }, observerOptions);

            sections.forEach(section => {
                observer.observe(section);
            });

            const experienceData = [
                {
                    role: "Legal Intern",
                    company: "JB Laalwani and Co.",
                    date: "Most Recent",
                    side: 'left',
                    details: [
                        "Gained extensive experience in litigation, working on a diverse portfolio of family matters and property cases.",
                        "Drafted and vetted contracts, including redlining for clarity and legal compliance.",
                        "Assisted in arbitration proceedings and worked on complex mergers and acquisition cases."
                    ]
                },
                {
                    role: "Legal Intern",
                    company: "Chambers of Adv. Kevic Setalvad",
                    date: "Jun-Jul 2025",
                    side: 'right',
                    details: [
                        "Attended court proceedings at Bombay High Court, SAT, DRT & DRAT, gaining comprehensive litigation exposure.",
                        "Conducted in-depth legal research on testamentary matters, bail hearings, and NI Act Section 138 cases."
                    ]
                },
                {
                    role: "Legal Intern",
                    company: "Regsteel Law",
                    date: "Dec 2024",
                    side: 'left',
                    details: [
                        "Drafted comprehensive legal notes, client meeting minutes, and case briefs for SEBI-related matters.",
                        "Conducted specialized research on SEBI regulations for insider trading defenses."
                    ]
                },
                {
                    role: "Legal Intern",
                    company: "Olive Law",
                    date: "Jul 2024",
                    side: 'right',
                    details: [
                        "Prepared detailed case presentations for mediation sessions and client consultations.",
                        "Organized case documents and evidence for arbitration hearings."
                    ]
                },
                 {
                    role: "Legal Intern",
                    company: "K Ashar & Co.",
                    date: "Jun-Dec 2023",
                    side: 'left',
                    details: [
                        "Researched Maharashtra property laws and Company Secretary roles under Companies Act.",
                        "Drafted property agreements and conducted title searches."
                    ]
                }
            ];

            const timelineContainer = document.getElementById('timeline-container');
            experienceData.forEach((item, index) => {
                const alignClass = item.side === 'left' ? 'md:text-right' : 'md:text-left';
                const itemHTML = `
                    <div class="timeline-item relative cursor-pointer group" data-index="${index}">
                        <div class="absolute left-1/2 -translate-x-1/2 top-1/2 -translate-y-1/2 w-4 h-4 rounded-full bg-white border-2 border-[#4A90E2] icon"></div>
                        <div class="grid md:grid-cols-2 gap-4">
                            <div class="${item.side === 'left' ? 'md:col-start-1 md:text-right' : 'md:col-start-2 md:text-left'}">
                                <div class="bg-white p-4 rounded-lg shadow-sm border border-[#D4E2F0]">
                                    <p class="font-semibold">${item.role}</p>
                                    <p class="text-sm text-[#4A90E2]">${item.company}</p>
                                    <p class="text-xs text-[#6B778D] mt-1">${item.date}</p>
                                </div>
                            </div>
                        </div>
                        <div class="md:grid md:grid-cols-2 gap-4">
                             <div class="details-content mt-2 col-span-2 text-sm text-[#6B778D]" id="details-${index}">
                                 <ul class="list-disc list-inside bg-white p-4 rounded-lg shadow-sm border border-[#D4E2F0] space-y-2">
                                     ${item.details.map(d => `<li>${d}</li>`).join('')}
                                 </ul>
                            </div>
                        </div>
                    </div>`;
                timelineContainer.innerHTML += itemHTML;
            });
            
            document.querySelectorAll('.timeline-item').forEach(item => {
                const itemContent = item.querySelector('.bg-white');
                itemContent.addEventListener('click', (e) => {
                     e.stopPropagation();
                    const index = item.getAttribute('data-index');
                    const details = document.getElementById(`details-${index}`);
                    details.classList.toggle('open');
                });
            });

            const ctx = document.getElementById('skillsChart').getContext('2d');
            const skillsChart = new Chart(ctx, {
                type: 'radar',
                data: {
                    labels: ['Legal Research', 'Contract Drafting', 'Regulatory Compliance', 'Litigation Support', 'AI Prompt Engineering', 'Client Relations'],
                    datasets: [{
                        label: 'Proficiency',
                        data: [90, 85, 80, 88, 75, 95],
                        backgroundColor: 'rgba(74, 144, 226, 0.2)',
                        borderColor: 'rgba(74, 144, 226, 1)',
                        pointBackgroundColor: 'rgba(74, 144, 226, 1)',
                        pointBorderColor: '#fff',
                        pointHoverBackgroundColor: '#fff',
                        pointHoverBorderColor: 'rgba(74, 144, 226, 1)'
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    scales: {
                        r: {
                            angleLines: {
                                color: '#D4E2F0'
                            },
                            grid: {
                                color: '#D4E2F0'
                            },
                            pointLabels: {
                                font: {
                                    size: 12,
                                    family: 'Inter, sans-serif'
                                },
                                color: '#6B778D'
                            },
                            ticks: {
                                backdropColor: 'transparent',
                                stepSize: 20,
                                display: false
                            },
                            suggestedMin: 0,
                            suggestedMax: 100
                        }
                    },
                    plugins: {
                        legend: {
                            display: false
                        }
                    }
                }
            });
        });
    </script>
</body>
</html>

