<script>
    import Counter from './lib/Counter.svelte'; // Импортируем компонент Counter
    import GifImage from './lib/GifImage.svelte'; // Импортируем новый компонент

    const colors = ['red', 'green', 'blue'];
    let currentColorIndex = 0;
    let intervalId;
    let colorChangeCount = 0; // Счетчик изменений цвета
    let currentClass = ''; // Текущий класс для фона

    const setColor = (color) => {
        currentClass = color;
        clearInterval(intervalId); // Останавливаем автоцикл
        colorChangeCount = 0; // Сбрасываем счетчик при ручном выборе цвета
    };

    const startCycle = () => {
        clearInterval(intervalId);
        intervalId = setInterval(() => {
            currentClass = colors[currentColorIndex];
            currentColorIndex = (currentColorIndex + 1) % colors.length;
            colorChangeCount++; // Увеличиваем счетчик при каждом изменении цвета
        }, 200);
    };
</script>

<main class={currentClass}>
    <GifImage src="https://media.tenor.com/ADP4nszb5AcAAAAi/shigure-ui-dance.gif" alt="Dancing Shigure UI" />
    <div class="hmm">
        <div class="button-container">
            <button on:click={() => setColor('red')}>Красный</button>
            <button on:click={() => setColor('green')}>Зеленый</button>
            <button on:click={() => setColor('blue')}>Синий</button>
            <button on:click={startCycle}>Автоцикл цветов</button>
        </div>
        <Counter count={colorChangeCount} /> <!-- Отображаем счетчик -->
    </div>
</main>

<style>
    main {
        position: absolute; /* Занимаем всю площадь экрана */
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        transition: background-color 0.3s;
    }

    .red {
        background-color: #e74c3c; /* Красный цвет */
    }

    .green {
        background-color: #2ecc71; /* Зеленый цвет */
    }

    .blue {
        background-color: #3498db; /* Синий цвет */
    }

    .hmm {
        display: flex;
        gap: 10px;
        flex-direction: column;
        flex-wrap: nowrap;
    }

    .button-container {
        display: flex; /* Горизонтальное расположение кнопок */
        gap: 10px; /* Отступ между кнопками */
        margin-top: 20px; /* Отступ сверху для кнопок */
    }

    button {
        padding: 15px 30px; /* Увеличенные отступы для кнопок */
        font-size: 18px; /* Увеличенный шрифт */
        cursor: pointer;
        border: none; /* Убираем рамку */
        border-radius: 5px; /* Закругляем углы */
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2); /* Объемный эффект */
        transition: all 0.3s; /* Плавный переход для эффектов */
    }

    button:hover {
        box-shadow: 0 6px 12px rgba(0, 0, 0, 0.3); /* Увеличиваем тень при наведении */
        transform: translateY(-2px); /* Поднимаем кнопку при наведении */
    }
</style>