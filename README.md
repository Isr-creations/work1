name: Create Torrent File

on:
  workflow_dispatch:
    inputs:
      link:
        description: "URL to download content"
        required: true

jobs:
  create-torrent:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout Repository
      uses: actions/checkout@v3

    - name: Set up Python
      uses: actions/setup-python@v4
      with:
        python-version: '3.x'

    - name: Install Python Dependencies
      run: |
        python -m pip install --upgrade pip
        pip install torrentool requests

    - name: Download File
      run: |
        mkdir -p download
        python - <<EOF
        import requests
        url = "${{ github.event.inputs.link }}"
        response = requests.get
