<template>
    <div class="book-card" :class="{ completed: book.completed }">
        <div class="book-info">
            <h3>
                {{ book.title }}
                <span v-if="book.favorite" class="favorite-badge">★</span>
            </h3>
            <p class="author">{{ book.author }}</p>
            <span class="genre">{{ book.genre }}</span>
        </div>

        <div class="book-actions">
            <button @click="emit('toggle-favorite')" class="btn-favorite" :class="{ favorite: book.favorite }"
                :title="book.favorite ? 'Убрать из избранного' : 'Добавить в избранное'">
                {{ book.favorite ? '★' : '☆' }}
            </button>

            <div v-if="book.completed" class="rating">
                <span v-for="star in 5" :key="star" @click="emit('rate', star)" class="star">
                    {{ star <= book.rating ? '★' : '☆' }} </span>
            </div>

            <button @click="emit('toggle')" class="btn" :class="book.completed ? 'btn-secondary' : 'btn-primary'">
                {{ book.completed ? 'Не прочитана' : 'Прочитана' }}
            </button>

            <button @click="emit('delete')" class="btn btn-danger">
                Удалить
            </button>
        </div>
    </div>
</template>

<script setup>
const props = defineProps(['book'])
const emit = defineEmits(['toggle', 'delete', 'rate', 'toggle-favorite'])
</script>

<style scoped>
.book-card {
    background: white;
    border-radius: 8px;
    padding: 16px;
    margin-bottom: 12px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    display: flex;
    justify-content: space-between;
    align-items: center;
    transition: all 0.3s;
}

.book-card.completed {
    background: #f0f7f0;
    opacity: 0.9;
}

.book-info {
    flex: 1;
}

.book-info h3 {
    margin-bottom: 4px;
    color: #333;
    display: flex;
    align-items: center;
    gap: 8px;
}

.favorite-badge {
    font-size: 1.2em;
    cursor: default;
}

.author {
    color: #666;
    font-size: 0.9em;
    margin-bottom: 4px;
}

.genre {
    background: #e0e0e0;
    padding: 2px 8px;
    border-radius: 4px;
    font-size: 0.8em;
    display: inline-block;
}

.book-actions {
    display: flex;
    gap: 8px;
    align-items: center;
}

.btn-favorite {
    background: none;
    border: none;
    font-size: 24px;
    cursor: pointer;
    transition: transform 0.2s;
    padding: 4px;
}

.btn-favorite:hover {
    transform: scale(1.2);
}

.btn-favorite.favorite {
    color: gold;
}

.rating {
    display: flex;
    gap: 2px;
}

.rating span {
    font-size: 20px;
    cursor: pointer;
    color: gold;
}

.rating span:hover {
    transform: scale(1.2);
}

.btn {
    padding: 8px 12px;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    font-size: 0.9em;
    transition: background 0.3s;
}

.btn-primary {
    background: #90539c;
    color: white;
}

.btn-primary:hover {
    background: #72477a;
}

.btn-secondary {
    background: #f99d2d;
    color: white;
}

.btn-secondary:hover {
    background: #b86f16;
}

.btn-danger {
    background: #e25e54;
    color: white;
}

.btn-danger:hover {
    background: #da190b;
}
</style>