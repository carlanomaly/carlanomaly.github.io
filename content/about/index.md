---
title: About
date: 2025-01-01
type: landing

design:
  spacing: '3rem'

sections:
  - block: markdown
    content:
      title: About the Project
      text: |
        <!-- Placeholder: insert project narrative, contributors, and provenance -->

  - block: markdown
    content:
      title: FAQ
      text: |
        <div class="faq">

        <details>
        <summary>Why did you not use the new version of CARLA?</summary>
        Because it only supports two maps.
        </details>

        <details>
        <summary>Did you generate this with the vanilla version of CARLA?</summary>
        No, we used a version with several patches because the vanilla version does not have all of the features we need. The patching process is described in the documentation of CarlaGen.
        </details>

        <details>
        <summary>Why did you use the feather format?</summary>
        We found that feather files are significantly smaller and faster to load than CSV files or binary dumps (and support compression).
        </details>

        </div>
---
