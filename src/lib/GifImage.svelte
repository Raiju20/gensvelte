<script>
    export let src = ''; // URL изображения
    export let alt = ''; // Альтернативный текст
</script>

<img src={src} alt={alt} class="gif-image" />

<style>
    .gif-image {
        max-width: 100%; /* Ограничиваем максимальную ширину изображения */
        height: auto; /* Сохраняем пропорции изображения */
        margin-bottom: 20px; /* Отступ снизу для кнопок */
    }
</style>