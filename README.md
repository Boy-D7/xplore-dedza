# xplore-dedza
a tourism website showcasing the beauty of Dedza, Malawi.
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>XploreDedza | Discover Malawi's Highland Gem</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&family=Montserrat:wght@700;800&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css" />
    <style>
        :root {
            --primary: #2a5d34;
            --secondary: #d4a017;
            --accent: #8b4513;
            --light: #f8f4e9;
            --dark: #1e2a1f;
            --text: #333333;
            --shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
            --transition: all 0.3s ease;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Poppins', sans-serif;
            color: var(--text);
            background-color: var(--light);
            line-height: 1.6;
            overflow-x: hidden;
        }

        h1, h2, h3, h4 {
            font-family: 'Montserrat', sans-serif;
            font-weight: 700;
            color: var(--primary);
        }

        .container {
            width: 100%;
            max-width: 1200px;
            margin: 0 auto;
            padding: 0 20px;
        }

        .section-title {
            text-align: center;
            margin-bottom: 50px;
            position: relative;
        }

        .section-title h2 {
            font-size: 2.5rem;
            display: inline-block;
            margin-bottom: 15px;
        }

        .section-title:after {
            content: '';
            display: block;
            width: 80px;
            height: 4px;
            background: var(--secondary);
            margin: 0 auto;
        }

        .btn {
            background: var(--secondary);
            color: var(--dark);
            border: none;
            padding: 12px 28px;
            border-radius: 30px;
            font-weight: 600;
            cursor: pointer;
            transition: var(--transition);
            font-size: 1rem;
            text-decoration: none;
            display: inline-block;
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        .btn:hover {
            background: #e0b52a;
            transform: translateY(-3px);
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
        }

        /* Header & Navigation */
        header {
            background: var(--primary);
            color: white;
            padding: 15px 0;
            position: fixed;
            width: 100%;
            top: 0;
            z-index: 1000;
            box-shadow: var(--shadow);
        }

        .header-container {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .logo {
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .logo i {
            color: var(--secondary);
            font-size: 1.8rem;
        }

        .logo h1 {
            font-size: 1.8rem;
            color: white;
            margin: 0;
        }

        nav ul {
            display: flex;
            list-style: none;
            gap: 30px;
        }

        nav a {
            color: white;
            text-decoration: none;
            font-weight: 500;
            font-size: 1.1rem;
            transition: var(--transition);
            padding: 5px 10px;
            border-radius: 4px;
        }

        nav a:hover, nav a.active {
            background: var(--secondary);
            color: var(--dark);
        }

        .hamburger {
            display: none;
            cursor: pointer;
            background: none;
            border: none;
            color: white;
            font-size: 1.8rem;
        }

        /* Hero Section */
        .hero {
            height: 100vh;
            background: linear-gradient(rgba(0, 0, 0, 0.4), rgba(0, 0, 0, 0.4)), url('https://images.unsplash.com/photo-1516026672322-bc52d61a55d5?ixlib=rb-4.0.3') no-repeat center center/cover;
            display: flex;
            align-items: center;
            text-align: center;
            color: white;
            padding-top: 80px;
        }

        .hero-content {
            max-width: 800px;
            margin: 0 auto;
            padding: 0 20px;
        }

        .hero h2 {
            font-size: 3.5rem;
            margin-bottom: 20px;
            color: white;
            text-shadow: 0 2px 4px rgba(0, 0, 0, 0.5);
            line-height: 1.2;
        }

        .hero p {
            font-size: 1.4rem;
            margin-bottom: 30px;
            text-shadow: 0 1px 3px rgba(0, 0, 0, 0.5);
        }

        /* Introduction Section */
        .intro {
            padding: 100px 0;
            background: var(--light);
        }

        .intro-content {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 40px;
            align-items: center;
        }

        .intro-image {
            border-radius: 10px;
            overflow: hidden;
            box-shadow: var(--shadow);
        }

        .intro-image img {
            width: 100%;
            height: auto;
            display: block;
            transition: var(--transition);
        }

        .intro-image img:hover {
            transform: scale(1.03);
        }

        .intro-text h3 {
            font-size: 2rem;
            margin-bottom: 20px;
            color: var(--accent);
        }

        .intro-text p {
            margin-bottom: 20px;
        }

        /* Attractions Section */
        .attractions {
            padding: 80px 0;
            background: #eef5e9;
        }

        .attractions-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 30px;
        }

        .attraction-card {
            background: white;
            border-radius: 10px;
            overflow: hidden;
            box-shadow: var(--shadow);
            transition: var(--transition);
        }

        .attraction-card:hover {
            transform: translateY(-10px);
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.15);
        }

        .attraction-img {
            height: 200px;
            overflow: hidden;
        }

        .attraction-img img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            transition: var(--transition);
        }

        .attraction-card:hover .attraction-img img {
            transform: scale(1.1);
        }

        .attraction-content {
            padding: 25px;
        }

        .attraction-content h3 {
            font-size: 1.5rem;
            margin-bottom: 15px;
            color: var(--primary);
        }

        /* Map Section */
        .map-section {
            padding: 80px 0;
            background: var(--light);
        }

        #map {
            height: 500px;
            width: 100%;
            border-radius: 10px;
            overflow: hidden;
            box-shadow: var(--shadow);
        }

        /* Testimonials Section */
        .testimonials {
            padding: 80px 0;
            background: linear-gradient(to right, var(--primary), var(--dark));
            color: white;
        }

        .testimonials .section-title h2 {
            color: white;
        }

        .testimonials-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 30px;
        }

        .testimonial-card {
            background: rgba(255, 255, 255, 0.1);
            padding: 30px;
            border-radius: 10px;
            backdrop-filter: blur(10px);
        }

        .testimonial-text {
            font-style: italic;
            margin-bottom: 20px;
            position: relative;
        }

        .testimonial-text:before {
            content: '"';
            font-size: 4rem;
            position: absolute;
            top: -20px;
            left: -10px;
            opacity: 0.2;
        }

        .testimonial-author {
            display: flex;
            align-items: center;
            gap: 15px;
        }

        .author-img {
            width: 60px;
            height: 60px;
            border-radius: 50%;
            overflow: hidden;
            border: 2px solid var(--secondary);
        }

        .author-img img {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }

        /* Gallery Section */
        .gallery {
            padding: 80px 0;
            background: #eef5e9;
        }

        .gallery-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 15px;
        }

        .gallery-item {
            border-radius: 8px;
            overflow: hidden;
            height: 250px;
            box-shadow: var(--shadow);
            transition: var(--transition);
            position: relative;
        }

        .gallery-item img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            transition: var(--transition);
        }

        .gallery-item:hover img {
            transform: scale(1.1);
        }

        .gallery-item:after {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(0, 0, 0, 0.2);
            opacity: 0;
            transition: var(--transition);
        }

        .gallery-item:hover:after {
            opacity: 1;
        }

        /* Contact Section */
        .contact {
            padding: 80px 0;
            background: var(--light);
        }

        .contact-container {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 40px;
        }

        .contact-info {
            background: var(--primary);
            color: white;
            padding: 40px;
            border-radius: 10px;
        }

        .contact-info h3 {
            color: white;
            margin-bottom: 30px;
        }

        .contact-details {
            display: flex;
            flex-direction: column;
            gap: 25px;
        }

        .contact-item {
            display: flex;
            gap: 15px;
            align-items: flex-start;
        }

        .contact-icon {
            font-size: 1.5rem;
            color: var(--secondary);
        }

        .social-links {
            display: flex;
            gap: 15px;
            margin-top: 20px;
        }

        .social-links a {
            display: flex;
            align-items: center;
            justify-content: center;
            width: 40px;
            height: 40px;
            background: rgba(255, 255, 255, 0.1);
            color: white;
            border-radius: 50%;
            transition: var(--transition);
            text-decoration: none;
        }

        .social-links a:hover {
            background: var(--secondary);
            color: var(--dark);
            transform: translateY(-5px);
        }

        .contact-form .form-group {
            margin-bottom: 20px;
        }

        .contact-form input,
        .contact-form textarea {
            width: 100%;
            padding: 12px 15px;
            border: 1px solid #ddd;
            border-radius: 5px;
            font-family: 'Poppins', sans-serif;
            font-size: 1rem;
        }

        .contact-form textarea {
            height: 150px;
        }

        /* Footer */
        footer {
            background: var(--dark);
            color: white;
            padding: 40px 0 20px;
            text-align: center;
        }

        .footer-logo {
            font-size: 2rem;
            font-weight: 700;
            margin-bottom: 20px;
            color: var(--secondary);
        }

        .copyright {
            padding-top: 30px;
            border-top: 1px solid rgba(255, 255, 255, 0.1);
            color: #aaa;
            font-size: 0.9rem;
        }

        /* Mobile Navigation */
        .mobile-nav {
            position: fixed;
            top: 0;
            right: -300px;
            width: 280px;
            height: 100vh;
            background: var(--primary);
            z-index: 1001;
            padding: 80px 30px 30px;
            transition: var(--transition);
            box-shadow: -5px 0 15px rgba(0, 0, 0, 0.2);
        }

        .mobile-nav.active {
            right: 0;
        }

        .mobile-nav ul {
            list-style: none;
        }

        .mobile-nav li {
            margin-bottom: 20px;
        }

        .mobile-nav a {
            color: white;
            text-decoration: none;
            font-size: 1.2rem;
            display: block;
            padding: 10px;
            border-radius: 4px;
            transition: var(--transition);
        }

        .mobile-nav a:hover {
            background: var(--secondary);
            color: var(--dark);
        }

        .close-nav {
            position: absolute;
            top: 20px;
            right: 20px;
            background: none;
            border: none;
            color: white;
            font-size: 1.8rem;
            cursor: pointer;
        }

        /* Responsive Design */
        @media (max-width: 992px) {
            .intro-content,
            .contact-container {
                grid-template-columns: 1fr;
            }
            
            .intro-image {
                max-width: 500px;
                margin: 0 auto;
            }
            
            .hero h2 {
                font-size: 2.8rem;
            }
        }

        @media (max-width: 768px) {
            nav ul {
                display: none;
            }
            
            .hamburger {
                display: block;
            }
            
            .hero h2 {
                font-size: 2.2rem;
            }
            
            .hero p {
                font-size: 1.1rem;
            }
            
            .section-title h2 {
                font-size: 2rem;
            }

            #map {
                height: 400px;
            }
        }

        @media (max-width: 576px) {
            .hero {
                padding-top: 140px;
            }
            
            .logo h1 {
                font-size: 1.5rem;
            }
            
            .section-title h2 {
                font-size: 1.8rem;
            }
        }
    </style>
</head>
<body>
    <!-- Header Section -->
    <header>
        <div class="container header-container">
            <div class="logo">
                <i class="fas fa-mountain"></i>
                <h1>XploreDedza</h1>
            </div>
            <nav>
                <ul>
                    <li><a href="#" class="active">Home</a></li>
                    <li><a href="#intro">About</a></li>
                    <li><a href="#attractions">Attractions</a></li>
                    <li><a href="#map-section">Map</a></li>
                    <li><a href="#testimonials">Stories</a></li>
                    <li><a href="#gallery">Gallery</a></li>
                    <li><a href="#contact">Contact</a></li>
                </ul>
            </nav>
            <button class="hamburger">
                <i class="fas fa-bars"></i>
            </button>
        </div>
    </header>

    <!-- Mobile Navigation -->
    <div class="mobile-nav">
        <button class="close-nav">
            <i class="fas fa-times"></i>
        </button>
        <ul>
            <li><a href="#" class="active">Home</a></li>
            <li><a href="#intro">About</a></li>
            <li><a href="#attractions">Attractions</a></li>
            <li><a href="#map-section">Map</a></li>
            <li><a href="#testimonials">Stories</a></li>
            <li><a href="#gallery">Gallery</a></li>
            <li><a href="#contact">Contact</a></li>
        </ul>
    </div>

    <!-- Hero Section -->
    <section class="hero">
        <div class="hero-content">
            <h2>Discover the Hidden Gem of Malawi</h2>
            <p>Experience the breathtaking beauty, rich culture, and warm hospitality of Dedza</p>
            <a href="#attractions" class="btn">Explore Dedza</a>
        </div>
    </section>

    <!-- Introduction Section -->
    <section id="intro" class="intro">
        <div class="container">
            <div class="section-title">
                <h2>Welcome to XploreDedza</h2>
            </div>
            <div class="intro-content">
                <div class="intro-image">
                    <img src="https://images.unsplash.com/photo-1519046904884-53103b34b206?ixlib=rb-4.0.3" alt="Dedza Landscape">
                </div>
                <div class="intro-text">
                    <h3>The Heart of Malawi</h3>
                    <p>XploreDedza is your gateway to discovering one of Malawi's most captivating regions. Nestled in the highlands, Dedza offers stunning landscapes, rich cultural heritage, and unforgettable experiences.</p>
                    <p>Our mission is to promote sustainable tourism that benefits local communities while preserving the natural beauty and cultural traditions of this remarkable area.</p>
                    <p>From the majestic Dedza Mountain to the renowned pottery workshops, every corner of this region tells a story waiting to be discovered.</p>
                    <a href="#attractions" class="btn">Discover More</a>
                </div>
            </div>
        </div>
    </section>

    <!-- Attractions Section -->
    <section id="attractions" class="attractions">
        <div class="container">
            <div class="section-title">
                <h2>Featured Attractions</h2>
            </div>
            <div class="attractions-grid">
                <div class="attraction-card">
                    <div class="attraction-img">
                        <img src="https://images.unsplash.com/photo-1540575467063-178a50c2df87?ixlib=rb-4.0.3" alt="Dedza Mountain">
                    </div>
                    <div class="attraction-content">
                        <h3>Dedza Mountain</h3>
                        <p>Hike to the highest point in Central Malawi for breathtaking 360° views. Trails range from easy walks to challenging climbs.</p>
                    </div>
                </div>
                
                <div class="attraction-card">
                    <div class="attraction-img">
                        <img src="https://images.unsplash.com/photo-1605108720274-9b88357e1d51?ixlib=rb-4.0.3" alt="Dedza Pottery">
                    </div>
                    <div class="attraction-content">
                        <h3>Dedza Pottery</h3>
                        <p>Visit the famous pottery workshop and learn centuries-old techniques from master artisans. Create your own souvenir!</p>
                    </div>
                </div>
                
                <div class="attraction-card">
                    <div class="attraction-img">
                        <img src="https://images.unsplash.com/photo-1519996529931-28324d5a630e?ixlib=rb-4.0.3" alt="Forest Reserve">
                    </div>
                    <div class="attraction-content">
                        <h3>Dedza Forest Reserve</h3>
                        <p>Explore this protected area with diverse flora and fauna. Perfect for birdwatching, nature photography, and peaceful walks.</p>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Map Section -->
    <section id="map-section" class="map-section">
        <div class="container">
            <div class="section-title">
                <h2>Explore Dedza Region</h2>
            </div>
            <div id="map"></div>
        </div>
    </section>

    <!-- Testimonials Section -->
    <section id="testimonials" class="testimonials">
        <div class="container">
            <div class="section-title">
                <h2>Local Stories & Testimonials</h2>
            </div>
            <div class="testimonials-grid">
                <div class="testimonial-card">
                    <div class="testimonial-text">
                        "The hike up Dedza Mountain was challenging but absolutely worth it. The views from the top were spectacular, and our guide was knowledgeable about the local flora and fauna."
                    </div>
                    <div class="testimonial-author">
                        <div class="author-img">
                            <img src="https://randomuser.me/api/portraits/women/44.jpg" alt="Sarah Johnson">
                        </div>
                        <div>
                            <h4>Sarah Johnson</h4>
                            <p>Adventure Traveler, UK</p>
                        </div>
                    </div>
                </div>
                
                <div class="testimonial-card">
                    <div class="testimonial-text">
                        "The pottery workshop was the highlight of our trip. Learning traditional techniques from local artisans gave us a deep appreciation for Dedza's cultural heritage."
                    </div>
                    <div class="testimonial-author">
                        <div class="author-img">
                            <img src="https://randomuser.me/api/portraits/men/32.jpg" alt="Michael Chen">
                        </div>
                        <div>
                            <h4>Michael Chen</h4>
                            <p>Cultural Enthusiast, USA</p>
                        </div>
                    </div>
                </div>
                
                <div class="testimonial-card">
                    <div class="testimonial-text">
                        "Staying in a community homestay allowed us to connect with local families and experience authentic Malawian hospitality. The food was incredible!"
                    </div>
                    <div class="testimonial-author">
                        <div class="author-img">
                            <img src="https://randomuser.me/api/portraits/women/68.jpg" alt="Amina Diallo">
                        </div>
                        <div>
                            <h4>Amina Diallo</h4>
                            <p>Sustainable Travel Advocate, Senegal</p>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Gallery Section -->
    <section id="gallery" class="gallery">
        <div class="container">
            <div class="section-title">
                <h2>Photo Gallery</h2>
            </div>
            <div class="gallery-grid">
                <div class="gallery-item">
                    <img src="https://images.unsplash.com/photo-1551632811-561732d1e306?ixlib=rb-4.0.3" alt="Mountain View">
                </div>
                <div class="gallery-item">
                    <img src="https://images.unsplash.com/photo-1586773860418-d37222d8fce3?ixlib=rb-4.0.3" alt="Pottery Making">
                </div>
                <div class="gallery-item">
                    <img src="https://images.unsplash.com/photo-1504674900247-0877df9cc836?ixlib=rb-4.0.3" alt="Local Cuisine">
                </div>
                <div class="gallery-item">
                    <img src="https://images.unsplash.com/photo-1544551763-46a013bb70d5?ixlib=rb-4.0.3" alt="Landscape">
                </div>
                <div class="gallery-item">
                    <img src="https://images.unsplash.com/photo-1593111774240-d529f12e7d84?ixlib=rb-4.0.3" alt="Village Life">
                </div>
                <div class="gallery-item">
                    <img src="https://images.unsplash.com/photo-1473496169904-658ba7c44d8a?ixlib=rb-4.0.3" alt="Sunset">
                </div>
            </div>
        </div>
    </section>

    <!-- Contact Section -->
    <section id="contact" class="contact">
        <div class="container">
            <div class="section-title">
                <h2>Contact Us</h2>
            </div>
            <div class="contact-container">
                <div class="contact-info">
                    <h3>Get In Touch</h3>
                    <div class="contact-details">
                        <div class="contact-item">
                            <div class="contact-icon">
                                <i class="fas fa-map-marker-alt"></i>
                            </div>
                            <div>
                                <h4>Location</h4>
                                <p>Dedza Town, Central Region, Malawi</p>
                            </div>
                        </div>
                        
                        <div class="contact-item">
                            <div class="contact-icon">
                                <i class="fas fa-phone-alt"></i>
                            </div>
                            <div>
                                <h4>Phone</h4>
                                <p>+265 123 456 789</p>
                            </div>
                        </div>
                        
                        <div class="contact-item">
                            <div class="contact-icon">
                                <i class="fas fa-envelope"></i>
                            </div>
                            <div>
                                <h4>Email</h4>
                                <p>info@xplorededza.org</p>
                            </div>
                        </div>
                        
                        <div class="contact-item">
                            <div class="contact-icon">
                                <i class="fas fa-clock"></i>
                            </div>
                            <div>
                                <h4>Office Hours</h4>
                                <p>Monday - Friday: 8:00 AM - 5:00 PM</p>
                                <p>Saturday: 9:00 AM - 1:00 PM</p>
                            </div>
                        </div>
                    </div>
                    <div class="social-links">
                        <a href="#"><i class="fab fa-facebook-f"></i></a>
                        <a href="#"><i class="fab fa-twitter"></i></a>
                        <a href="#"><i class="fab fa-instagram"></i></a>
                        <a href="#"><i class="fab fa-youtube"></i></a>
                    </div>
                </div>
                
                <div class="contact-form">
                    <form>
                        <div class="form-group">
                            <input type="text" placeholder="Your Name" required>
                        </div>
                        <div class="form-group">
                            <input type="email" placeholder="Your Email" required>
                        </div>
                        <div class="form-group">
                            <input type="text" placeholder="Subject">
                        </div>
                        <div class="form-group">
                            <textarea placeholder="Your Message" required></textarea>
                        </div>
                        <button type="submit" class="btn">Send Message</button>
                    </form>
                </div>
            </div>
        </div>
    </section>

    <!-- Footer -->
    <footer>
        <div class="container">
            <div class="footer-logo">XploreDedza</div>
            <p>Promoting sustainable tourism and community development in Dedza, Malawi</p>
            <div class="copyright">
                &copy; 2023 XploreDedza. All rights reserved. | Designed with ❤️ for Dedza, Malawi
            </div>
        </div>
    </footer>

    <script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>
    <script>
        // Mobile Navigation
        const hamburger = document.querySelector('.hamburger');
        const mobileNav = document.querySelector('.mobile-nav');
        const closeNav = document.querySelector('.close-nav');

        hamburger.addEventListener('click', () => {
            mobileNav.classList.add('active');
        });

        closeNav.addEventListener('click', () => {
            mobileNav.classList.remove('active');
        });

        // Smooth scrolling for navigation links
        document.querySelectorAll('a[href^="#"]').forEach(anchor => {
            anchor.addEventListener('click', function(e) {
                e.preventDefault();
                
                // Close mobile nav if open
                mobileNav.classList.remove('active');
                
                const target = document.querySelector(this.getAttribute('href'));
                if (target) {
                    window.scrollTo({
                        top: target.offsetTop - 80,
                        behavior: 'smooth'
                    });
                }
            });
        });

        // Initialize map
        const map = L.map('map').setView([-14.3775, 34.3332], 12);

        L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
            attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors'
        }).addTo(map);

        // Add markers for attractions
        const attractions = [
            {
                name: "Dedza Mountain",
                position: [-14.3800, 34.3500],
                description: "Highest point in Central Malawi with panoramic views"
            },
            {
                name: "Dedza Pottery",
                position: [-14.3820, 34.3400],
                description: "Traditional pottery workshops and cultural center"
            },
            {
                name: "Forest Reserve",
                position: [-14.3900, 34.3200],
                description: "Protected area with diverse flora and fauna"
            },
            {
                name: "Dedza Town",
                position: [-14.3775, 34.3332],
                description: "Main town with markets and local crafts"
            }
        ];

        attractions.forEach(attraction => {
            const marker = L.marker(attraction.position).addTo(map);
            marker.bindPopup(`<b>${attraction.name}</b><br>${attraction.description}`);
        });

        // Header scroll effect
        window.addEventListener('scroll', function() {
            const header = document.querySelector('header');
            if (window.scrollY > 100) {
                header.style.background = 'var(--primary)';
                header.style.boxShadow = '0 4px 12px rgba(0, 0, 0, 0.1)';
            } else {
                header.style.background = 'var(--primary)';
                header.style.boxShadow = 'none';
            }
        });

        // Form submission
        const contactForm = document.querySelector('.contact-form form');
        if (contactForm) {
            contactForm.addEventListener('submit', function(e) {
                e.preventDefault();
                alert('Thank you for your message! We will get back to you soon.');
                this.reset();
            });
        }
    </script>
</body>
</html>
