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
        Caricamento immagini astronomiche...
    </div>

    <img id="cosmo-slide" src="" alt="Cosmology Data" style="width: 100%; height: 100%; object-fit: cover; opacity: 0; transition: opacity 1s ease-in-out; position: relative; z-index: 10;">

</div>

</div>
</div>

<script>
document.addEventListener("DOMContentLoaded", function() {
    
    // MAGIA DI GITHUB PAGES: Questo codice dice al server di cercare fisicamente 
    // i file nelle tue due cartelle e inserirli nell'elenco durante la pubblicazione.
    // Nessuna chiamata API esterna, impossibile che venga bloccato!
    let imageUrls = [
        {% for file in site.static_files %}
            {% if file.path contains 'App/cluster_img/' or file.path contains 'App/galaxy_img/' %}
                "{{ file.path | relative_url }}",
            {% endif %}
        {% endfor %}
    ];

    // Rimuove eventuali righe vuote per sicurezza
    imageUrls = imageUrls.filter(url => url.trim() !== "");

    if (imageUrls.length === 0) {
        document.getElementById("loading-text").innerText = "In attesa delle immagini. Se le hai appena caricate, attendi 1 minuto che GitHub aggiorni il sito.";
        return;
    }

    // Nascondi la scritta di caricamento
    document.getElementById("loading-text").style.display = "none";

    // Mescola l'ordine casualmente
    imageUrls.sort(() => 0.5 - Math.random());

    const imgElement = document.getElementById("cosmo-slide");
    let currentIndex = 0;

    function changeImage() {
        imgElement.style.opacity = 0; 
        
        setTimeout(() => {
            imgElement.src = imageUrls[currentIndex];
            setTimeout(() => {
                imgElement.style.opacity = 1;
            }, 100);
            
            currentIndex = (currentIndex + 1) % imageUrls.length;
        }, 1000); 
    }

    // Inizializza la prima immagine istantaneamente
    imgElement.src = imageUrls[currentIndex];
    setTimeout(() => { imgElement.style.opacity = 1; }, 100);
    currentIndex = (currentIndex + 1) % imageUrls.length;

    // Cambia immagine regolarmente
    setInterval(changeImage, 4000);
});
</script>
