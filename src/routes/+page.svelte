<script>
	import { onMount } from 'svelte';

	let activeSection = $state('home');
	let scrollY = $state(0);
	let isMenuOpen = $state(false);

	const services = [
		{
			icon: '🧘‍♀️',
			title: 'Meditation',
			description:
				'Find inner peace through guided meditation practices designed to calm your mind and awaken your spirit.',
			image: 'https://images.unsplash.com/photo-1506126613408-eca07ce68773?w=800&q=80'
		},
		{
			icon: '🌿',
			title: 'Holistic Healing',
			description:
				'Experience natural healing therapies that nurture your body, mind, and soul in perfect harmony.',
			image: 'https://images.unsplash.com/photo-1544161515-4ab6ce6db874?w=800&q=80'
		},
		{
			icon: '✨',
			title: 'Energy Work',
			description:
				'Balance your chakras and restore your natural energy flow for complete spiritual alignment.',
			image: 'https://images.unsplash.com/photo-1518241353330-0f7941c2d9b5?w=800&q=80'
		},
		{
			icon: '🕉️',
			title: 'Yoga Classes',
			description:
				'Transform your practice with yoga sessions that connect breath, movement, and consciousness.',
			image: 'https://images.unsplash.com/photo-1588286840104-8957b019727f?w=800&q=80'
		}
	];

	const testimonials = [
		{
			name: 'Sarah Mitchell',
			text: 'This journey has transformed my life. I found peace I never knew existed within me.',
			role: 'Meditation Student',
			image: 'https://images.unsplash.com/photo-1438761681033-6461ffad8d80?w=400&q=80'
		},
		{
			name: 'David Chen',
			text: 'The holistic approach here is truly life-changing. Every session brings new insights.',
			role: 'Wellness Client',
			image: 'https://images.unsplash.com/photo-1507003211169-0a1dd7228f2d?w=400&q=80'
		},
		{
			name: 'Emma Rodriguez',
			text: 'I finally feel aligned with my true self. The guidance here is exceptional.',
			role: 'Yoga Practitioner',
			image: 'https://images.unsplash.com/photo-1494790108377-be9c29b29330?w=400&q=80'
		}
	];

	onMount(() => {
		const handleScroll = () => {
			scrollY = window.scrollY;

			const sections = ['home', 'about', 'services', 'testimonials', 'contact'];
			const current = sections.find((section) => {
				const element = document.getElementById(section);
				if (element) {
					const rect = element.getBoundingClientRect();
					return rect.top <= 100 && rect.bottom >= 100;
				}
				return false;
			});

			if (current) activeSection = current;
		};

		window.addEventListener('scroll', handleScroll);
		return () => window.removeEventListener('scroll', handleScroll);
	});

	function scrollToSection(sectionId) {
		const element = document.getElementById(sectionId);
		if (element) {
			element.scrollIntoView({ behavior: 'smooth' });
			isMenuOpen = false;
		}
	}
</script>

<svelte:head>
	<title>Serene Path - Spiritual Wellness & Healing</title>
	<meta
		name="description"
		content="Find your inner peace through meditation, holistic healing, and spiritual guidance"
	/>
</svelte:head>

<div class="app">
	<!-- Navigation -->
	<nav class="nav" class:scrolled={scrollY > 50}>
		<div class="nav-container">
			<div class="logo">
				<span class="logo-icon">🌸</span>
				<span class="logo-text">Serene Path</span>
			</div>

			<button
				class="menu-toggle"
				onclick={() => (isMenuOpen = !isMenuOpen)}
				aria-label="Toggle menu"
			>
				<span></span>
				<span></span>
				<span></span>
			</button>

			<ul class="nav-links" class:open={isMenuOpen}>
				{#each ['home', 'about', 'services', 'testimonials', 'contact'] as section}
					<li>
						<button
							onclick={() => scrollToSection(section)}
							class:active={activeSection === section}
						>
							{section.charAt(0).toUpperCase() + section.slice(1)}
						</button>
					</li>
				{/each}
			</ul>
		</div>
	</nav>

	<!-- Hero Section -->
	<section id="home" class="hero">
		<div class="hero-bg"></div>
		<div class="hero-overlay"></div>
		<div class="hero-content">
			<h1 class="fade-in">Find Your Inner Light</h1>
			<p class="hero-subtitle fade-in-delay">
				Embark on a transformative journey to wellness, peace, and spiritual awakening
			</p>
			<button class="cta-button fade-in-delay-2" onclick={() => scrollToSection('contact')}>
				Begin Your Journey
			</button>
		</div>
		<div class="hero-decoration">
			<div class="circle circle-1"></div>
			<div class="circle circle-2"></div>
			<div class="circle circle-3"></div>
		</div>
	</section>

	<!-- About Section -->
	<section id="about" class="about">
		<div class="container">
			<div class="about-content">
				<div class="about-image">
					<img
						src="https://images.unsplash.com/photo-1545389336-cf090694435e?w=1200&q=80"
						alt="Peaceful meditation space"
						class="about-img"
					/>
				</div>
				<div class="about-text">
					<h2>Welcome to Your Sanctuary</h2>
					<p>
						At Serene Path, we believe that true wellness comes from harmony between mind, body, and
						spirit. Our holistic approach combines ancient wisdom with modern practices to guide you
						on your unique journey to inner peace.
					</p>
					<p>
						Whether you're seeking relief from stress, spiritual growth, or simply a moment of
						tranquility in your busy life, we provide a nurturing space where you can reconnect with
						your authentic self.
					</p>
					<div class="about-features">
						<div class="feature">
							<span class="feature-icon">💫</span>
							<span>10+ Years Experience</span>
						</div>
						<div class="feature">
							<span class="feature-icon">🌟</span>
							<span>Certified Practitioners</span>
						</div>
						<div class="feature">
							<span class="feature-icon">🙏</span>
							<span>Holistic Approach</span>
						</div>
					</div>
				</div>
			</div>
		</div>
	</section>

	<!-- Services Section -->
	<section id="services" class="services">
		<div class="container">
			<h2 class="section-title">Our Sacred Offerings</h2>
			<p class="section-subtitle">Discover paths to healing and transformation</p>

			<div class="services-grid">
				{#each services as service, i}
					<div class="service-card" style="animation-delay: {i * 0.1}s">
						<div class="service-image">
							<img src={service.image} alt={service.title} />
							<div class="service-icon-overlay">{service.icon}</div>
						</div>
						<div class="service-content">
							<h3>{service.title}</h3>
							<p>{service.description}</p>
						</div>
					</div>
				{/each}
			</div>
		</div>
	</section>

	<!-- Testimonials Section -->
	<section id="testimonials" class="testimonials">
		<div class="container">
			<h2 class="section-title">Voices of Transformation</h2>
			<p class="section-subtitle">Stories from our community</p>

			<div class="testimonials-grid">
				{#each testimonials as testimonial, i}
					<div class="testimonial-card" style="animation-delay: {i * 0.15}s">
						<div class="quote-mark">"</div>
						<p class="testimonial-text">{testimonial.text}</p>
						<div class="testimonial-author">
							<img src={testimonial.image} alt={testimonial.name} class="author-avatar" />
							<div class="author-info">
								<strong>{testimonial.name}</strong>
								<span>{testimonial.role}</span>
							</div>
						</div>
					</div>
				{/each}
			</div>
		</div>
	</section>

	<!-- Contact Section -->
	<section id="contact" class="contact">
		<div class="container">
			<h2 class="section-title">Start Your Journey</h2>
			<p class="section-subtitle">Reach out and take the first step toward inner peace</p>

			<div class="contact-content">
				<div class="contact-info">
					<div class="info-item">
						<span class="info-icon">📍</span>
						<div>
							<h4>Visit Us</h4>
							<p>123 Serenity Lane<br />Peaceful Valley, CA 94000</p>
						</div>
					</div>
					<div class="info-item">
						<span class="info-icon">📧</span>
						<div>
							<h4>Email</h4>
							<p>hello@serenepath.com</p>
						</div>
					</div>
					<div class="info-item">
						<span class="info-icon">📞</span>
						<div>
							<h4>Call</h4>
							<p>(555) 123-4567</p>
						</div>
					</div>
				</div>

				<form class="contact-form">
					<input type="text" placeholder="Your Name" required />
					<input type="email" placeholder="Your Email" required />
					<textarea placeholder="Your Message" rows="5" required></textarea>
					<button type="submit" class="submit-button">Send Message</button>
				</form>
			</div>
		</div>
	</section>

	<!-- Footer -->
	<footer class="footer">
		<div class="container">
			<div class="footer-content">
				<div class="footer-logo">
					<span class="logo-icon">🌸</span>
					<span class="logo-text">Serene Path</span>
				</div>
				<p class="footer-text">© 2025 Serene Path. All rights reserved. Find your light within.</p>
			</div>
		</div>
	</footer>
</div>

<style>
	:global(*) {
		margin: 0;
		padding: 0;
		box-sizing: border-box;
	}

	:global(body) {
		font-family:
			'Inter',
			-apple-system,
			BlinkMacSystemFont,
			'Segoe UI',
			Roboto,
			sans-serif;
		color: #2c3e50;
		line-height: 1.6;
		overflow-x: hidden;
	}

	.app {
		width: 100%;
		overflow-x: hidden;
	}

	/* Navigation */
	.nav {
		position: fixed;
		top: 0;
		left: 0;
		right: 0;
		z-index: 1000;
		background: rgba(255, 255, 255, 0.95);
		backdrop-filter: blur(10px);
		transition: all 0.3s ease;
		box-shadow: 0 2px 10px rgba(0, 0, 0, 0);
	}

	.nav.scrolled {
		box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
	}

	.nav-container {
		max-width: 1200px;
		margin: 0 auto;
		padding: 1.5rem 2rem;
		display: flex;
		justify-content: space-between;
		align-items: center;
	}

	.logo {
		display: flex;
		align-items: center;
		gap: 0.5rem;
		font-size: 1.5rem;
		font-weight: 600;
		color: #6b5b95;
	}

	.logo-icon {
		font-size: 2rem;
	}

	.nav-links {
		display: flex;
		gap: 2rem;
		list-style: none;
	}

	.nav-links button {
		background: none;
		border: none;
		color: #2c3e50;
		font-size: 1rem;
		cursor: pointer;
		padding: 0.5rem 0;
		position: relative;
		transition: color 0.3s ease;
	}

	.nav-links button:hover,
	.nav-links button.active {
		color: #6b5b95;
	}

	.nav-links button.active::after {
		content: '';
		position: absolute;
		bottom: 0;
		left: 0;
		right: 0;
		height: 2px;
		background: #6b5b95;
	}

	.menu-toggle {
		display: none;
		flex-direction: column;
		gap: 4px;
		background: none;
		border: none;
		cursor: pointer;
		padding: 0.5rem;
	}

	.menu-toggle span {
		width: 25px;
		height: 3px;
		background: #2c3e50;
		border-radius: 3px;
		transition: all 0.3s ease;
	}

	/* Hero Section */
	.hero {
		min-height: 100vh;
		display: flex;
		align-items: center;
		justify-content: center;
		position: relative;
		padding: 2rem;
		overflow: hidden;
	}

	.hero-bg {
		position: absolute;
		top: 0;
		left: 0;
		right: 0;
		bottom: 0;
		background-image: url('https://images.unsplash.com/photo-1528715471579-d1bcf0ba5e83?w=1920&q=80');
		background-size: cover;
		background-position: center;
		background-attachment: fixed;
	}

	.hero-overlay {
		position: absolute;
		top: 0;
		left: 0;
		right: 0;
		bottom: 0;
		background: linear-gradient(
			135deg,
			rgba(245, 247, 250, 0.95) 0%,
			rgba(232, 238, 245, 0.9) 100%
		);
	}

	.hero-content {
		text-align: center;
		z-index: 2;
		max-width: 800px;
	}

	.hero h1 {
		font-size: 4rem;
		font-weight: 700;
		color: #6b5b95;
		margin-bottom: 1.5rem;
		line-height: 1.2;
	}

	.hero-subtitle {
		font-size: 1.5rem;
		color: #5a6a7f;
		margin-bottom: 2.5rem;
		font-weight: 300;
	}

	.cta-button {
		background: linear-gradient(135deg, #6b5b95 0%, #8b7bb8 100%);
		color: white;
		border: none;
		padding: 1.2rem 3rem;
		font-size: 1.1rem;
		border-radius: 50px;
		cursor: pointer;
		transition: all 0.3s ease;
		box-shadow: 0 10px 30px rgba(107, 91, 149, 0.3);
	}

	.cta-button:hover {
		transform: translateY(-3px);
		box-shadow: 0 15px 40px rgba(107, 91, 149, 0.4);
	}

	.hero-decoration {
		position: absolute;
		width: 100%;
		height: 100%;
		top: 0;
		left: 0;
		z-index: 1;
		pointer-events: none;
	}

	.circle {
		position: absolute;
		border-radius: 50%;
		background: linear-gradient(135deg, rgba(107, 91, 149, 0.1) 0%, rgba(139, 123, 184, 0.1) 100%);
	}

	.circle-1 {
		width: 500px;
		height: 500px;
		top: -200px;
		right: -100px;
		animation: float 20s infinite ease-in-out;
	}

	.circle-2 {
		width: 300px;
		height: 300px;
		bottom: -100px;
		left: -50px;
		animation: float 15s infinite ease-in-out reverse;
	}

	.circle-3 {
		width: 200px;
		height: 200px;
		top: 50%;
		left: 10%;
		animation: float 10s infinite ease-in-out;
	}

	@keyframes float {
		0%,
		100% {
			transform: translateY(0) rotate(0deg);
		}
		50% {
			transform: translateY(-30px) rotate(5deg);
		}
	}

	.fade-in {
		animation: fadeIn 1s ease-out;
	}

	.fade-in-delay {
		animation: fadeIn 1s ease-out 0.3s backwards;
	}

	.fade-in-delay-2 {
		animation: fadeIn 1s ease-out 0.6s backwards;
	}

	@keyframes fadeIn {
		from {
			opacity: 0;
			transform: translateY(30px);
		}
		to {
			opacity: 1;
			transform: translateY(0);
		}
	}

	/* Container */
	.container {
		max-width: 1200px;
		margin: 0 auto;
		padding: 5rem 2rem;
	}

	.section-title {
		font-size: 3rem;
		text-align: center;
		color: #6b5b95;
		margin-bottom: 1rem;
		font-weight: 700;
	}

	.section-subtitle {
		text-align: center;
		font-size: 1.2rem;
		color: #5a6a7f;
		margin-bottom: 4rem;
		font-weight: 300;
	}

	/* About Section */
	.about {
		background: white;
	}

	.about-content {
		display: grid;
		grid-template-columns: 1fr 1fr;
		gap: 4rem;
		align-items: center;
	}

	.image-placeholder {
		width: 100%;
		height: 400px;
		background: linear-gradient(135deg, #f5f7fa 0%, #e8eef5 100%);
		border-radius: 20px;
		display: flex;
		align-items: center;
		justify-content: center;
	}

	.about-img {
		width: 100%;
		height: 500px;
		object-fit: cover;
		border-radius: 20px;
		box-shadow: 0 20px 60px rgba(0, 0, 0, 0.15);
	}

	.zen-icon {
		font-size: 8rem;
		opacity: 0.5;
	}

	.about-text h2 {
		font-size: 2.5rem;
		color: #6b5b95;
		margin-bottom: 1.5rem;
	}

	.about-text p {
		font-size: 1.1rem;
		color: #5a6a7f;
		margin-bottom: 1.5rem;
		line-height: 1.8;
	}

	.about-features {
		display: flex;
		gap: 2rem;
		margin-top: 2rem;
	}

	.feature {
		display: flex;
		align-items: center;
		gap: 0.5rem;
		font-weight: 500;
		color: #2c3e50;
	}

	.feature-icon {
		font-size: 1.5rem;
	}

	/* Services Section */
	.services {
		background: linear-gradient(135deg, #f5f7fa 0%, #e8eef5 100%);
	}

	.services-grid {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
		gap: 2rem;
	}

	.service-card {
		background: white;
		border-radius: 20px;
		overflow: hidden;
		transition: all 0.3s ease;
		box-shadow: 0 5px 20px rgba(0, 0, 0, 0.05);
		animation: slideUp 0.6s ease-out backwards;
	}

	@keyframes slideUp {
		from {
			opacity: 0;
			transform: translateY(30px);
		}
		to {
			opacity: 1;
			transform: translateY(0);
		}
	}

	.service-card:hover {
		transform: translateY(-10px);
		box-shadow: 0 15px 40px rgba(107, 91, 149, 0.2);
	}

	.service-image {
		position: relative;
		height: 250px;
		overflow: hidden;
	}

	.service-image img {
		width: 100%;
		height: 100%;
		object-fit: cover;
		transition: transform 0.5s ease;
	}

	.service-card:hover .service-image img {
		transform: scale(1.1);
	}

	.service-icon-overlay {
		position: absolute;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%);
		font-size: 4rem;
		background: rgba(255, 255, 255, 0.95);
		width: 100px;
		height: 100px;
		border-radius: 50%;
		display: flex;
		align-items: center;
		justify-content: center;
		box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
	}

	.service-content {
		padding: 2rem;
		text-align: center;
	}

	.service-icon {
		font-size: 4rem;
		margin-bottom: 1rem;
	}

	.service-card h3 {
		font-size: 1.5rem;
		color: #6b5b95;
		margin-bottom: 1rem;
	}

	.service-card p {
		color: #5a6a7f;
		line-height: 1.8;
	}

	/* Testimonials Section */
	.testimonials {
		background: white;
	}

	.testimonials-grid {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
		gap: 2rem;
	}

	.testimonial-card {
		background: linear-gradient(135deg, #f5f7fa 0%, #e8eef5 100%);
		padding: 2.5rem;
		border-radius: 20px;
		position: relative;
		animation: slideUp 0.6s ease-out backwards;
	}

	.quote-mark {
		font-size: 4rem;
		color: #6b5b95;
		opacity: 0.2;
		position: absolute;
		top: 1rem;
		left: 1.5rem;
	}

	.testimonial-text {
		font-size: 1.1rem;
		color: #2c3e50;
		margin-bottom: 1.5rem;
		line-height: 1.8;
		position: relative;
		z-index: 1;
	}

	.testimonial-author {
		display: flex;
		align-items: center;
		gap: 1rem;
	}

	.author-avatar {
		width: 60px;
		height: 60px;
		border-radius: 50%;
		object-fit: cover;
		border: 3px solid white;
		box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
	}

	.author-info {
		display: flex;
		flex-direction: column;
		gap: 0.3rem;
	}

	.testimonial-author strong {
		color: #6b5b95;
		font-size: 1.1rem;
	}

	.testimonial-author span {
		color: #5a6a7f;
		font-size: 0.9rem;
	}

	/* Contact Section */
	.contact {
		background: linear-gradient(135deg, #f5f7fa 0%, #e8eef5 100%);
	}

	.contact-content {
		display: grid;
		grid-template-columns: 1fr 1fr;
		gap: 4rem;
	}

	.contact-info {
		display: flex;
		flex-direction: column;
		gap: 2rem;
	}

	.info-item {
		display: flex;
		gap: 1.5rem;
		align-items: flex-start;
	}

	.info-icon {
		font-size: 2rem;
	}

	.info-item h4 {
		color: #6b5b95;
		font-size: 1.3rem;
		margin-bottom: 0.5rem;
	}

	.info-item p {
		color: #5a6a7f;
		line-height: 1.8;
	}

	.contact-form {
		display: flex;
		flex-direction: column;
		gap: 1.5rem;
	}

	.contact-form input,
	.contact-form textarea {
		padding: 1rem 1.5rem;
		border: 2px solid #e8eef5;
		border-radius: 10px;
		font-size: 1rem;
		font-family: inherit;
		transition: all 0.3s ease;
		background: white;
	}

	.contact-form input:focus,
	.contact-form textarea:focus {
		outline: none;
		border-color: #6b5b95;
	}

	.submit-button {
		background: linear-gradient(135deg, #6b5b95 0%, #8b7bb8 100%);
		color: white;
		border: none;
		padding: 1.2rem;
		font-size: 1.1rem;
		border-radius: 10px;
		cursor: pointer;
		transition: all 0.3s ease;
	}

	.submit-button:hover {
		transform: translateY(-2px);
		box-shadow: 0 10px 30px rgba(107, 91, 149, 0.3);
	}

	/* Footer */
	.footer {
		background: #2c3e50;
		color: white;
		padding: 3rem 2rem;
	}

	.footer-content {
		max-width: 1200px;
		margin: 0 auto;
		text-align: center;
	}

	.footer-logo {
		display: flex;
		align-items: center;
		justify-content: center;
		gap: 0.5rem;
		font-size: 1.5rem;
		font-weight: 600;
		margin-bottom: 1rem;
	}

	.footer-text {
		color: rgba(255, 255, 255, 0.7);
		font-size: 0.9rem;
	}

	/* Responsive Design */
	@media (max-width: 768px) {
		.menu-toggle {
			display: flex;
		}

		.nav-links {
			position: fixed;
			top: 80px;
			left: 0;
			right: 0;
			background: white;
			flex-direction: column;
			padding: 2rem;
			gap: 1rem;
			box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
			transform: translateY(-100%);
			opacity: 0;
			visibility: hidden;
			transition: all 0.3s ease;
		}

		.nav-links.open {
			transform: translateY(0);
			opacity: 1;
			visibility: visible;
		}

		.hero h1 {
			font-size: 2.5rem;
		}

		.hero-subtitle {
			font-size: 1.2rem;
		}

		.section-title {
			font-size: 2rem;
		}

		.about-content,
		.contact-content {
			grid-template-columns: 1fr;
			gap: 2rem;
		}

		.services-grid,
		.testimonials-grid {
			grid-template-columns: 1fr;
		}

		.about-features {
			flex-direction: column;
			gap: 1rem;
		}
	}
</style>
