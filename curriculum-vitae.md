---
permalink: /curriculum-vitae/
title: Curriculum Vitae
nav_title: CV
layout: page
---

A thorough and easy-going all-in-all IT engineer, with over 20 years of experience in different fields across the jungle of IT. Skilled at solving complex problems, I develop my own tools when needed and continuously seek new challenges to learn from. My expertise spans programming, server maintenance, and database administration - identifying and resolving performance issues with ease. Whether it’s virtual or physical infrastructure, I’m at home managing Windows, Linux, and even MacOS environments. I thrive in diverse tech stacks. I take pride in well-organized data centres, efficient systems, and making IT work seamlessly.

## Skills

These are some of the skills that I currently have, among other things. (I'm by no means an expert at all of these things)

{% assign sorted_skills = site.data.cv.skills | sort: "order" %}

{% for category in sorted_skills %}

### {{ category.category }}
{% for skill in category.items %}- {{ skill }}
{% endfor %}

{% endfor %}

## Experience

{% assign sorted_experiences = site.data.cv.experience | sort: "order" %}

<table>
  <thead>
    <tr>
      <th>Period of Time</th>
      <th>Role</th>
    </tr>
  </thead>
  <tbody>
  {% for experience in sorted_experiences %}
    <tr>
      <td><b>{{ experience.period }}</b></td>
      <td>
        <b>
        {% if experience.link %}
        <a href="{{experience.link}}" target="_blank">
          {{ experience.company }}
        </a>
        {% else %}
        {{ experience.company }}
        {% endif %}
        </b><br />
        <i>{{ experience.role }}</i><br />
       {{ experience.description }}
      </td>
    </tr>
{% endfor %}
  </tbody>
</table>

## Education

{% assign sorted_education = site.data.cv.education | sort: "order" %}

<table>
  <thead>
    <tr>
      <th>Period of Time</th>
      <th>Role</th>
    </tr>
  </thead>
  <tbody>
    {% for education in sorted_education %}
    <tr>
      <td><b>{{ education.period }}</b></td>
      <td>
        <b>
        {{ education.company }}
        </b><br />
        <i>{{ education.title }}</i><br />
       {{ education.description }}
      </td>
    </tr>
{% endfor %}
  </tbody>
</table>

## Miscellaneous and Additions

### Languages

{% for language in site.data.cv.languages %}
- {{ language.name }} - {{ language.level_text }} ({{ language.level }})
{% endfor %}

### References

- Available upon request

### Additional Info

**Nov 2023** - NIC Cloud Connect

Participated in the Nordic Infrastructure Conference (NIC Cloud Connect) in Oslo. Attended multiple talks and courses about managing Windows through Intune, among other topics.

## More contact info and other links

- GitHub: <https://github.com/itssimple>
- X: <https://x.com/NoLifeKing85>
- Instagram: <https://www.instagram.com/NoLifeKing85/>
- LinkedIn: <https://www.linkedin.com/in/nolifeking/>
- Smule: <https://www.smule.com/NoLifeKing>
