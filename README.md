# Dilaso-Spiral-Wave-Force_1
.github/workflows/latex.yml

paper_v1.0.pdf   → initial draft
paper_v1.1.pdf   → minor revision
paper_v1.2.pdf   → stability analysis added
paper_v2.0.pdf   → major theoretical update
name: Build and Commit PDF

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v3

      - name: Compile LaTeX
        uses: xu-cheng/latex-action@v2
        with:
          root_file: main.tex

      - name: Commit PDF to repository
        run: |
          git config --global user.name "github-actions"
          git config --global user.email "actions@github.com"
          git add main.pdf
          git commit -m "Auto-build: Update PDF"
          git push
Setup automatic PDF build and commit
main.tex
main.pdf   ← auto-generated
references.bib
.github/
   workflows/
      latex.yml
      

name: Build and Commit Versioned PDF

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v3

      - name: Compile LaTeX
        uses: xu-cheng/latex-action@v2
        with:
          root_file: main.tex

      - name: Rename PDF
        run: mv main.pdf paper_v1.2.pdf

      - name: Commit PDF to repository
        run: |
          git config --global user.name "github-actions"
          git config --global user.email "actions@github.com"
          git add paper_v1.2.pdf
          git commit -m "Auto-build: Update paper_v1.2.pdf"
          git push
