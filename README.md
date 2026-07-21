name: Generate Metrics Dashboard

on:
  workflow_dispatch:
  schedule:
    - cron: "0 0 * * *"
  push:
    branches: [main]

jobs:
  build-metrics:
    runs-on: ubuntu-latest
    permissions:
      contents: write
    steps:
      - uses: lowlighter/metrics@latest
        with:
          token: ${{ secrets.METRICS_TOKEN }}
          user: amanrai0067-maker
          filename: metrics.classic.svg
          template: classic
          base: header, activity, community, repositories, metadata
          plugin_languages: yes
          plugin_languages_analysis_timeout: 15
          plugin_languages_categories: markup, programming
          plugin_languages_recent_categories: markup, programming
          plugin_lines: yes
          plugin_habits: yes
          plugin_habits_charts_type: bar
          plugin_achievements: yes
          plugin_achievements_display: compact
          plugin_isocalendar: yes
          plugin_isocalendar_duration: half-year

      - uses: lowlighter/metrics@latest
        with:
          token: ${{ secrets.METRICS_TOKEN }}
          user: amanrai0067-maker
          filename: metrics.isocalendar.svg
          template: classic
          base: ""
          plugin_isocalendar: yes
          plugin_isocalendar_duration: full-year
