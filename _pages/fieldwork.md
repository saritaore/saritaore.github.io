---
layout: page
permalink: assets/img/
title: fieldwork
nav: true
nav_order: 3
# Photos shown in this order. Add a photo by adding two lines below.
photos:
- file: moz_fieldteamtraining.jpg
  caption: "Training the field team before data collection, Mozambique"
- file: moz_teachertraining4.jpg
  caption: "Teachers working through the session materials during training, Mozambique"
- file: moz_rural3.jpg
  caption: "Crossing the river by boat on the way to schools, Mozambique"
- file: moz_rural1.jpg
  caption: "Walking the last stretch to a school on foot, Mozambique"
- file: moz_fieldteam1.jpg
  caption: "Field team at School after intervention, Mozambique"
- file: moz_survey4.jpg
  caption: "One-on-one student survey, Mozambique"
- file: moz_interv3.jpg
  caption: "Students in an intervention session led by a trained teacher, Mozambique"
- file: moz_interv7.jpg
  caption: "Group activity during an intervention session, Mozambique"
---

<!-- _pages/fieldwork.md -->

<div class="fw-gallery" id="fw-gallery">
  <div class="fw-stage">
    <button class="fw-arrow fw-prev" type="button" aria-label="Previous photo">&#8249;</button>
    {% for photo in page.photos %}
    <figure class="fw-slide{% if forloop.first %} is-active{% endif %}">
      <img src="{{ photo.src | relative_url }}" alt="{{ photo.caption | escape }}" {% unless forloop.first %}loading="lazy"{% endunless %}>
      <figcaption>{{ photo.caption }}</figcaption>
    </figure>
    {% endfor %}
    <button class="fw-arrow fw-next" type="button" aria-label="Next photo">&#8250;</button>
  </div>

  <div class="fw-thumbs" aria-label="Fieldwork photos">
    {% for photo in page.photos %}
    <button class="fw-thumb{% if forloop.first %} is-active{% endif %}" type="button" data-index="{{ forloop.index0 }}" aria-label="Show photo: {{ photo.caption | escape }}">
      <img src="{{ photo.src | relative_url }}" alt="" loading="lazy">
    </button>
    {% endfor %}
  </div>
</div>

<style>
  .fw-gallery { max-width: 900px; margin: 0 auto; }
  .fw-stage { position: relative; }
  .fw-slide { display: none; margin: 0; text-align: center; }
  .fw-slide.is-active { display: block; }
  .fw-slide img {
    width: 100%;
    max-height: 70vh;
    object-fit: contain;
    border-radius: 4px;
  }
  .fw-slide figcaption {
    margin-top: 0.75rem;
    color: var(--global-text-color-light);
    font-size: 0.95rem;
    min-height: 1.5em;
  }
  .fw-arrow {
    position: absolute;
    top: calc(50% - 1.2rem);
    transform: translateY(-50%);
    z-index: 2;
    width: 44px;
    height: 44px;
    border: none;
    border-radius: 50%;
    background: rgba(0, 0, 0, 0.45);
    color: #fff;
    font-size: 1.8rem;
    line-height: 1;
    cursor: pointer;
    opacity: 0.8;
  }
  .fw-arrow:hover { opacity: 1; }
  .fw-prev { left: 8px; }
  .fw-next { right: 8px; }
  .fw-thumbs {
    display: flex;
    gap: 6px;
    overflow-x: auto;
    padding: 1rem 0 0.5rem;
    scroll-behavior: smooth;
  }
  .fw-thumb {
    flex: 0 0 auto;
    width: 84px;
    height: 60px;
    padding: 0;
    border: 2px solid transparent;
    border-radius: 3px;
    background: none;
    cursor: pointer;
    opacity: 0.55;
  }
  .fw-thumb img { width: 100%; height: 100%; object-fit: cover; display: block; border-radius: 2px; }
  .fw-thumb:hover { opacity: 0.85; }
  .fw-thumb.is-active { opacity: 1; border-color: var(--global-theme-color); }
  .fw-thumb:focus-visible, .fw-arrow:focus-visible { outline: 2px solid var(--global-theme-color); outline-offset: 2px; opacity: 1; }
  @media (max-width: 576px) {
    .fw-arrow { width: 36px; height: 36px; font-size: 1.4rem; }
    .fw-thumb { width: 64px; height: 46px; }
  }
  @media (prefers-reduced-motion: reduce) { .fw-thumbs { scroll-behavior: auto; } }
</style>

<script>
  (function () {
    var root = document.getElementById("fw-gallery");
    if (!root) return;
    var slides = root.querySelectorAll(".fw-slide");
    var thumbs = root.querySelectorAll(".fw-thumb");
    var n = slides.length, current = 0;
    if (n < 2) {
      root.querySelectorAll(".fw-arrow").forEach(function (b) { b.style.display = "none"; });
      return;
    }

    function show(i) {
      current = (i + n) % n;
      slides.forEach(function (s, k) { s.classList.toggle("is-active", k === current); });
      thumbs.forEach(function (t, k) {
        var on = k === current;
        t.classList.toggle("is-active", on);
        if (on) {
          var strip = t.parentElement;
          strip.scrollLeft = t.offsetLeft - strip.clientWidth / 2 + t.clientWidth / 2;
        }
      });
    }

    root.querySelector(".fw-prev").addEventListener("click", function () { show(current - 1); });
    root.querySelector(".fw-next").addEventListener("click", function () { show(current + 1); });
    thumbs.forEach(function (t) {
      t.addEventListener("click", function () { show(parseInt(t.dataset.index, 10)); });
    });
    document.addEventListener("keydown", function (e) {
      if (e.target.matches("input, textarea, [contenteditable]")) return;
      if (e.key === "ArrowLeft") show(current - 1);
      if (e.key === "ArrowRight") show(current + 1);
    });

    // Swipe on phones
    var x0 = null;
    var stage = root.querySelector(".fw-stage");
    stage.addEventListener("touchstart", function (e) { x0 = e.touches[0].clientX; }, { passive: true });
    stage.addEventListener("touchend", function (e) {
      if (x0 === null) return;
      var dx = e.changedTouches[0].clientX - x0;
      if (Math.abs(dx) > 40) show(current + (dx < 0 ? 1 : -1));
      x0 = null;
    });
  })();
</script>
