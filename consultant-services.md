---
layout: page
title: Freelance SQL Server DBA & Full-Stack Consultant
description: >-
  Senior freelance IT consultant in Sweden: SQL Server performance tuning,
  emergency DBA support and full-stack .NET/TypeScript development for
  companies across the EU. Transparent SEK pricing.
permalink: /consultant/
image:
  path: /assets/387688504_837616101175543_758639594224552948_n.jpeg
  width: 1440
  height: 1440
  alt: NoLifeKing, freelance IT consultant and SQL Server DBA
twitter:
  card: summary
consulting_schema:
  email: consulting@nolifeking85.tv
  area_served:
    - Sweden
    - European Union
---

<style type="text/css">
.consulting-container {
  margin-top: 30px;
}

.consulting-ingress {
  margin-bottom: 30px;
  line-height: 1.5;
}

.consulting-ingress .lead-text {
  font-size: 1.15rem;
  color: var(--minima-text-color);
}

/* Call To Action (CTA) button - themed after Minima's link colour */
.btn-custom-cta,
.btn-custom-cta:visited {
  display: inline-block;
  background-color: var(--minima-link-base-color);
  color: var(--minima-background-color); /* contrasts with the button in both skins */
  padding: 10px 20px;
  border-radius: 4px;
  text-decoration: none;
  font-weight: bold;
  transition: background-color 0.2s ease-in-out, opacity 0.2s ease-in-out;
}

.btn-custom-cta:hover,
.btn-custom-cta:focus {
  color: var(--minima-background-color);
  opacity: 0.85;
  text-decoration: none;
}

.category-description {
  color: var(--minima-brand-color-dimmed);
  font-style: italic;
  margin-bottom: 15px;
}

.services-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(min(300px, 100%), 1fr));
  gap: 20px;
  margin-bottom: 30px;
}

.service-card {
  border: 1px solid var(--minima-border-color-01);
  padding: 20px;
  border-radius: 4px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  background-color: transparent;
}

.service-card h3 {
  margin-top: 0;
  font-size: 1.1rem;
}

.service-description {
  font-size: 0.95rem;
  color: var(--minima-text-color);
}

.service-footer {
  margin-top: 15px;
  border-top: 1px solid var(--minima-border-color-01);
  padding-top: 12px;
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
  justify-content: space-between;
  align-items: center;
}

.service-pricing .price-amount {
  font-weight: bold;
  font-size: 1.05rem;
  color: var(--minima-text-color);
}

.service-pricing .price-type {
  font-size: 0.8rem;
  color: var(--minima-brand-color-dimmed);
}

/* Individual item callout element linking directly to email */
.btn-service-cta,
.btn-service-cta:visited {
  font-size: 0.85rem;
  color: var(--minima-link-base-color);
  text-decoration: none;
  font-weight: bold;
  border: 1px solid var(--minima-link-base-color);
  padding: 4px 10px;
  border-radius: 3px;
  transition: background-color 0.2s;
}

.btn-service-cta:hover,
.btn-service-cta:focus {
  color: var(--minima-link-base-color);
  background-color: color-mix(in srgb, var(--minima-link-base-color) 10%, transparent);
  text-decoration: none;
}

.category-divider {
  margin: 30px 0;
  border: 0;
  border-top: 1px solid var(--minima-border-color-01);
}
</style>

{% assign sorted_categories = site.data.consulting.categories | sort: "order" %}
{% assign all_services = site.data.consulting.services | sort: "order" %}

<div class="consulting-container">
<header class="consulting-ingress">
      <p class="lead-text">
        <strong>Looking for senior technical expertise?</strong> I offer specialized freelance consulting services spanning full-stack software development, high-throughput backend systems, cloud infrastructure architectures, and deep-dive database optimization.
      </p>
      <p>
        Whether you need emergency on-call DBA incident response to resolve a production bottleneck, a structural review of your application's data layer, or a custom training workshop for your engineering team, I am available to help stabilize and scale your technology stack. Browse the service listings below to find the model that fits your operational needs.
      </p>
      <div class="ingress-actions">
        <a href="mailto:consulting@nolifeking85.tv?subject=Consulting%20Inquiry" class="btn-custom-cta">Get in Touch Directly</a>
      </div>
    </header>

<hr class="category-divider" />
{% for category in sorted_categories %}
      <section class="consulting-category" id="{{ category.id }}">
        <h2>{{ category.title }}</h2>
        <p class="category-description">{{ category.description }}</p>

        <div class="services-grid">
          {% assign category_services = all_services | where: "category", category.id %}
          {% for service in category_services %}
            <div class="service-card" id="{{ service.id }}">
              <div class="service-content">
                <h3>{{ service.title }}</h3>
                <p class="service-description">{{ service.description }}</p>
              </div>

              <div class="service-footer">
                <div class="service-pricing">
                  <span class="price-amount">{{ service.price }} SEK</span>
                  <span class="price-type">
                    {% if service.pricing == 'hourly' %}
                      / hr
                    {% else %}
                      fixed
                    {% endif %}
                  </span>
                </div>
                <a href="mailto:consulting@nolifeking85.tv?subject=Inquiry:%20{{ service.title | url_encode }}" class="btn-service-cta">Request Service</a>
              </div>
            </div>
          {% endfor %}
        </div>
      </section>
      {% unless forloop.last %}<hr class="category-divider" />{% endunless %}
    {% endfor %}
</div>
