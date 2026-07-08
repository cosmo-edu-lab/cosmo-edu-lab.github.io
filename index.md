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
        Recupero immagini dalle cartelle in corso...
    </div>

    <img id="cosmo-slide" src="" alt="Cosmology Data" style="width: 100%; height: 100%; object-fit: cover; opacity: 0; transition: opacity 1s ease-in-out; position: relative; z-index: 10;">

</div>

</div>
</div>

<script>
document.addEventListener("DOMContentLoaded", async function() {
    let imageUrls = [];

    // PIANO A: Tenta la lettura nativa di GitHub Pages
    {% for file in site.static_files %}
        {% assign path = file.path | downcase %}
        {% if path contains 'cluster_img' or path contains 'galaxy_img' %}
            imageUrls.push("{{ site.baseurl }}{{ file.path }}");
        {% endif %}
    {% endfor %}

    // PIANO B: Se il metodo nativo non vede la cartella App, usa l'API di GitHub in modo sicuro
    if (imageUrls.length === 0) {
        // Controlla la memoria per non farsi bloccare da GitHub ricaricando la pagina di continuo
        const cache = sessionStorage.getItem("cosmo_immagini_cache");
        if (cache) {
            imageUrls = JSON.parse(cache);
        } else {
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
                
                // Salva le foto scaricate nella memoria della sessione
                if (imageUrls.length > 0) {
                    sessionStorage.setItem("cosmo_immagini_cache", JSON.stringify(imageUrls));
                }
            } catch (error) {
                console.error("Errore recupero API:", error);
            }
        }
    }

    // Se ENTRAMBI i metodi falliscono
    if (imageUrls.length === 0) {
        document.getElementById("loading-text").innerText = "Non riesco ad accedere alle cartelle App/cluster_img e App/galaxy_img.";
        return;
    }

    // Togli la scritta di caricamento e inizia!
    document.getElementById("loading-text").style.display = "none";

    // Mescola l'ordine
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

    // Mostra subito la prima foto 
    imgElement.src = imageUrls[currentIndex];
    setTimeout(() => { imgElement.style.opacity = 1; }, 100);
    currentIndex = (currentIndex + 1) % imageUrls.length;

    // Fai scorrere le immagini in loop
    setInterval(changeImage, 4000);
});
</script>
