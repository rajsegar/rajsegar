name: Generate Snake Animation

on:
  schedule:
    - cron: "0 0 * * *"     # Runs every day at midnight
  workflow_dispatch:        # Allows manual trigger
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v3

      - name: Generate Snake SVG
        id: snake
        uses: Platane/snk@v3
        with:
          github_user_name: rajsegar
          outputs: dist/snake.svg

      - name: Push Snake to Output Branch
        uses: crazy-max/ghaction-github-pages@v4
        with:
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
