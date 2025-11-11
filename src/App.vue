<script setup>
import { ref } from 'vue'

const q = ref('')
const isSearchOpen = ref(false)

const toggleSearch = () => {
  isSearchOpen.value = !isSearchOpen.value
}

const doSearch = () => {
  console.log('Buscando por:', q.value)
}

const recipes = ref([
  { id: 1, title: 'Lasanha Bolonhesa', image: 'https://placehold.co/600x400/E8A978/4F321A?text=Lasanha', time: 90, category: 'Jantar', views: '2200', rating: 4.6, popular: true },
  { id: 2, title: 'Bolo de Chocolate Molhadinho', image: 'https://placehold.co/600x400/E8A978/4F321A?text=Bolo', time: 60, category: 'Sobremesa', views: '2100', rating: 4.5, popular: true },
  { id: 3, title: 'Sushi Caseiro', image: 'https://placehold.co/600x400/E8A978/4F321A?text=Sushi', time: 60, category: 'Jantar', views: '1950', rating: 4.5, popular: true },
  { id: 4, title: 'Brigadeiro Gourmet', image: 'https://placehold.co/600x400/E8A978/4F321A?text=Brigadeiro', time: 45, category: 'Sobremesa', views: '1800', rating: 4.7, popular: true },
  { id: 5, title: 'Pudim de Leite', image: 'https://placehold.co/600x400/E8A978/4F321A?text=Pudim', time: 70, category: 'Sobremesa', views: '1650', rating: 4.9, popular: true },
  { id: 6, title: 'Panquecas Americanas', image: 'https://placehold.co/600x400/E8A978/4F321A?text=Panquecas', time: 25, category: 'Café da Manhã', views: '1520', rating: 4.2, popular: true },
  { id: 7, title: 'Tacos Mexicanos', image: 'https://placehold.co/600x400/E8A978/4F321A?text=Tacos', time: 35, category: 'Jantar', views: '1450', rating: 4.3, popular: true },
  { id: 8, title: 'Risoto de Cogumelos', image: 'https://placehold.co/600x400/E8A978/4F321A?text=Risoto', time: 40, category: 'Jantar', views: '1350', rating: 4.4, popular: false },
  { id: 9, title: 'Frango com Quiabo', image: 'https://placehold.co/600x400/E8A978/4F321A?text=Frango', time: 45, category: 'Jantar', views: '1250', rating: 4.8, popular: false },
  { id: 10, title: 'Salada Caesar', image: 'https://placehold.co/600x400/E8A978/4F321A?text=Salada', time: 15, category: 'Salada', views: '980', rating: 4.0, popular: false }
])
</script>

<template>
  <div class="app">
    <!-- ===== Cabeçalho ===== -->
    <header class="navbar">
      <a href="#" class="logo-link">
        <span class="logo-text">Receitas Deliciosas</span>
      </a>

      <nav class="nav-center">
        <a href="#" class="active"><span>🏠</span> Início</a>
        <a href="#"><span>🍽️</span> Receitas</a>
        <a href="#"><span>❤️</span> Favoritos</a>
        <a href="#"><span>➕</span> Adicionar</a>
      </nav>

      <div class="search-box" :class="{ open: isSearchOpen }">
        <input
          v-model="q"
          placeholder="Buscar receitas..."
          @keyup.enter="doSearch"
        />
        <button @click="toggleSearch">🔍</button>
      </div>
    </header>

    <!-- ===== Hero ===== -->
    <section class="hero">
      <div class="hero-content">
        <h1>Descubra pratos incríveis<br />para todas as ocasiões</h1>
        <p>Encontre receitas deliciosas, simples e rápidas!</p>
        <button class="cta-btn">Explorar Receitas</button>
      </div>
    </section>

    <!-- ===== Filtros ===== -->
    <section class="filters">
      <h2>Filtrar Receitas</h2>
      <div class="filter-group">
        <select>
          <option>Todas (Categoria)</option>
          <option>Jantar</option>
          <option>Sobremesa</option>
          <option>Café da Manhã</option>
        </select>
        <select>
          <option>Todas (Tipo)</option>
          <option>Doce</option>
          <option>Salgado</option>
          <option>Bebida</option>
        </select>
        <select>
          <option>Popularidade</option>
          <option>Mais Recentes</option>
          <option>Melhor Avaliado</option>
        </select>
      </div>
    </section>

    <!-- ===== Receitas ===== -->
    <main class="recipes">
      <h3>{{ recipes.length }} receitas encontradas</h3>

      <div class="grid">
        <div v-for="r in recipes" :key="r.id" class="card">
          <div class="img-wrap">
            <img :src="r.image" :alt="r.title" />
            <span v-if="r.popular" class="badge">⭐ Popular</span>
          </div>
          <div class="content">
            <h4>{{ r.title }}</h4>
            <p class="meta">{{ r.category }} • {{ r.time }} min</p>
            <div class="info">
              <span class="rating">⭐ {{ r.rating }}</span>
              <span class="views">👁️ {{ r.views }}</span>
            </div>
            <button class="see-btn">Ver Receita</button>
          </div>
        </div>
      </div>
    </main>
  </div>
</template>

<style scoped>
body {
  font-family: 'Inter', sans-serif;
  background: #fdfaf7;
  color: #333;
}

/* ===== Navbar ===== */
.navbar {
  display: flex;
  align-items: center;
  justify-content: space-between;
  background: #fff;
  padding: 6px 24px;
  box-shadow: 0 1px 6px rgba(0,0,0,0.05);
  border-radius: 0 0 10px 10px;
  font-family: 'Poppins', sans-serif;
  position: sticky;
  top: 0;
  z-index: 1000;
}

/* ===== Logo ===== */
.logo-link {
  display: flex;
  align-items: center;
  gap: 10px;
  text-decoration: none;
}

.logo {
  width: 38px;
  height: 38px;
  border-radius: 10px;
  background: #ff7b00;
  padding: 4px;
  box-shadow: 0 2px 6px rgba(255, 123, 0, 0.3);
}

.logo-text {
  background: rgba(255, 123, 0, 0.15);
  color: #ff7b00;
  font-weight: 600;
  border-radius: 50px;
  padding: 6px 14px;
  font-size: 0.9rem;
  box-shadow: inset 0 0 0 1px rgba(255, 123, 0, 0.2);
}

/* ===== Navegação ===== */
.nav-center {
  display: flex;
  align-items: center;
  gap: 14px;
}

.nav-center a {
  text-decoration: none;
  color: #333;
  font-weight: 500;
  font-size: 0.9rem;
  padding: 6px 12px;
  border-radius: 10px;
  transition: all 0.25s ease;
  display: flex;
  align-items: center;
  gap: 6px;
}

.nav-center a:hover {
  background: #fff3e6;
  color: #ff7b00;
}

.nav-center .active {
  background: #ff7b00;
  color: #fff;
}

/* ===== Busca ===== */
.search-box {
  display: flex;
  align-items: center;
  background: rgba(255, 123, 0, 0.15);
  border-radius: 50px;
  padding: 4px 6px;
  transition: all 0.3s ease;
  box-shadow: inset 0 0 0 1px rgba(255, 123, 0, 0.2);
}

.search-box input {
  border: none;
  background: transparent;
  outline: none;
  color: #333;
  padding: 6px 10px;
  width: 0;
  transition: width 0.3s ease;
  font-size: 0.9rem;
}

.search-box.open input {
  width: 140px;
}

.search-box button {
  border: none;
  background: #ff7b00;
  color: #fff;
  font-size: 1rem;
  border-radius: 50%;
  width: 30px;
  height: 30px;
  cursor: pointer;
}

/* ===== Hero ===== */
.hero {
  height: 400px;
  background: linear-gradient(rgba(0,0,0,0.5), rgba(0,0,0,0.5)),
              url('https://images.unsplash.com/photo-1546069901-ba9599a7e63c') center/cover;
  display: flex;
  align-items: center;
  justify-content: center;
  color: #fff;
  text-align: center;
}

.hero-content h1 {
  font-size: 2.6rem;
  font-weight: 700;
  text-shadow: 0 2px 8px rgba(0,0,0,0.4);
}

.hero-content p {
  margin-top: 12px;
  font-size: 1.1rem;
}

.cta-btn {
  background: #ff7b00;
  border: none;
  padding: 12px 24px;
  margin-top: 20px;
  border-radius: 10px;
  color: white;
  font-weight: 600;
  cursor: pointer;
  transition: 0.3s;
}

.cta-btn:hover {
  background: #e06f00;
}

/* ===== Filtros ===== */
.filters {
  max-width: 900px;
  margin: 40px auto;
  background: #fff;
  padding: 24px;
  border-radius: 16px;
  box-shadow: 0 2px 10px rgba(0,0,0,0.05);
}

.filter-group {
  display: flex;
  gap: 16px;
  margin-top: 12px;
}

.filter-group select {
  flex: 1;
  padding: 10px;
  border-radius: 8px;
  border: 1px solid #ddd;
  font-size: 1rem;
}

/* ===== Receitas ===== */
.recipes {
  max-width: 1100px;
  margin: 0 auto 60px;
  padding: 0 20px;
}

.recipes h3 {
  font-size: 1.4rem;
  margin-bottom: 20px;
}

.grid {
  display: grid;
  grid-template-columns: repeat(auto-fill,minmax(300px,1fr));
  gap: 28px;
}

.card {
  background: #fff;
  border-radius: 18px;
  box-shadow: 0 4px 12px rgba(0,0,0,0.08);
  overflow: hidden;
  transition: transform 0.25s ease, box-shadow 0.25s ease;
}

.card:hover {
  transform: translateY(-6px);
  box-shadow: 0 6px 18px rgba(0,0,0,0.12);
}

.img-wrap {
  position: relative;
  overflow: hidden;
}

.img-wrap img {
  width: 100%;
  height: 200px;
  object-fit: cover;
  transition: transform 0.3s ease;
}

.card:hover img {
  transform: scale(1.05);
}

.badge {
  position: absolute;
  top: 10px;
  right: 10px;
  background: #ff7b00;
  color: white;
  font-size: 0.8rem;
  padding: 4px 10px;
  border-radius: 8px;
}

.content {
  padding: 18px;
}

.content h4 {
  font-size: 1.1rem;
  font-weight: 600;
  color: #333;
}

.meta {
  color: #777;
  margin: 6px 0 10px;
  font-size: 0.9rem;
}

.info {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.rating {
  color: #ffb400;
  font-weight: 600;
}

.views {
  font-size: 0.85rem;
  color: #999;
}

.see-btn {
  margin-top: 14px;
  width: 100%;
  background: #ff7b00;
  color: #fff;
  border: none;
  padding: 10px 0;
  border-radius: 10px;
  cursor: pointer;
  font-weight: 500;
  transition: 0.3s;
}

.see-btn:hover {
  background: #e06f00;
}
</style>
