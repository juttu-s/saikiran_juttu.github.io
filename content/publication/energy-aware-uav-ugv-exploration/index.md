---
title: 'Energy-Aware Collaborative Exploration for a UAV–UGV Team'

# Authors
# If you created a profile for a user (e.g. the default `admin` user), write the username (folder name) here
# and it will be replaced with their full name and linked to their profile.
authors:
  - Cahit Ikbal Er
  - admin
  - Yasin Yazıcıoğlu

date: '2026-03-01T00:00:00Z'
doi: ''

# Schedule page publish date (NOT publication's date).
publishDate: '2026-03-01T00:00:00Z'

# Publication type.
# Accepts a single type but formatted as a YAML list (for Hugo requirements).
# Enter a publication type from the CSL standard.
publication_types: ['paper-conference']

# Publication name and optional abbreviated publication name.
publication: 'Submitted to *IEEE/RSJ International Conference on Intelligent Robots and Systems (IROS)*, 2026'
publication_short: 'Submitted to *IROS 2026*'

abstract: We present an energy-aware collaborative exploration framework for a UAV–UGV team operating in unknown environments, where the UAV's energy constraint is modeled as a maximum flight-time limit. The UAV executes a sequence of energy-bounded exploration tours, while the UGV simultaneously explores on the ground and serves as a mobile charging station. Rendezvous is enforced under a shared time budget so that the vehicles meet at the end of each tour before the UAV reaches its flight-time limit. We construct a sparsely coupled air–ground roadmap using a density-aware layered probabilistic roadmap (PRM) and formulate tour selection over the roadmap as coupled orienteering problems (OPs) to maximize information gain subject to the rendezvous constraint. The resulting tours are constructed over collision-validated roadmap edges. We validate our method through simulation studies, benchmark comparisons, and real-world experiments.

# Summary. An optional shortened abstract.
summary: A density-aware layered PRM and coupled orienteering formulation for energy-bounded UAV–UGV collaborative exploration with rendezvous constraints, validated in simulation and real-world experiments.

tags:
  - Multi-Robot Planning
  - Collaborative Exploration
  - UAV-UGV
  - Orienteering Problem
  - PRM

# Display this page in the Featured widget?
featured: true

# Custom links (uncomment lines below)
# links:
# - name: Custom Link
#   url: http://example.org

url_pdf: 'https://arxiv.org/abs/2603.22507'
url_code: 'https://github.com/juttu-s/uav-ugv-collaborative-exploration'
url_dataset: ''
url_poster: ''
url_project: '/saikiran_juttu.github.io/details/grad-research-assistant/'
url_slides: ''
url_source: ''
url_video: ''

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
image:
  caption: ''
  focal_point: ''
  preview_only: false

# Associated Projects (optional).
projects: []
---

This work was submitted to **IEEE/RSJ IROS 2026**. It proposes a **density-aware layered PRM** and a **coupled orienteering formulation** for **energy-bounded UAV–UGV collaborative exploration** with rendezvous constraints, validated through both simulation benchmarks and real-world experiments.
