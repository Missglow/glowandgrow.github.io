name: Deploy Website via GitHub Pages

on:
  push:
    branches:
      - main

jobs:
  build-deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Setup Pages
        uses: actions/configure-pages@v3

      - name: Create index.html
        run: |
          mkdir -p $GITHUB_WORKSPACE/www
          cat > $GITHUB_WORKSPACE/www/index.html <<EOF
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Glow & Grow 💖</title>
  <style>
    body {
      margin: 0;
      font-family: Arial, sans-serif;
      background: linear-gradient(to bottom right, #ffe6f0, #f0f8ff);
      color: #333;
      text-align: center;
      padding: 40px;
    }
    h1 {
      color: #e91e63;
      font-size: 2.5rem;
    }
    p {
      font-size: 1.2rem;
      margin-top: 20px;
    }
    .quote {
      font-style: italic;
      margin-top: 40px;
      color: #7a004d;
    }
    img {
      margin-top: 30px;
      border-radius: 10px;
      max-width: 100%;
    }
  </style>
</head>
<body>
  <h1>Glow & Grow 💖</h1>
  <p>Your daily dose of fashion, food & positivity</p>

  <div class="quote">
    “You are allowed to be a masterpiece AND a work in progress.” – Sophia Amoruso
  </div>

  <img src="https://placehold.co/600x300/fad0c4/ffffff?text=Girly+Vibes" alt="Feel Good Vibes">
</body>
</html>
EOF

      - name: Upload artifact
        uses: actions/upload-pages-artifact@v2
        with:
          path: $GITHUB_WORKSPACE/www

      - name: Deploy to GitHub Pages
        uses: actions/deploy-pages@v2
