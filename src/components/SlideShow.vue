<template>
  <div class="slideshow-container">
    <div class="news-grid">
      <div v-for="(article, index) in articles" :key="index" class="news-item" :class="{ active: index === currentIndex }">
        <img :src="article.image" :alt="article.title" class="news-image">
        <div class="news-content">
          <h5>{{ article.title }}</h5>
          <p>{{ article.content }}</p>
        </div>
      </div>
    </div>
    <button class="nav-button prev" @click="prevSlide">&lt;</button>
    <button class="nav-button next" @click="nextSlide">&gt;</button>
    <div class="pagination">
      {{ currentIndex + 1 }} / {{ articles.length }}
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      articles: [
        { title: "Breaking News: Major Tech Breakthrough", content: "Scientists announce a revolutionary advancement in quantum computing...", image: "https://via.placeholder.com/400x200?text=Tech+Breakthrough", timestamp: "2023-04-15 09:30" },
        { title: "Global Economy Shows Signs of Recovery", content: "Recent economic indicators suggest a positive trend in global markets...", image: "https://via.placeholder.com/400x200?text=Economy+Recovery", timestamp: "2023-04-15 11:45" },
        { title: "New Environmental Policy Unveiled", content: "Government officials reveal ambitious plans to combat climate change...", image: "https://via.placeholder.com/400x200?text=Environmental+Policy", timestamp: "2023-04-15 14:20" },
        { title: "Sports: Underdog Team Wins Championship", content: "In a stunning upset, the underdog team clinches the championship title...", image: "https://via.placeholder.com/400x200?text=Sports+Championship", timestamp: "2023-04-15 18:00" },
        { title: "Health: Breakthrough in Cancer Research", content: "Scientists report a significant advancement in cancer treatment...", image: "https://via.placeholder.com/400x200?text=Cancer+Research", timestamp: "2023-04-16 10:15" },
        { title: "Technology: AI Achieves Human-like Reasoning", content: "New AI model demonstrates unprecedented problem-solving abilities...", image: "https://via.placeholder.com/400x200?text=AI+Breakthrough", timestamp: "2023-04-16 13:40" },
        { title: "Space Exploration: New Exoplanet Discovered", content: "Astronomers identify a potentially habitable planet outside our solar system...", image: "https://via.placeholder.com/400x200?text=Exoplanet+Discovery", timestamp: "2023-04-16 16:55" }
      ],
      currentIndex: 0
    }
  },
  computed: {
    // Remove isFirstSlide and isLastSlide computed properties
  },
  methods: {
    prevSlide() {
      if (this.currentIndex > 1) {
        this.currentIndex -= 2;
      } else {
        this.currentIndex = this.articles.length - 2 + this.currentIndex;
      }
      this.updateSlidePosition();
    },
    nextSlide() {
      if (this.currentIndex < this.articles.length - 2) {
        this.currentIndex += 2;
      } else {
        this.currentIndex = (this.currentIndex + 2) % this.articles.length;
      }
      this.updateSlidePosition();
    },
    updateSlidePosition() {
      const slideWidth = 270; // 250px width + 20px margin-right
      const offset = -Math.floor(this.currentIndex / 2) * (slideWidth * 2);
      this.$el.querySelector('.news-grid').style.transform = `translateX(${offset}px)`;
    }
  }
}
</script>

<style scoped>
.slideshow-container {
  position: relative;
  overflow: hidden;
}

.news-grid {
  display: flex;
  transition: transform 0.5s ease;
}

.news-item {
  display: flex;
  flex-direction: column;
  border: 1px solid #ddd;
  border-radius: 8px;
  padding: 10px;
  background-color: #fff;
  min-width: 250px;
  max-width: 250px;
  margin-right: 20px;
  transition: all 0.5s ease;
}

.news-item.active {
  opacity: 1;
  transform: scale(1.05);
}

.news-image {
  width: 100%;
  height: 150px;
  object-fit: cover;
  border-radius: 8px;
  margin-bottom: 10px;
}

.news-content {
  flex: 1;
}

h5 {
  font-size: 1rem;
  margin-bottom: 5px;
}

p {
  font-size: 0.9rem;
  color: #666;
  overflow: hidden;
  text-overflow: ellipsis;
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
}

.nav-button {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  background-color: rgba(0, 0, 0, 0.5);
  color: white;
  border: none;
  padding: 10px 15px;
  cursor: pointer;
  font-size: 18px;
  border-radius: 5px;
  transition: background-color 0.3s ease;
}

.nav-button:hover:not(:disabled) {
  background-color: rgba(0, 0, 0, 0.7);
}

.nav-button:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}

.prev {
  left: 10px;
}

.next {
  right: 10px;
}

.pagination {
  position: absolute;
  bottom: 10px;
  left: 50%;
  transform: translateX(-50%);
  background-color: rgba(0, 0, 0, 0.5);
  color: white;
  padding: 5px 10px;
  border-radius: 15px;
  font-size: 14px;
}
</style>