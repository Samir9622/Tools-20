<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Tool-20 | Image Compression Tool</title>
  <meta name="google-adsense-account" content="ca-am-pub-8773480799818158">
  <style>
    body { font-family: Arial, sans-serif; margin: 0; padding: 0; background: #fff; }
    header { background: #333; color: #fff; padding: 15px; position: relative; }
    .back-button { position: absolute; left: 15px; top: 15px; color: white; text-decoration: none; font-weight: bold; }
    .home-container { margin-top: 100px; text-align: center; }
    .tool-button { padding: 12px 24px; background-color: #008CBA; color: white; text-decoration: none; border-radius: 5px; }
    .upload-area { border: 2px dashed #999; padding: 40px; margin: 30px; background: #f9f9f9; text-align: center; cursor: pointer; }
    #file-input { display: none; }
    .settings { margin: 20px; text-align: center; }
    .preview { display: flex; flex-wrap: wrap; justify-content: center; gap: 15px; }
    .preview img { max-width: 200px; max-height: 200px; object-fit: contain; border: 1px solid #ccc; padding: 5px; }
    .actions { margin: 20px; text-align: center; }
  </style>
  <script async src="https://pagead2.googlesyndication.com/pagead/js/adsbygoogle.js?client=-ca-pub-8773480799818158crossorigin="anonymous"></script>
</head>
<body>
  <header>
    <a href="../" class="back-button">&larr; Back</a>
    <h1 style="text-align:center;">Image Compression Tool</h1>
  </header>
  <!-- Ad Unit Top -->
  <ins class="adsbygoogle"
       style="display:block; text-align:center;"
       data-ad-client="9055111364"
       data-ad-slot="8773480799818158"
       data-ad-format="auto"
       data-full-width-responsive="true"></ins>
  <script>(adsbygoogle = window.adsbygoogle || []).push({});</script>

  <div class="upload-area" onclick="document.getElementById('file-input').click()">
    Drag & Drop Images Here or Click to Upload
    <input type="file" id="file-input" multiple accept="image/*">
  </div>
  <div class="settings">
    <label for="quality">Compression Quality: <span id="quality-value">80%</span></label>
    <input type="range" id="quality" min="10" max="100" value="80">
    <label><input type="checkbox" id="webp"> Convert to WebP</label>
  </div>
  <div class="preview" id="preview"></div>
  <div class="actions">
    <button onclick="downloadAll()">Download All</button>
  </div>

  <!-- Ad Unit Bottom -->
  <ins class="adsbygoogle"
       style="display:block; text-align:center; margin: 20px auto;"
       data-ad-client="ca-app-pub-9354903383"
       data-ad-slot="9055111364"
       data-ad-format="auto"
       data-full-width-responsive="true"></ins>
  <script>(adsbygoogle = window.adsbygoogle || []).push({});</script>

  <script>
    const fileInput = document.getElementById('file-input');
    const preview = document.getElementById('preview');
    const qualityInput = document.getElementById('quality');
    const qualityValue = document.getElementById('quality-value');
    const convertWebP = document.getElementById('webp');

    qualityInput.addEventListener('input', () => {
      qualityValue.textContent = qualityInput.value + '%';
    });

    fileInput.addEventListener('change', handleFiles);

    function handleFiles() {
      preview.innerHTML = '';
      const files = fileInput.files;
      for (let file of files) {
        const reader = new FileReader();
        reader.onload = e => {
          const img = new Image();
          img.onload = () => compressImage(img, file.name);
          img.src = e.target.result;
        };
        reader.readAsDataURL(file);
      }
    }

    function compressImage(img, name) {
      const canvas = document.createElement('canvas');
      const ctx = canvas.getContext('2d');
      canvas.width = img.width;
      canvas.height = img.height;
      ctx.drawImage(img, 0, 0);
      let type = convertWebP.checked ? 'image/webp' : 'image/jpeg';
      canvas.toBlob(blob => {
        const url = URL.createObjectURL(blob);
        const a = document.createElement('a');
        a.href = url;
        const extension = type === 'image/webp' ? '.webp' : '.jpg';
        a.download = name.replace(/\.[^/.]+$/, "") + extension;
        const imgEl = new Image();
        imgEl.src = url;
        preview.appendChild(imgEl);
        a.style.display = 'none';
        document.body.appendChild(a);
        a.dataset.downloadurl = [type, a.download, a.href].join(':');
      }, type, qualityInput.value / 100);
    }

    function downloadAll() {
      const links = document.querySelectorAll('a[data-downloadurl]');
      links.forEach(link => link.click());
    }
  </script>
</body>
</html>
