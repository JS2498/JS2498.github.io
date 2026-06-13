---
layout: page
title: projects
permalink: /projects/
description:
nav: true
nav_order: 3
---

<div class="publications">
  <ul class="card-text font-weight-light list-group list-group-flush">
    {% assign projects = site.data.resume.projects | sort: 'startDate' | reverse %}
    {% for project in projects %}
      <li class="list-group-item" style="border-left: none; border-right: none;">
        <div class="row">
          <div class="col-xs-2 cl-sm-2 col-md-2 text-center date-column">
            {% assign year = project.startDate | split: '-' | first %}
            <span class="badge font-weight-bold danger-color-dark text-uppercase align-middle" style="min-width: 75px">{{ year }}</span>
          </div>
          <div class="col-xs-10 cl-sm-10 col-md-10 mt-2 mt-md-0">
            <h6 class="title font-weight-bold ml-1 ml-md-4">
              {% if project.url %}
                <a href="{{ project.url }}" target="_blank" rel="noopener noreferrer">{{ project.name }}</a>
              {% else %}
                {{ project.name }}
              {% endif %}
            </h6>
            <p class="ml-1 ml-md-4" style="font-size: 0.95rem; font-style: italic">{{ project.summary }}</p>
          </div>
        </div>
      </li>
    {% endfor %}
  </ul>
</div>
