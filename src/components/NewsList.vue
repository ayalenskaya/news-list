<template>
    <div>
        <header>
            <img class="header-logo" src="/header.svg" alt="Лого">
            <div class="header-img-container">
                <img src="/img.png" alt="Текст на изображении">
                <p class="header-text">Новости</p>
            </div>
        </header>
        <div class="news-row">
            <news-item v-for="item in newsItems" :key="item.code" :item="item" />

        </div>
        <div class="load-more-news">
            <button v-if="showLoadMoreButton" @click="loadMoreNews">Загрузить еще</button>
        </div>
        <footer>
            <div class="footer-logo">
                <img src="/header.svg" alt="Лого">
                <p>
                    © alpha, 2023
                </p>
            </div>
        </footer>
    </div>
</template>
  
<script>
import { ref, onMounted } from 'vue';
import NewsItem from '@/components/NewsItem.vue';

export default {
    name: 'NewsList',
    components: {
        NewsItem
    },
    setup() {
        const newsItems = ref([]);
        const currentPage = ref(1);
        const showLoadMoreButton = ref(false);

        const loadNews = async () => {
            try {
                const response = await fetch('http://flems.github.io/test/api/news/' + currentPage.value + '/');
                const data = await response.json();

                newsItems.value = newsItems.value.concat(data.items);

                showLoadMoreButton.value = data.nav.current < data.nav.total;
            } catch (error) {
                alert('Извините, произошла какая-то ошибка. попробуйте перезагрузить страницу')
            }
        };

        const loadMoreNews = () => {
            currentPage.value++;
            loadNews();
        };
        onMounted(() => {
            loadNews();
        });

        return {
            newsItems,
            showLoadMoreButton,
            loadMoreNews
        };
    },
};
</script>
  
<style scoped>
.header-logo {
    margin: 40px 0 40px 100px;
}

.footer-text {
    margin-left: 40px;
}

.header-img-container {
    position: relative;
}

.header-img-container img {
    width: 100%;
}

.header-text {
    position: absolute;
    top: 50%;
    left: 12%;
    transform: translate(-50%, -50%);
    font-size: 40px;
    font-weight: 700;
    color: #17171A;
}

.news-row {
    display: flex;
    flex-wrap: wrap;
    gap: 50px;
    margin: 50px 0;
    justify-content: center;
}

.load-more-news {
    display: flex;
    justify-content: center;
}

.load-more-news button {
    padding: 16px 32px;
    color: #002DBF;
    border: 1px solid #0F62FE;
    background-color: #fff;
    border-radius: 16px;
    font-size: 20px;
    line-height: 24px;
    font-weight: 600;
}

footer {
    background-color: #F0F6FE;
}

.footer-logo {
    margin-top: 40px;
    padding: 100px;
}

.footer-logo p {
    margin: 0;
    color: #81899D;
    font-size: 16px;
}

@media (max-width: 1366px) {
    .header-text {
        top: 20%;
        left: 23%;
    }

    .item-name {
        font-size: 16px;
    }

    .item-description {
        font-size: 14px;
    }
}

@media (max-width: 1024px) {
    .news-item {
        width: 100%;
    }
}
</style>