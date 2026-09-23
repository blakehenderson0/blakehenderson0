![header](https://capsule-render.vercel.app/api?type=waving&color=gradient&height=200&text=Hello%20World&animation=fadeIn)
![Typing SVG](https://readme-typing-svg.demolab.com?font=Fira+Code&lines=Software+Engineer;Open+Source+Enthusiast;Always+learning)
![Stats](https://github-readme-stats.vercel.app/api?username=blakehenderson0&show_icons=true&theme=tokyonight)

name: Update Profile
on:
  schedule:
    - cron: '0 0 * * *'
  workflow_dispatch:

jobs:
  update:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Generate metrics
        uses: lowlighter/metrics@latest
        with:
          token: ${{ secrets.METRICS_TOKEN }}
          filename: metrics.svg
          base: header, activity, community, repositories
      - name: Commit changes
        run: |
          git config user.name "github-actions[bot]"
          git config user.email "github-actions[bot]@users.noreply.github.com"
          git add metrics.svg
          git diff --cached --quiet || git commit -m "chore: update metrics"
          git push
