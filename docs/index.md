---
# https://vitepress.dev/reference/default-theme-home-page
layout: home

hero:
  name: "XOMDA"
  text: "Tools for Data Abstraction"
  tagline: Don't write it. Generate it!
  image: "./logo.png"
  actions:
    - theme: brand
      text: Get started
      link: /getting-started/the-object-model
    - theme: alt
      text: Documentation
      link: /intro/what-is-xomda
#    - theme: sponsor
#      text: Become a sponsor
#      link: https://www.patreon.com/JorisAerts

features:
  - title: CSV Model
    details: Define your object model in CSV format.
  - title: Code Generation
    details: Parse the object model CSV into (a custom) AST and generate code from it.
  - title: Extensible
    details: Customise the way models are parsed and how code is generated.
  - title: Gradle Integration
    details: Easily integrate the whole process into your gradle build.
---

