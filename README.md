# github-action-visualize-gcb-graph

A github action that creates image files of a graph of cloudbuild.yaml jobs with https://github.com/RyanSiu1995/gcb-visualizer .

The created image files can be used in later steps of the github action, for example, commit to the repository via https://github.com/EndBug/add-and-commit ,
or store as build artifacts via https://github.com/actions/upload-artifact .

## Sample usage

```.github/workflows/commit-visualized-gcb-graph.yaml
name: Visualize cloudbuild job graph and commit
on: push

env:
  SEARCH_DIRECTORIES: sample
  FILENAME_FIND_PATTERN: 'cloudbuild.*.yaml'

jobs:
  format:
    runs-on: ubuntu-20.04
    name: Visualize cloudbuild job graph and commit
    steps:
      - name: checkout
        uses: actions/checkout@v2.4.0

      - name: Create png image for each cloudbuild.yaml
        uses: gecko655/github-action-visualize-gcb-graph@v0.0.3
        with:
          gcb-visualizer-version: v1.0.1
          search-directories: '${{ env.SEARCH_DIRECTORIES }}'
          filename-find-pattern: '${{ env.FILENAME_FIND_PATTERN }}'
          output-directory-relative-path: images
          output-filetype: png

      - name: commit and push
        uses: EndBug/add-and-commit@v7.4.0
        with:
          message: "Visualize cloudbuild jobs by GitHub Action"
          committer_name: "github-actions[bot]"
          committer_email: "41898282+github-actions[bot]@users.noreply.github.com"
          push: true
```

## Demo action and commit

https://github.com/gecko655/github-action-visualize-gcb-graph/runs/5087550688?check_suite_focus=true

https://github.com/gecko655/github-action-visualize-gcb-graph/commit/5cf81104e3ebb34920fd803671934fba142bcd46
