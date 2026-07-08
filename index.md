---
layout: default
title: Home
permalink: /
description: "Cosmo-Edu-Lab brings modern cosmology into the high school curriculum through real data and inquiry-based learning."
# image: "/assets/images/home.jpg"          # uncomment once the file exists in assets/images/ — recommended ~1600x700px
# image_alt: "The night sky over a telescope"
---
<div class="hero" markdown="1">
<p class="eyebrow">Cosmo-Edu-Lab — An Educational Project</p>

# Bring the universe to the classroom

<p class="lead">Cosmo-Edu-Lab is an educational project which brings modern cosmology, one of humanity’s greatest intellectual achievements, into the high school curriculum using real observational data, and understand how the universe works.</p>

* **The project** makes selected concepts in cosmology — from dark matter to inflation — accessible and engaging, allowing students to connect familiar physics tools with the frontiers of science.
* **The digital platform** where all concepts are deployed in interactive activities based on real data.

<div class="hero-actions" markdown="1">

- **[About the project]({{ '/about/' | relative_url }})** What Cosmo-Edu-Lab is and why it exists.
- **[Our approach]({{ '/approach/' | relative_url }})** The commitments behind the project.
- **[The app]({{ '/app/' | relative_url }})** Download the platform and explore its features.
{: .grid}

</div>
</div>

<div id="cosmo-slideshow-container" style="max-width: 900px; margin: 4rem auto; border-radius: 16px; overflow: hidden; box-shadow: 0 20px 40px rgba(0,0,0,0.4); aspect-ratio: 16/9; background: #0d1117; position: relative;">
    <img id="cosmo-slide" src="" alt="Cosmology Images" style="width: 100%; height: 100%; object-fit: cover; opacity: 0; transition: opacity 1s ease-in-out;">
</div>

<script>
document.addEventListener("DOMContentLoaded", async function() {
    // URL dell'API di GitHub che punta direttamente alle tue cartelle
    const apiBase = "https://api.github.com/repos/cosmo-edu-lab/cosmo-edu-lab/contents/App";
    const folders = ["cluster_img", "galaxy_img"];
    let imageUrls = [];

    try {
        // 1. Recupera la lista dei file da entrambe le cartelle
        for (const folder of folders) {
            const response = await fetch(`${apiBase}/${folder}`);
            if (response.ok) {
                const data = await response.json();
                // Filtra solo i file immagine e salva il link diretto (download_url)
                const images = data
                    .filter(file => file.name.match(/\.(jpg|jpeg|png|gif|webp)$/i))
                    .map(file => file.download_url);
                imageUrls = imageUrls.concat(images);
            }
        }

        if (imageUrls.length === 0) return;

        // 2. Mescola l'array di immagini in modo casuale
        imageUrls.sort(() => 0.5 - Math.random());

        const imgElement = document.getElementById("cosmo-slide");
        let currentIndex = 0;

        // 3. Funzione per cambiare immagine con effetto dissolvenza incrociata
        function changeImage() {
            // Rimuove l'opacità (inizia il fade out)
            imgElement.style.opacity = 0;
            
            // Aspetta 1 secondo (il tempo della transizione CSS) prima di cambiare l'immagine
            setTimeout(() => {
                imgElement.src = imageUrls[currentIndex];
                
                // Appena la nuova immagine è scaricata, la rende visibile (fade in)
                imgElement.onload = () => {
                    imgElement.style.opacity = 1;
                };
                
                // Passa all'indice successivo (o riparte da zero se è finita la lista)
                currentIndex = (currentIndex + 1) % imageUrls.length;
            }, 1000); 
        }

        // Avvia la prima immagine
        changeImage();
        
        // Imposta il timer: cambia immagine ogni 4.5 secondi (3.5s visibile + 1s di transizione)
        setInterval(changeImage, 4500);

    } catch (error) {
        console.error("Errore nel caricamento delle immagini astronomiche:", error);
    }
});
</script>
