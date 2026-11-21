document.addEventListener("DOMContentLoaded", () => {
  // 1. Smooth Lagging Cursor Aura (#9cad78)
  const blob = document.getElementById("cursor-blob");
  let mouseX = window.innerWidth / 2;
  let mouseY = window.innerHeight / 2;
  let blobX = mouseX;
  let blobY = mouseY;

  if (blob) {
    window.addEventListener("pointermove", (e) => {
      mouseX = e.clientX;
      mouseY = e.clientY;
      blob.style.opacity = "1";
    });

    window.addEventListener("pointerleave", () => {
      blob.style.opacity = "0";
    });

    // Smooth animation loop so the aura glides gently behind the cursor
    function animateBlob() {
      blobX += (mouseX - blobX) * 0.12;
      blobY += (mouseY - blobY) * 0.12;
      blob.style.transform = `translate3d(${blobX - 120}px, ${blobY - 120}px, 0)`;
      requestAnimationFrame(animateBlob);
    }
    animateBlob();
  }

  // 2. Category Filtering with Gentle Fade-In
  const filterBtns = document.querySelectorAll(".filter-btn");
  const cards = document.querySelectorAll(".card");

  filterBtns.forEach((btn) => {
    btn.addEventListener("click", () => {
      filterBtns.forEach((b) => b.classList.remove("active"));
      btn.classList.add("active");

      const filter = btn.dataset.filter;

      cards.forEach((card) => {
        const match = filter === "all" || card.dataset.category === filter;
        if (match) {
          card.style.display = "block";
          card.animate(
            [
              { opacity: 0, transform: "translateY(10px)" },
              { opacity: 1, transform: "translateY(0)" },
            ],
            { duration: 280, easing: "ease-out" }
          );
        } else {
          card.style.display = "none";
        }
      });
    });
  });

  // 3. Artwork Preview Modal (Supports both <img> tags and gradient placeholders)
  const modal = document.getElementById("modal");
  const modalTitle = document.getElementById("modal-title");
  const modalMeta = document.getElementById("modal-meta");
  const modalDetails = document.getElementById("modal-details");
  const modalMedia = document.getElementById("modal-media");
  const modalClose = document.getElementById("modal-close");

  cards.forEach((card) => {
    card.addEventListener("click", () => {
      if (!modal) return;

      modalTitle.textContent = card.dataset.title || "Untitled Project";
      modalMeta.textContent = card.dataset.meta || "";
      modalDetails.textContent = card.dataset.details || "";

      // If you added an <img> inside .card-thumb, display that image in the modal
      const thumbImg = card.querySelector(".card-thumb img");
      modalMedia.innerHTML = "";

      if (thumbImg) {
        const previewImg = document.createElement("img");
        previewImg.src = thumbImg.src;
        previewImg.alt = thumbImg.alt || card.dataset.title;
        previewImg.style.width = "100%";
        previewImg.style.height = "100%";
        previewImg.style.objectFit = "contain";
        modalMedia.style.background = "#0b0d11";
        modalMedia.appendChild(previewImg);
      } else {
        modalMedia.style.background = card.dataset.bg || "#1e2330";
        modalMedia.textContent = card.dataset.title || "";
      }

      modal.classList.add("open");
    });
  });

  const closeModal = () => {
    if (modal) modal.classList.remove("open");
  };

  if (modalClose) modalClose.addEventListener("click", closeModal);
  if (modal) {
    modal.addEventListener("click", (e) => {
      if (e.target === modal) closeModal();
    });
  }

  window.addEventListener("keydown", (e) => {
    if (e.key === "Escape") closeModal();
  });

  // 4. Active Navigation Link Highlighter on Scroll
  const sections = document.querySelectorAll("section[id]");
  const navLinks = document.querySelectorAll("nav a[href^='#']");

  const observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          const id = entry.target.getAttribute("id");
          navLinks.forEach((link) => {
            link.classList.toggle("active", link.getAttribute("
