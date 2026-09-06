---
layout: page
title: Projects
permalink: /projects/
description: A showcase of personal, research, and engineering projects.
nav: true
nav_order: 3
display_categories: [ai-ml, systems, software-engineering, knowledge-engineering]
horizontal: false
---

<div class="projects">

  <!-- 1. AI & Machine Learning -->
  <h2 class="category mt-4 mb-3">Artificial Intelligence & Machine Learning</h2>
  {% assign ai_projects = site.projects | where: "category", "ai-ml" | sort: "importance" %}
  <div class="container">
    {% for project in ai_projects %}
      {% include projects.liquid %}
    {% endfor %}
  </div>

  <!-- 2. Knowledge Engineering & Semantics -->
  <h2 class="category mt-5 mb-3">Knowledge Engineering & Semantics</h2>
  {% assign ke_projects = site.projects | where: "category", "knowledge-engineering" | sort: "importance" %}
  <div class="container">
    {% for project in ke_projects %}
      {% include projects.liquid %}
    {% endfor %}
  </div>

  <!-- 3. Software Engineering & Backend -->
  <h2 class="category mt-5 mb-3">Software Engineering & Backend</h2>
  {% assign se_projects = site.projects | where: "category", "software-engineering" | sort: "importance" %}
  <div class="container">
    {% for project in se_projects %}
      {% include projects.liquid %}
    {% endfor %}
  </div>

  <!-- 4. Low-Level Systems & Hardware -->
  <h2 class="category mt-5 mb-3">Low-Level Systems & Hardware</h2>
  {% assign sys_projects = site.projects | where: "category", "systems" | sort: "importance" %}
  <div class="container">
    {% for project in sys_projects %}
      {% include projects.liquid %}
    {% endfor %}
  </div>

</div>