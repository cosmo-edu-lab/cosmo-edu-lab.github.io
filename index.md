---
layout: default
title: Home
permalink: /
description: "Cosmo-Edu-Lab brings modern cosmology into the high school curriculum through real data and inquiry-based learning."
---
<div class="hero" markdown="1">
<p class="eyebrow">Cosmo-Edu-Lab — An Educational Project</p>

# Bring the universe to the classroom

<p class="lead">Cosmo-Edu-Lab is an educational project which brings modern cosmology, one of humanity’s greatest intellectual achievements, into the high school curriculum using real observational data, and understand how the universe works.</p>

* **The project** makes selected concepts in cosmology — from dark matter to inflation — accessible and engaging, allowing students to connect familiar physics tools with the frontiers of science.
* **The digital platform** where all concepts are deployed in interactive activities based on real data.

<div style="display: flex; flex-wrap: wrap; gap: 3rem; align-items: stretch; margin-top: 3rem;" markdown="1">

<div class="hero-actions" markdown="1" style="flex: 1; min-width: 280px; margin: 0;">

- **[About the project]({{ '/about/' | relative_url }})** What Cosmo-Edu-Lab is and why it exists.
- **[Our approach]({{ '/approach/' | relative_url }})** The commitments behind the project.
- **[The app]({{ '/app/' | relative_url }})** Download the platform and explore its features.
{: .grid}

</div>

<div id="cosmo-slideshow-container" style="flex: 2; min-width: 450px; border-radius: 16px; overflow: hidden; box-shadow: 0 20px 40px rgba(0,0,0,0.4); aspect-ratio: 16/9; background: #0d1117; position: relative; margin: 0;">
    
    <div id="loading-text" style="position: absolute; top: 50%; left: 50%; transform: translate(-50%, -50%); color: #64748b; font-family: monospace; font-size: 1.1rem; text-align: center; z-index: 5;">
        Inizializzazione immagini in corso...
    </div>

    <img id="cosmo-slide" src="" alt="Cosmo Edu Lab Universo" style="width: 100%; height: 100%; object-fit: cover; opacity: 0; transition: opacity 1s ease-in-out; position: relative; z-index: 10;">

</div>

</div>
</div>

<script>
document.addEventListener("DOMContentLoaded", function() {
    
    // Percorsi base crudi di GitHub per aggirare i limiti delle API
    const baseCluster = "https://raw.githubusercontent.com/cosmo-edu-lab/cosmo-edu-lab/main/App/cluster_img/";
    const baseGalaxy = "https://raw.githubusercontent.com/cosmo-edu-lab/cosmo-edu-lab/main/App/galaxy_img/";

    // Array statico con tutti i file estratti dal repository
    const imageUrls = [
        // Ammassi
        baseCluster + "Abell0080.jpg",
        baseCluster + "Abell0118.jpg",
        baseCluster + "Abell0380.jpg",
        baseCluster + "Abell0487.jpg",
        baseCluster + "Abell2734.jpg",
        baseCluster + "Abell2778.jpg",
        baseCluster + "Abell2799.jpg",
        baseCluster + "Abell2800.jpg",
        baseCluster + "Abell2819.jpg",
        baseCluster + "Abell2854.jpg",
        baseCluster + "Abell2871.jpg",
        baseCluster + "Abell2911.jpg",
        baseCluster + "Abell3864.jpg",
        baseCluster + "Abell3921.jpg",
        baseCluster + "Abell4067.jpg",
        baseCluster + "bullet_lensing.jpg",
        baseCluster + "bullet_xray.jpg",
        baseCluster + "coma_img.jpg",
        
        // Galassie
        baseGalaxy + "M31.jpg",
        baseGalaxy + "NGC0024.jpg",
        baseGalaxy + "NGC0055.jpg",
        baseGalaxy + "NGC0100.jpg",
        baseGalaxy + "NGC0247.jpg",
        baseGalaxy + "NGC0289.jpg",
        baseGalaxy + "NGC0300.jpg",
        baseGalaxy + "NGC0801.jpeg",
        baseGalaxy + "NGC0891.jpg",
        baseGalaxy + "NGC1003.jpeg",
        baseGalaxy + "NGC1090.jpg",
        baseGalaxy + "NGC1705.jpg",
        baseGalaxy + "NGC2366.jpg",
        baseGalaxy + "NGC2403.jpg",
        baseGalaxy + "NGC2683.jpg",
        baseGalaxy + "NGC2841.jpg",
        baseGalaxy + "NGC3198.jpg",
        baseGalaxy + "NGC5055.jpg",
        baseGalaxy + "NGC6946.jpg"
    ];

    // Nasconde il testo di caricamento una volta che l'array è pronto
    document.getElementById("loading-text").style.display = "none";
    
    // Mischia l'ordine delle immagini per avere uno slideshow sempre diverso
    imageUrls.sort(() => 0.5 - Math.random());

    const imgElement = document.getElementById("cosmo-slide");
    let currentIndex = 0;

    function showNextImage() {
        // Assegna l'evento ONLOAD prima di cambiare il src
        imgElement.onload = () => {
            imgElement.style.opacity = 1;
        };

        // Se per caso un URL è sbagliato o rimosso in futuro, salta alla prossima
        imgElement.onerror = () => {
            console.warn("Immagine non trovata:", imageUrls[currentIndex]);
            currentIndex = (currentIndex + 1) % imageUrls.length;
            showNextImage();
        };

        imgElement.src = imageUrls[currentIndex];
    }

    function triggerTransition() {
        // Avvia la transizione a opacità 0
        imgElement.style.opacity = 0; 
        
        // Aspetta che sfumi (1 secondo, in base al CSS), poi carica la successiva
        setTimeout(() => {
            currentIndex = (currentIndex + 1) % imageUrls.length;
            showNextImage(); 
        }, 1000); 
    }

    // Inizializza la primissima immagine
    showNextImage();

    // Loop ogni 4 secondi
    setInterval(triggerTransition, 4000);
});
</script>
