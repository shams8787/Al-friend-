<!-- index.html -->
<!DOCTYPE html>
<html>
<head>
  <title>تحويل الصور إلى فيديو</title>
</head>
<body>
  <h1>ارفع صورك لإنشاء فيديو 🎥</h1>
  <form id="uploadForm" enctype="multipart/form-data">
    <input type="file" name="images" multiple accept="image/*" required><br>
    <label>مدة عرض كل صورة (بالثواني):</label>
    <input type="number" name="duration" value="2"><br>
    <label>موسيقى خلفية (اختياري):</label>
    <input type="file" name="music" accept="audio/*"><br>
    <button type="submit">إنشاء الفيديو</button>
  </form>
  <div id="videoResult"></div>

  <script>
    const form = document.getElementById("uploadForm");
    form.onsubmit = async (e) => {
      e.preventDefault();
      const formData = new FormData(form);
      const res = await fetch("/create-video", {
        method: "POST",
        body: formData,
      });
      const blob = await res.blob();
      const url = URL.createObjectURL(blob);
      document.getElementById("videoResult").innerHTML = `<video controls src="${url}"></video>`;
    };
  </script>
</body>
</html>
