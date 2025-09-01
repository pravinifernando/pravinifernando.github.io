---
layout: default
title: "Gallery"
---

## Group Photos

<i class="fab fa-instagram" style="color: #762334;"></i> Follow us on [Instagram @fernandoresearchgroup](https://instagram.com/fernandoresearchgroup) for more lab moments and research updates!

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
        <img id="lightbox-img" src="" alt="">
        <div id="lightbox-caption" class="lightbox-caption"></div>
    </div>
</div>

<script>
// Centralized photo data - Add new photos here
const galleryPhotos = [
    // December 2024
    {
        src: "assets/img/placeholder/smiley.png",
        alt: "Research Group End-of-Year Celebration",
        date: "December 2024",
        caption: "Research group end-of-year celebration",
        isGroupPhoto: true
    },
    {
        src: "assets/img/placeholder/smiley.png",
        alt: "Paper Celebration",
        date: "December 2024",
        caption: "Celebrating paper acceptance in Nature Materials",
        isGroupPhoto: false
    },
    
    // November 2024
    {
        src: "assets/img/placeholder/smiley.png",
        alt: "Fall 2024 Group Photo",
        date: "November 2024",
        caption: "Fall 2024 group photo with new PhD students",
        isGroupPhoto: true
    },
    {
        src: "assets/img/placeholder/smiley.png",
        alt: "Conference Presentation",
        date: "November 2024",
        caption: "Presenting research at the Materials Research Society conference",
        isGroupPhoto: false
    },
    {
        src: "assets/img/placeholder/smiley.png",
        alt: "Lab Training Session",
        date: "November 2024",
        caption: "Training session on spectroscopy instrumentation",
        isGroupPhoto: false
    },
    
    // October 2024
    {
        src: "assets/img/placeholder/smiley.png",
        alt: "Collaboration Meeting",
        date: "October 2024",
        caption: "Collaboration meeting with researchers from Brookhaven National Lab",
        isGroupPhoto: false
    },
    {
        src: "assets/img/placeholder/smiley.png",
        alt: "STEM Outreach Event",
        date: "October 2024",
        caption: "High school students visiting the lab for STEM outreach",
        isGroupPhoto: false
    },
    
    // September 2024
    {
        src: "assets/img/placeholder/smiley.png",
        alt: "AFM Operation",
        date: "September 2024",
        caption: "Student operating the atomic force microscope",
        isGroupPhoto: false
    },
    {
        src: "assets/img/placeholder/smiley.png",
        alt: "Device Fabrication",
        date: "September 2024",
        caption: "Device fabrication in the controlled atmosphere glove box",
        isGroupPhoto: false
    },
    
    // August 2024
    {
        src: "assets/img/placeholder/smiley.png",
        alt: "Summer 2024 REU Group",
        date: "August 2024",
        caption: "Summer 2024 REU program group photo",
        isGroupPhoto: true
    },
    {
        src: "assets/img/placeholder/smiley.png",
        alt: "Research Group Meeting",
        date: "August 2024",
        caption: "Weekly research group meeting discussing latest findings",
        isGroupPhoto: false
    },
    
    // July 2024
    {
        src: "assets/img/placeholder/smiley.png",
        alt: "Spring 2024 Conference Group",
        date: "July 2024",
        caption: "Spring 2024 lab group after successful conference presentations",
        isGroupPhoto: true
    }
];

// Auto-generate carousel from group photos
function generateCarousel() {
    const groupPhotos = galleryPhotos.filter(photo => photo.isGroupPhoto);
    const carouselSlides = document.getElementById('carousel-slides');
    const carouselDots = document.getElementById('carousel-dots');
    
    // Generate slides
    carouselSlides.innerHTML = groupPhotos.map((photo, index) => `
        <div class="carousel-slide ${index === 0 ? 'active' : ''}">
            <img src="${photo.src}" alt="${photo.alt}">
            <div class="carousel-caption">${photo.caption} - ${photo.date}</div>
        </div>
    `).join('');
    
    // Generate dots
    carouselDots.innerHTML = groupPhotos.map((_, index) => `
        <span class="dot ${index === 0 ? 'active' : ''}" onclick="currentSlide(${index + 1})"></span>
    `).join('');
}

// Auto-generate gallery grid from all photos
function generateGallery() {
    const galleryGrid = document.getElementById('gallery-grid');
    
    galleryGrid.innerHTML = galleryPhotos.map(photo => `
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