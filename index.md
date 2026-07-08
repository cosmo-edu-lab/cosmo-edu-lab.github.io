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
        Connessione al database immagini in corso...
    </div>

    <img id="cosmo-slide" src="" alt="" style="width: 100%; height: 100%; object-fit: cover; opacity: 0; transition: opacity 1s ease-in-out; position: relative; z-index: 10;">

</div>

</div>
</div>

<script>
document.addEventListener("DOMContentLoaded", async function() {
    // 1. Pulisce la memoria da eventuali link rotti scaricati nei tentativi precedenti
    sessionStorage.removeItem("cosmo_immagini_cache");

    let imageUrls = [];

    // PIANO A: Estrazione infallibile tramite URL assoluto crudo.
    // Invece di usare i link del sito web, prende i file dal codice sorgente puro di GitHub
    {% for file in site.static_files %}
        {% assign path = file.path | downcase %}
        {% if path contains 'cluster_img' or path contains 'galaxy_img' %}
            imageUrls.push("https://raw.githubusercontent.com/cosmo-edu-lab/cosmo-edu-lab/main{{ file.path }}");
        {% endif %}
    {% endfor %}

    // Rimuove eventuali stringhe difettose
    imageUrls = imageUrls.filter(url => url && url.includes("http"));

    // PIANO B: API Fallback
    if (imageUrls.length === 0) {
        try {
            const apiBase = "https://api.github.com/repos/cosmo-edu-lab/cosmo-edu-lab/contents/App";
            const folders = ["cluster_img", "galaxy_img"];
            
            for (const folder of folders) {
                const response = await fetch(`${apiBase}/${folder}`);
                if (response.ok) {
                    const data = await response.json();
                    const images = data
                        .filter(file => file.name.match(/\.(jpg|jpeg|png|gif|webp)$/i))
                        .map(file => file.download_url);
                    imageUrls = imageUrls.concat(images);
                }
            }
        } catch (error) {
            console.error("Errore API:", error);
        }
    }

    if (imageUrls.length === 0) {
        document.getElementById("loading-text").innerText = "Cartelle immagini vuote o non raggiungibili.";
        return;
    }

    document.getElementById("loading-text").style.display = "none";
    imageUrls.sort(() => 0.5 - Math.random());

    const imgElement = document.getElementById("cosmo-slide");
    let currentIndex = 0;

    function changeImage() {
        imgElement.style.opacity = 0; 
        
        setTimeout(() => {
            imgElement.src = imageUrls[currentIndex];
            
            // Aspetta che l'immagine sia effettivamente caricata prima di renderla visibile (risolve il nero fisso)
            imgElement.onload = () => {
                imgElement.style.opacity = 1;
            };
            
            // Se un'immagine dovesse essere corrotta, salta automaticamente alla successiva
            imgElement.onerror = () => {
                currentIndex = (currentIndex + 1) % imageUrls.length;
                changeImage();
            };
            
            currentIndex = (currentIndex + 1) % imageUrls.length;
        }, 1000); 
    }

    // Inizia con la prima
    imgElement.src = imageUrls[currentIndex];
    imgElement.onload = () => { imgElement.style.opacity = 1; };
    currentIndex = (currentIndex + 1) % imageUrls.length;

    setInterval(changeImage, 4000);
});
</script>
