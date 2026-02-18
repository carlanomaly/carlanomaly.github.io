---
title: ''
summary: ''
date: 2025-01-01
type: landing

design:
  spacing: '4rem'

sections:
  - block: markdown
    content:
      title: ''
      text: |
        {{< video-hero src="/video/carlagen-demo.mp4" title="CarlAnomaly" subtitle="A CARLA-based Dataset for Multi-Modal Anomaly Detection<br>in Autonomous Driving Scenarios" >}}
    design:
      spacing:
        padding: ['0', '0', '0', '0']

  - block: markdown
    content:
      title: ''
      text: |
        {{< feature-cards >}}

  - block: markdown
    content:
      title: Paper
      text: |
        ```bibtex
        @inproceedings{


        }
        ```

  - block: markdown
    content:
      title: Example Anomalies
      text: |
        CarlAnomaly features a wide range of anomalies.

        Overall, there are x different types of anomalies:

        - Randomly appearing and disappearing unknown objects
        - Traffic Lights Malfunctioning in several ways (off, blinking single color, switching to fast)
        - Instantaneous weather changes
        - Spawning or vanishing objects

        {{< anomaly-gallery >}}
---
