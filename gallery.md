---
layout: default
title: "Gallery"
---

<div class="carousel-container">
    <div class="carousel-slides" id="carousel-slides">
        <!-- Auto-generated from group photos -->
    </div>
    <div class="carousel-nav">
        <button class="carousel-btn prev-btn" onclick="changeSlide(-1)">‹</button>
        <button class="carousel-btn next-btn" onclick="changeSlide(1)">›</button>
    </div>
    <div class="carousel-dots" id="carousel-dots">
        <!-- Auto-generated dots -->
    </div>
</div>

## Photo Gallery

<div class="gallery-grid" id="gallery-grid">
    <!-- Auto-generated from all photos -->
</div>

<!-- Lightbox -->
<div id="lightbox" class="lightbox" onclick="closeLightbox()">
    <div class="lightbox-content">
        <span class="lightbox-close" onclick="closeLightbox()">&times;</span>
        <img id="lightbox-img" src="assets/img/gallery/union_spring_2026.jpg" alt="">
        <div id="lightbox-caption" class="lightbox-caption"></div>
    </div>
</div>

<script>
// Centralized photo data - Add new photos here
const galleryPhotos = [
    {
        src: "assets/img/gallery/summer_research_poster_session_july_2026.jpg",
        alt: "Nadya and Eloise present their first poster at the 2026 Summer Research Poster Session",
        date: "July 2026",
        sortDate: "2026-07-27",
        caption: "Nadya and Eloise present their first poster at the 2026 Summer Research Poster Session",
        showInCarousel: false,
        showInGallery: true
    },
    {
        src: "assets/img/gallery/union_spring_2026.jpg",
        alt: "Union College getting ready for spring",
        date: "Spring 2026",
        sortDate: "2026-04-01",
        caption: "Union College getting ready for spring",
        showInGallery: false
    },
    {
        src: "assets/img/gallery/union_fall_2025.jpg",
        alt: "Union College in the fall",
        date: "Fall 2025",
        sortDate: "2025-10-01",
        caption: "Union College in the fall",
        showInGallery: false
    },
    {
        src: "assets/img/gallery/mrs_december_2025.jpg",
        alt: "Presenting at the MRS Fall Meeting 2025",
        date: "December 2025",
        sortDate: "2025-12-01",
        caption: "Presenting at the MRS Fall Meeting 2025 in Boston",
        showInGallery: true
    },
    {
        src: "assets/img/gallery/binghamton_invited_talk_february_2026.jpg",
        alt: "Invited talk at Binghamton University",
        date: "February 2026",
        sortDate: "2026-02-01",
        caption: "Invited talk at Binghamton University",
        showInGallery: true
    },
    {
        src: "assets/img/gallery/glovebox_installation.jpg",
        alt: "Installation of our custom-made glovebox system for the lab",
        date: "May 2026",
        sortDate: "2026-05-01",
        caption: "Installation of our custom-made glovebox system for the lab",
        showInGallery: true
    },
    {
        src: "assets/img/gallery/glovebox_ready_spin_coating_june_2026.jpg",
        alt: "Glovebox ready for spin coating thin films",
        date: "June 2026",
        sortDate: "2026-06-11",
        caption: "Our glovebox is now ready to use, with the capability to spin coat thin films inside",
        showInGallery: true
    }
];

// Auto-generate carousel from all photos
function generateCarousel() {
    const carouselSlides = document.getElementById('carousel-slides');
    const carouselDots = document.getElementById('carousel-dots');
    const carouselPhotos = galleryPhotos.filter(photo => photo.showInCarousel !== false);
    
    // Generate slides
    carouselSlides.innerHTML = carouselPhotos.map((photo, index) => `
        <div class="carousel-slide ${index === 0 ? 'active' : ''}">
            <img src="${photo.src}" alt="${photo.alt}">
            <div class="carousel-caption">${photo.caption} - ${photo.date}</div>
        </div>
    `).join('');
    
    // Generate dots
    carouselDots.innerHTML = carouselPhotos.map((_, index) => `
        <span class="dot ${index === 0 ? 'active' : ''}" onclick="currentSlide(${index + 1})"></span>
    `).join('');
}

// Auto-generate gallery grid from all photos
function generateGallery() {
    const galleryGrid = document.getElementById('gallery-grid');
    const galleryOnlyPhotos = galleryPhotos
        .filter(photo => photo.showInGallery)
        .sort((a, b) => new Date(b.sortDate) - new Date(a.sortDate));
    
    galleryGrid.innerHTML = galleryOnlyPhotos.map(photo => `
        <div class="gallery-item" onclick="openLightbox('${photo.src}', '${photo.alt}', '${photo.date}')">
            <img src="${photo.src}" alt="${photo.alt}">
            <div class="gallery-caption">
                <div class="gallery-date">${photo.date}</div>
                ${photo.caption}
            </div>
        </div>
    `).join('');
}

// Initialize gallery on page load
document.addEventListener('DOMContentLoaded', function() {
    generateCarousel();
    generateGallery();
});

// Carousel functionality
let slideIndex = 1;

function changeSlide(n) {
    showSlide(slideIndex += n);
}

function currentSlide(n) {
    showSlide(slideIndex = n);
}

function showSlide(n) {
    let slides = document.getElementsByClassName("carousel-slide");
    let dots = document.getElementsByClassName("dot");
    
    if (n > slides.length) {slideIndex = 1}
    if (n < 1) {slideIndex = slides.length}
    
    for (let i = 0; i < slides.length; i++) {
        slides[i].classList.remove("active");
    }
    
    for (let i = 0; i < dots.length; i++) {
        dots[i].classList.remove("active");
    }
    
    if (slides[slideIndex-1]) {
        slides[slideIndex-1].classList.add("active");
    }
    if (dots[slideIndex-1]) {
        dots[slideIndex-1].classList.add("active");
    }
}

// Auto-slide disabled - manual navigation only

// Lightbox functionality
function openLightbox(imageSrc, imageAlt, imageDate) {
    const lightbox = document.getElementById('lightbox');
    const lightboxImg = document.getElementById('lightbox-img');
    const lightboxCaption = document.getElementById('lightbox-caption');
    
    lightboxImg.src = imageSrc;
    lightboxImg.alt = imageAlt;
    lightboxCaption.innerHTML = `<strong>${imageDate}</strong><br>${imageAlt}`;
    
    lightbox.classList.add('active');
    document.body.style.overflow = 'hidden';
}

function closeLightbox() {
    const lightbox = document.getElementById('lightbox');
    lightbox.classList.remove('active');
    document.body.style.overflow = 'auto';
}

// Close lightbox with escape key
document.addEventListener('keydown', function(event) {
    if (event.key === 'Escape') {
        closeLightbox();
    }
});
</script>
