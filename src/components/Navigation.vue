<template>
  <nav class="navigation">
    <div class="container">
      <ul class="nav-list">
        <li v-for="(item, key) in translations.navigation" :key="key">
          <a 
            href="#" 
            class="nav-link"
            :class="{ active: activeTab === key }"
            @click.prevent="$emit('tab-change', key)"
          >
            {{ item }}
          </a>
        </li>
      </ul>
    </div>
  </nav>
</template>

<script>
export default {
  name: 'Navigation',
  props: {
    translations: {
      type: Object,
      required: true
    },
    activeTab: {
      type: String,
      default: 'home'
    }
  },
  emits: ['tab-change']
}
</script>

<style scoped>
.navigation {
  background: #2c3e50;
  padding: 1rem 0;
  border-bottom: 3px solid #34495e;
}

.nav-list {
  list-style: none;
  display: flex;
  gap: 0.5rem;
  flex-wrap: wrap;
}

.nav-link {
  color: white;
  text-decoration: none;
  padding: 0.75rem 1.5rem;
  border-radius: 8px;
  transition: all 0.3s ease;
  font-weight: 500;
  display: block;
  border: 2px solid transparent;
}

.nav-link:hover {
  background: rgba(255,255,255,0.1);
  transform: translateY(-2px);
}

.nav-link.active {
  background: #3498db;
  border-color: #2980b9;
  box-shadow: 0 4px 12px rgba(52, 152, 219, 0.3);
}

@media (max-width: 768px) {
  .nav-list {
    flex-direction: column;
    gap: 0.25rem;
  }
  
  .nav-link {
    text-align: center;
    padding: 1rem;
  }
}
</style>