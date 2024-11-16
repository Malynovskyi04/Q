<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Приглашение на свидание</title>
  <style>
    /* Основные стили */
    body {
      display: flex;
      align-items: center;
      justify-content: center;
      height: 100vh;
      font-family: Arial, sans-serif;
      margin: 0;
      background: radial-gradient(circle, #2a3a58, #1e2a3a); /* Светлое ночное небо с фиолетовым оттенком */
      color: #ffffff;
      overflow: hidden;
    }

    /* Полупрозрачный слой для улучшенной видимости */
    .overlay {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background-color: rgba(0, 0, 0, 0.5); /* Черный полупрозрачный слой */
      z-index: 1;
    }

    /* Центрирование контейнера */
    .container {
      width: 350px;
      height: 350px;
      text-align: center;
      padding: 30px;
      border: 3px solid #fff;
      border-radius: 15px;
      background-color: rgba(0, 0, 0, 0.7); /* Полупрозрачный фон */
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      z-index: 10;
    }

    /* Стили для кнопок */
    .button {
      padding: 10px 20px;
      margin: 10px;
      font-size: 16px;
      cursor: pointer;
      border: 1px solid #333;
      border-radius: 5px;
      background-color: #ffffff;
      color: #333;
    }

    /* Скрытие блока */
    .hidden {
      display: none;
    }

    /* Анимация для падающих фиолетовых сердечек */
    .heart {
      position: fixed;
      top: -50px;
      color: #9b59b6; /* Фиолетовый цвет */
      font-size: 24px;
      animation-name: fallHearts;
      animation-timing-function: linear;
      animation-iteration-count: infinite;
      opacity: 0.8;
      z-index: 2; /* Сердечки будут над снежинками */
    }

    /* Анимация падения сердечек */
    @keyframes fallHearts {
      to {
        transform: translateY(100vh);
      }
    }

    /* Стили для снежинок */
    .snowflake {
      position: fixed;
      top: -50px;
      color: #FFF;
      font-size: 24px;
      animation-name: fallSnow;
      animation-timing-function: linear;
      animation-iteration-count: infinite;
      opacity: 0.8;
      z-index: 1; /* Снежинки будут под сердечками */
    }

    /* Анимация падения снежинок */
    @keyframes fallSnow {
      to {
        transform: translateY(100vh);
      }
    }
  </style>
</head>
<body>

  <!-- Полупрозрачный слой поверх фона -->
  <div class="overlay"></div>

  <!-- Квадрат с вопросом и кнопками -->
  <div class="container" id="inviteBox">
    <p>Мы идем на свидание?</p>
    <button class="button" id="yesButton">Да</button>
    <button class="button" id="noButton">Нет</button>
    <button class="button" id="sickButton">Я заболела</button>
    <button class="button" id="examButton">У меня экзамены</button> 
 </div>

  <!-- Квадрат для выбора даты и времени -->
  <div class="container hidden" id="formBox">
    <p>Выбирай дату и время:</p>
    <label for="date">Дата:</label>
    <input type="date" id="date"><br><br>
    <label for="time">Время:</label>
    <input type="time" id="time"><br><br>
    <button class="button" id="sendButton">Отправить</button>
  </div>

  <script>
    // Получаем элементы кнопок и блоков
    const noButton = document.getElementById("noButton");
    const yesButton = document.getElementById("yesButton");
    const sickButton = document.getElementById("sickButton");
    const examButton = document.getElementById("examButton");
    const inviteBox = document.getElementById("inviteBox");
    const formBox = document.getElementById("formBox");
    const sendButton = document.getElementById("sendButton");

    // Функция для убегания кнопки от курсора
    function makeButtonMove(button) {
      button.addEventListener("mouseover", () => {
        const boxRect = inviteBox.getBoundingClientRect();
        const buttonWidth = button.clientWidth;
        const buttonHeight = button.clientHeight;
        
        // Случайные координаты для кнопки внутри контейнера
        const x = Math.random() * (boxRect.width - buttonWidth);
        const y = Math.random() * (boxRect.height - buttonHeight);
        
        button.style.position = "absolute";
        button.style.left = `${x}px`;
        button.style.top = `${y}px`;
      });
    }

    // Добавляем обработчик на все кнопки, чтобы они убегали от курсора, кроме кнопки "Да"
    makeButtonMove(noButton);
    makeButtonMove(sickButton);
    makeButtonMove(examButton);

    // Обработка нажатия на "Да" и запуск анимаций
    yesButton.addEventListener("click", () => {
      inviteBox.classList.add("hidden");   // Скрываем первоначальный блок
      formBox.classList.remove("hidden"); // Показываем блок с формой
      startHearts(); // Запускаем падение сердечек
      startSnowflakes(); // Запускаем падение снежинок
    });

    // Обработка нажатия на "Я заболела"
    sickButton.addEventListener("click", () => {
      alert("Желаю скорейшего выздоровления!");
    });

    // Обработка нажатия на "У меня экзамены"
    examButton.addEventListener("click", () => {
      alert("Желаю удачи на экзаменах!");
    });

    // Функция для добавления падающих сердечек
    function startHearts() {
      const heartSymbol = "💜";  // Используем только фиолетовое сердечко
      setInterval(() => {
        const heart = document.createElement("div");
        heart.classList.add("heart");
        heart.textContent = heartSymbol;
        heart.style.left = `${Math.random() * 100}vw`; // Случайная позиция по горизонтали
        heart.style.animationDuration = `${Math.random() * 3 + 2}s`; // Рандомная скорость падения
        heart.style.fontSize = `${Math.random() * 10 + 20}px`; // Разнообразие в размере сердечек
        heart.style.opacity = Math.random() * 0.5 + 0.3; // Разная прозрачность
        document.body.appendChild(heart);

        // Удаляем сердечко после анимации
        heart.addEventListener("animationend", () => {
          heart.remove();
        });
      }, 100); // Интервал создания сердечек
    }

    // Функция для добавления падающих снежинок
    function startSnowflakes() {
      const snowflakeSymbols = ["❄", "❅", "❆"];
      setInterval(() => {
        const snowflake = document.createElement("div");
        snowflake.classList.add("snowflake");
        snowflake.textContent = snowflakeSymbols[Math.floor(Math.random() * snowflakeSymbols.length)];
        snowflake.style.left = `${Math.random() * 100}vw`; // Случайная позиция по горизонтали
        snowflake.style.animationDuration = `${Math.random() * 3 + 2}s`; // Рандомная скорость падения
        snowflake.style.fontSize = `${Math.random() * 10 + 20}px`; // Разнообразие в размере снежинок
        snowflake.style.opacity = Math.random() * 0.5 + 0.3; // Разная прозрачность
        document.body.appendChild(snowflake);

        // Удаляем снежинку после анимации
        snowflake.addEventListener("animationend", () => {
          snowflake.remove();
        });
      }, 100); // Интервал создания снежинок
    }

    // Отправка данных формы на email
    sendButton.addEventListener("click", () => {
      const date = document.getElementById("date").value;
      const time = document.getElementById("time").value;

      if (!date || !time) {
        alert("Пожалуйста, выберите дату и время.");
        return;
      }

      const email = "kiril20112004@gmail.com";
      const subject = "Запрос на свидание";
      const body = `Выбрана дата свидания: ${date}, время: ${time}`;
      const mailtoLink = `mailto:${email}?subject=${encodeURIComponent(subject)}&body=${encodeURIComponent(body)}`;
      window.location.href = mailtoLink;
    });
  </script>
</body>
</html>
