# proekt
<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Определение площади многоугольника</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      text-align: center;
      background: #f5f5f5;
      padding: 20px;
    }

    h1 {
      color: #333;
    }

    input[type="file"] {
      margin-top: 10px;
    }

    canvas {
      margin-top: 20px;
      border: 1px solid #ccc;
      max-width: 90%;
    }

    #output {
      margin-top: 20px;
      font-size: 1.2em;
      background: white;
      padding: 10px;
      border-radius: 6px;
      display: inline-block;
      max-width: 90%;
    }

    button {
      margin-top: 10px;
      padding: 8px 16px;
      background-color: #4CAF50;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }

    button:hover {
      background-color: #45a049;
    }
  </style>
</head>
<body>
  <h1>Определение площади многоугольника по изображению</h1>

  <p>Загрузите изображение многоугольника:</p>
  <input type="file" id="imageInput" accept="image/*">

  <canvas id="canvas"></canvas>

  <div id="output"></div>

  <script>
    const imageInput = document.getElementById('imageInput');
    const canvas = document.getElementById('canvas');
    const ctx = canvas.getContext('2d');
    const output = document.getElementById('output');

    imageInput.addEventListener('change', async (e) => {
      const file = e.target.files[0];
      if (!file) return;

      const img = new Image();
      img.src = URL.createObjectURL(file);
      img.onload = () => {
        canvas.width = img.width;
        canvas.height = img.height;
        ctx.drawImage(img, 0, 0);

        output.innerHTML = `
          <p><b>Фото загружено.</b></p>
          <p>Для вычисления площади многоугольника введите количество сторон:</p>
          <input type="number" id="sidesInput" min="3" max="10" value="4">
          <button id="calcButton">Показать формулу</button>
        `;

        document.getElementById('calcButton').addEventListener('click', showFormula);
      };
    });

    function showFormula() {
      const n = parseInt(document.getElementById('sidesInput').value);
      let formula = '';

      switch (n) {
        case 3:
          formula = 'Площадь треугольника: S = (1/2) * a * h или через стороны: √(p(p−a)(p−b)(p−c))';
          break;
        case 4:
          formula = 'Площадь прямоугольника: S = a * b или для квадрата: S = a²';
          break;
        case 5:
          formula = 'Площадь правильного пятиугольника: S = (1/4) * √(5(5 + 2√5)) * a²';
          break;
        case 6:
          formula = 'Площадь правильного шестиугольника: S = (3√3 / 2) * a²';
          break;
        default:
          formula = 'Площадь правильного n-угольника: S = (n * a²) / (4 * tan(π / n))';
      }

      output.innerHTML += `<p><b>${formula}</b></p>`;
    }
  </script>
</body>
</html>
