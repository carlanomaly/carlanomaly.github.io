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

        ### Contributors

        <div class="contributor-grid">

        <div class="contributor-card">
        <div class="contributor-avatar"></div>
        <div class="contributor-name">A. Anonymous</div>
        <div class="contributor-affiliation">University of Somewhere</div>
        </div>

        <div class="contributor-card">
        <div class="contributor-avatar"></div>
        <div class="contributor-name">A. Anonymous</div>
        <div class="contributor-affiliation">Institute of Technology</div>
        </div>

        <div class="contributor-card">
        <div class="contributor-avatar"></div>
        <div class="contributor-name">A. Anonymous</div>
        <div class="contributor-affiliation">Research Center for Autonomy</div>
        </div>

        <div class="contributor-card">
        <div class="contributor-avatar"></div>
        <div class="contributor-name">A. Anonymous</div>
        <div class="contributor-affiliation">Technical University of Somewhere</div>
        </div>

        <div class="contributor-card">
        <div class="contributor-avatar"></div>
        <div class="contributor-name">A. Anonymous</div>
        <div class="contributor-affiliation">School of Engineering</div>
        </div>

        <div class="contributor-card">
        <div class="contributor-avatar"></div>
        <div class="contributor-name">A. Anonymous</div>
        <div class="contributor-affiliation">Lab for Autonomous Systems</div>
        </div>

        </div>


  - block: markdown
    content:
      title: FAQ
      text: |
        <div class="faq">

        <details>
        <summary>Why did you not use the new version of CARLA?</summary>
        <p>Because it only supports two maps.</p>
        </details>

        <details>
        <summary>Did you generate this with the vanilla version of CARLA?</summary>
        <p>No, we used a version with several patches because the vanilla version does not have all of the features we need. The patching process is described in the documentation of CarlaGen.</p>
        </details>

        <details>
        <summary>Why did you use the feather format?</summary>
        <p>We found that feather files are significantly smaller and faster to load than CSV files or binary dumps (and support compression).</p>
        </details>

        </div>
---
