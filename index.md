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

<div style="display: flex; flex-wrap: wrap; gap: 2rem; align-items: stretch; margin-top: 3rem;" markdown="1">

<div class="hero-actions" markdown="1" style="flex: 1; min-width: 300px; margin: 0;">

- **[About the project]({{ '/about/' | relative_url }})** What Cosmo-Edu-Lab is and why it exists.
- **[Our approach]({{ '/approach/' | relative_url }})** The commitments behind the project.
- **[The app]({{ '/app/' | relative_url }})** Download the platform and explore its features.
{: .grid}

</div>

<div id="cosmo-slideshow-container" style="flex: 1; min-width: 300px; border-radius: 16px; overflow: hidden; box-shadow: 0 20px 40px rgba(0,0,0,0.4); aspect-ratio: 16/9; background: #0d1117; position: relative; margin: 0;">
    <img id="cosmo-slide" src="https://images.unsplash.com/photo-1462331940025-496dfbfc7564?auto=format&fit=crop&w=800&q=80" alt="Cosmology Images" style="width: 100%; height: 100%; object-fit: cover; opacity: 1; transition: opacity 1s ease-in-out;">
</div>

</div>
</div>

<script>
document.addEventListener("DOMContentLoaded", async function() {
    const apiBase = "https://api.github.com/repos/cosmo-edu-lab/cosmo-edu-lab/contents/App";
    const folders = ["cluster_img", "galaxy_img"];
    
    // Array di fallback: se GitHub blocca l'API per troppi tentativi, usa queste immagini sicure 
    // anziché mostrare un riquadro nero.
    let imageUrls = [
        "https://images.unsplash.com/photo-1462331940025-496dfbfc7564?auto=format&fit=crop&w=800&q=80",
        "https://images.unsplash.com/photo-1614730321146-b6fa6a46bcb4?auto=format&fit=crop&w=800&q=80",
        "https://images.unsplash.com/photo-1451187580459-43490279c0fa?auto=format&fit=crop&w=800&q=80"
    ];

    try {
        let fetchedUrls = [];
        for (const folder of folders) {
            const response = await fetch(`${apiBase}/${folder}`);
            if (response.ok) {
                const data = await response.json();
                const images = data
                    .filter(file => file.name.match(/\.(jpg|jpeg|png|gif|webp)$/i))
                    .map(file => file.download_url);
                fetchedUrls = fetchedUrls.concat(images);
            }
        }
        
        // Se l'API ha successo, sostituiamo le immagini di fallback con quelle vere delle tue cartelle
        if (fetchedUrls.length > 0) {
            imageUrls = fetchedUrls;
        }

        imageUrls.sort(() => 0.5 - Math.random());

        const imgElement = document.getElementById("cosmo-slide");
        let currentIndex = 0;

        function changeImage() {
            imgElement.style.opacity = 0; 
            
            setTimeout(() => {
                imgElement.onload = null; // Pulisce eventi vecchi
                imgElement.src = imageUrls[currentIndex];
                
                // Risolve il bug del browser: se l'immagine è già scaricata, mostrala subito
                if (imgElement.complete) {
                    imgElement.style.opacity = 1;
                } else {
                    imgElement.onload = () => {
                        imgElement.style.opacity = 1;
                    };
                }
                
                currentIndex = (currentIndex + 1) % imageUrls.length;
            }, 1000); 
        }

        // Aspettiamo i primi 4.5 secondi sull'immagine iniziale prima di iniziare a ruotarle
        setInterval(changeImage, 4500);

    } catch (error) {
        console.error("Errore nel caricamento delle immagini astronomiche:", error);
    }
});
</script>
