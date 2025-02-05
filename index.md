---
title: Instruções para o exercício
permalink: index.html
layout: home
---

# Exercícios

Esta página lista os exercícios associados ao conteúdo de habilidades da Microsoft no [Microsoft Learn](https://learn.microsoft.com)

{% assign labs = site.pages | where_exp:"page", "page.url contains '/Instructions/Labs'" %} {% for activity in labs  %}
- [{{ activity.lab.title }}]({{ site.github.url }}{{ activity.url }}) {% endfor %}

