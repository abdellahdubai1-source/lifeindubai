/* ==========================================================================
   Life in Dubai KAL — Scripts
   Handles: sticky navbar, mobile menu, smooth scroll, scroll-fade animations.
   Vanilla JS only — no dependencies.
   ========================================================================== */

(function () {
  "use strict";

  /* ---------- Sticky / solid navbar on scroll ---------- */
  var header = document.getElementById("site-header");

  function updateHeaderState() {
    if (!header) return;
    if (window.scrollY > 40) {
      header.classList.add("scrolled");
    } else {
      header.classList.remove("scrolled");
    }
  }

  updateHeaderState();
  window.addEventListener("scroll", updateHeaderState, { passive: true });

  /* ---------- Mobile hamburger menu ---------- */
  var navToggle = document.getElementById("navToggle");
  var navMenu = document.getElementById("navMenu");

  function openMenu() {
    navMenu.classList.add("open");
    navToggle.setAttribute("aria-expanded", "true");
    navToggle.setAttribute("aria-label", "Close menu");
    document.body.style.overflow = "hidden";
  }

  function closeMenu() {
    navMenu.classList.remove("open");
    navToggle.setAttribute("aria-expanded", "false");
    navToggle.setAttribute("aria-label", "Open menu");
    document.body.style.overflow = "";
  }

  if (navToggle && navMenu) {
    navToggle.addEventListener("click", function () {
      var isOpen = navMenu.classList.contains("open");
      if (isOpen) {
        closeMenu();
      } else {
        openMenu();
      }
    });

    /* Close the menu after a link is selected */
    var navLinks = navMenu.querySelectorAll("a");
    navLinks.forEach(function (link) {
      link.addEventListener("click", closeMenu);
    });

    /* Close the menu when pressing Escape */
    document.addEventListener("keydown", function (e) {
      if (e.key === "Escape" && navMenu.classList.contains("open")) {
        closeMenu();
        navToggle.focus();
      }
    });
  }

  /* ---------- Smooth scroll for in-page anchor links ---------- */
  var anchorLinks = document.querySelectorAll('a[href^="#"]');

  anchorLinks.forEach(function (link) {
    link.addEventListener("click", function (e) {
      var targetId = link.getAttribute("href");
      if (!targetId || targetId === "#") return;

      var targetEl = document.querySelector(targetId);
      if (!targetEl) return;

      e.preventDefault();
      targetEl.scrollIntoView({ behavior: "smooth", block: "start" });

      /* Update focus for accessibility once scrolled */
      targetEl.setAttribute("tabindex", "-1");
      targetEl.focus({ preventScroll: true });
    });
  });

  /* ---------- Fade-up on scroll (respects prefers-reduced-motion) ---------- */
  var prefersReducedMotion = window.matchMedia(
    "(prefers-reduced-motion: reduce)"
  ).matches;

  var fadeEls = document.querySelectorAll(".fade-up");

  if (prefersReducedMotion || !("IntersectionObserver" in window)) {
    /* Show everything immediately if motion is reduced or IO unsupported */
    fadeEls.forEach(function (el) {
      el.classList.add("in-view");
    });
  } else {
    var observer = new IntersectionObserver(
      function (entries) {
        entries.forEach(function (entry) {
          if (entry.isIntersecting) {
            entry.target.classList.add("in-view");
            observer.unobserve(entry.target);
          }
        });
      },
      { threshold: 0.15, rootMargin: "0px 0px -60px 0px" }
    );

    fadeEls.forEach(function (el) {
      observer.observe(el);
    });
  }

  /* ---------- Ensure hero video plays inline on mobile browsers ---------- */
  var heroVideo = document.querySelector(".hero-video");
  if (heroVideo) {
    heroVideo.play().catch(function () {
      /* Autoplay may be blocked by the browser; video poster remains visible */
    });
  }
})();
