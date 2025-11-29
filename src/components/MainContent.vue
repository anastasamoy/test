<template>
  <main class="main-content">
    <div class="container">
      
      <!-- Welcome Section -->
      <section class="section welcome-section">
        <h2 class="section-title">{{ translations.main.welcome }}</h2>
        <p class="intro-text">{{ translations.main.intro }}</p>
        
        <div class="button-demo mt-2">
          <h3>Demo tlačidlá:</h3>
          <div class="button-group">
            <button 
              v-for="btn in buttons" 
              :key="btn.type"
              :class="['btn', `btn-${btn.type}`]"
              @click="showAlert(btn.type)"
            >
              {{ btn.label }}
            </button>
          </div>
        </div>
      </section>

      <!-- Interactive Demo -->
      <section class="section interactive-section">
        <h2 class="section-title">Interaktívna demo časť</h2>
        
        <div class="interactive-controls">
          <button class="btn btn-primary" @click="toggleDemoContent">
            {{ showDemoContent ? 'Skryť' : 'Zobraziť' }} demo obsah
          </button>
          
          <transition name="slide-fade">
            <div v-if="showDemoContent" class="demo-content">
              <h3>Dynamický obsah</h3>
              <p>Tento obsah sa zobrazuje/skryva pomocou Vue.js reaktywnosti!</p>
              
              <div class="counter-demo">
                <h4>Počítadlo: {{ counter }}</h4>
                <div class="counter-controls">
                  <button class="btn btn-danger" @click="decrement">-</button>
                  <span class="counter-value">{{ counter }}</span>
                  <button class="btn btn-success" @click="increment">+</button>
                </div>
              </div>
            </div>
          </transition>
        </div>
      </section>

      <!-- Contact Form -->
      <section class="section form-section">
        <h2 class="section-title">{{ translations.main.contactForm }}</h2>
        
        <form @submit.prevent="submitForm" class="contact-form">
          <div class="form-grid">
            <div class="form-group">
              <label class="form-label">{{ translations.form.name }} *</label>
              <input 
                type="text" 
                class="form-input"
                v-model="form.name"
                placeholder="Zadajte vaše celé meno"
                required
              >
            </div>
            
            <div class="form-group">
              <label class="form-label">{{ translations.form.email }} *</label>
              <input 
                type="email" 
                class="form-input"
                v-model="form.email"
                placeholder="vas@email.sk"
                required
              >
            </div>
          </div>
          
          <div class="form-group">
            <label class="form-label">{{ translations.form.phone }}</label>
            <input 
              type="tel" 
              class="form-input"
              v-model="form.phone"
              placeholder="+421 XXX XXX XXX"
            >
          </div>
          
          <div class="form-group">
            <label class="form-label">{{ translations.form.category }}</label>
            <select class="form-select" v-model="form.category">
              <option 
                v-for="(cat, key) in translations.form.categories" 
                :value="key" 
                :key="key"
              >
                {{ cat }}
              </option>
            </select>
          </div>
          
          <div class="form-group">
            <label class="form-label">{{ translations.form.message }} *</label>
            <textarea 
              class="form-textarea"
              v-model="form.message"
              placeholder="Napíšte nám správu..."
              rows="5"
              required
            ></textarea>
          </div>
          
          <div class="form-actions">
            <button type="submit" class="btn btn-primary">
              {{ translations.form.submit }}
            </button>
            <button type="button" class="btn btn-secondary" @click="resetForm">
              {{ translations.form.reset }}
            </button>
          </div>
        </form>
      </section>

      <!-- Dynamic List -->
      <section class="section list-section">
        <h2 class="section-title">Dynamický zoznam úloh</h2>
        
        <div class="list-controls">
          <input 
            type="text" 
            class="form-input"
            v-model="newItem"
            placeholder="Pridajte novú položku..."
            @keyup.enter="addItem"
          >
          <button class="btn btn-success" @click="addItem">
            ➕ Pridať
          </button>
        </div>
        
        <ul class="item-list">
          <li 
            v-for="(item, index) in items" 
            :key="index"
            class="item-list-item"
          >
            <span class="item-text">{{ item }}</span>
            <button 
              class="btn btn-danger btn-sm"
              @click="removeItem(index)"
            >
              🗑️ Odstrániť
            </button>
          </li>
        </ul>
        
        <div v-if="items.length === 0" class="empty-state">
          📝 Zoznam je prázdny. Pridajte prvú položku!
        </div>
        
        <div class="list-stats">
          Celkový počet položiek: <strong>{{ items.length }}</strong>
        </div>
      </section>

    </div>
  </main>
</template>

<script>
export default {
  name: 'MainContent',
  props: {
    translations: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      showDemoContent: false,
      counter: 0,
      newItem: '',
      items: [
        'Prvá ukážková úloha',
        'Druhá ukážková úloha', 
        'Tretia ukážková úloha'
      ],
      form: {
        name: '',
        email: '',
        phone: '',
        category: 'general',
        message: ''
      },
      buttons: [
        { type: 'primary', label: 'Hlavná akcia' },
        { type: 'secondary', label: 'Vedľajšia akcia' },
        { type: 'success', label: 'Úspešná akcia' },
        { type: 'danger', label: 'Nebezpečná akcia' }
      ]
    }
  },
  methods: {
    showAlert(type) {
      const messages = {
        primary: 'Hlavná akcia bola spustená!',
        secondary: 'Vedľajšia akcia bola spustená!',
        success: 'Operácia prebehla úspešne! 🎉',
        danger: 'Varovanie: Táto akcia môže byť nebezpečná! ⚠️'
      }
      alert(messages[type])
    },
    
    toggleDemoContent() {
      this.showDemoContent = !this.showDemoContent
    },
    
    increment() {
      this.counter++
    },
    
    decrement() {
      this.counter--
    },
    
    addItem() {
      if (this.newItem.trim()) {
        this.items.push(this.newItem.trim())
        this.newItem = ''
      }
    },
    
    removeItem(index) {
      this.items.splice(index, 1)
    },
    
    submitForm() {
      if (this.form.name && this.form.email && this.form.message) {
        alert(`Formulár bol úspešne odoslaný! 📨\n\nMeno: ${this.form.name}\nEmail: ${this.form.email}\nTelefón: ${this.form.phone || 'Nezadaný'}\nKategória: ${this.translations.form.categories[this.form.category]}\nSpráva: ${this.form.message}`)
        this.resetForm()
      } else {
        alert('Prosím, vyplňte všetky povinné polia!')
      }
    },
    
    resetForm() {
      this.form = {
        name: '',
        email: '',
        phone: '',
        category: 'general',
        message: ''
      }
    }
  }
}
</script>

<style scoped>
.main-content {
  flex: 1;
  padding: 2rem 0;
}

.section {
  background: white;
  padding: 2rem;
  margin-bottom: 2rem;
  border-radius: 12px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  border: 1px solid #e1e8ed;
}

.section-title {
  color: #2c3e50;
  margin-bottom: 1.5rem;
  font-size: 1.5rem;
  font-weight: 600;
  border-bottom: 3px solid #3498db;
  padding-bottom: 0.5rem;
}

/* Buttons */
.btn {
  padding: 0.75rem 1.5rem;
  border: none;
  border-radius: 8px;
  font-size: 0.95rem;
  cursor: pointer;
  transition: all 0.3s ease;
  font-weight: 600;
  text-decoration: none;
  display: inline-block;
  text-align: center;
  border: 2px solid transparent;
}

.btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.2);
}

.btn-primary {
  background: #3498db;
  color: white;
}

.btn-primary:hover {
  background: #2980b9;
}

.btn-secondary {
  background: #95a5a6;
  color: white;
}

.btn-secondary:hover {
  background: #7f8c8d;
}

.btn-success {
  background: #27ae60;
  color: white;
}

.btn-success:hover {
  background: #219a52;
}

.btn-danger {
  background: #e74c3c;
  color: white;
}

.btn-danger:hover {
  background: #c0392b;
}

.btn-sm {
  padding: 0.5rem 1rem;
  font-size: 0.85rem;
}

.button-group {
  display: flex;
  gap: 1rem;
  flex-wrap: wrap;
  margin-top: 1rem;
}

/* Forms */
.contact-form {
  max-width: 800px;
}

.form-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1rem;
}

.form-group {
  margin-bottom: 1.5rem;
}

.form-label {
  display: block;
  margin-bottom: 0.5rem;
  font-weight: 600;
  color: #2c3e50;
}

.form-input,
.form-textarea,
.form-select {
  width: 100%;
  padding: 0.75rem;
  border: 2px solid #e1e8ed;
  border-radius: 8px;
  font-size: 1rem;
  transition: all 0.3s ease;
  background: #f8f9fa;
}

.form-input:focus,
.form-textarea:focus,
.form-select:focus {
  outline: none;
  border-color: #3498db;
  background: white;
  box-shadow: 0 0 0 3px rgba(52, 152, 219, 0.1);
}

.form-textarea {
  min-height: 120px;
  resize: vertical;
  font-family: inherit;
}

.form-actions {
  display: flex;
  gap: 1rem;
  margin-top: 2rem;
}

/* List Styles */
.list-controls {
  display: flex;
  gap: 1rem;
  margin-bottom: 1.5rem;
}

.list-controls .form-input {
  flex: 1;
}

.item-list {
  list-style: none;
  margin-bottom: 1rem;
}

.item-list-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem;
  background: #f8f9fa;
  margin-bottom: 0.5rem;
  border-radius: 8px;
  border-left: 4px solid #3498db;
  transition: all 0.3s ease;
}

.item-list-item:hover {
  background: #e9ecef;
  transform: translateX(5px);
}

.item-text {
  flex: 1;
}

.empty-state {
  text-align: center;
  color: #6c757d;
  font-style: italic;
  padding: 2rem;
  background: #f8f9fa;
  border-radius: 8px;
}

.list-stats {
  text-align: center;
  padding: 1rem;
  background: #e8f4fd;
  border-radius: 8px;
  color: #2c3e50;
}

/* Interactive Demo */
.interactive-controls {
  text-align: center;
}

.demo-content {
  background: #f8f9fa;
  padding: 2rem;
  border-radius: 8px;
  margin-top: 1.5rem;
  border-left: 4px solid #27ae60;
}

.counter-demo {
  margin-top: 1.5rem;
}

.counter-controls {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 1rem;
  margin-top: 1rem;
}

.counter-value {
  font-size: 2rem;
  font-weight: bold;
  color: #2c3e50;
  min-width: 60px;
  text-align: center;
}

/* Transitions */
.slide-fade-enter-active,
.slide-fade-leave-active {
  transition: all 0.5s ease;
}

.slide-fade-enter-from,
.slide-fade-leave-to {
  opacity: 0;
  transform: translateY(-20px);
}

/* Responsive */
@media (max-width: 768px) {
  .form-grid {
    grid-template-columns: 1fr;
  }
  
  .form-actions {
    flex-direction: column;
  }
  
  .button-group {
    flex-direction: column;
  }
  
  .list-controls {
    flex-direction: column;
  }
  
  .item-list-item {
    flex-direction: column;
    gap: 1rem;
    text-align: center;
  }
  
  .section {
    padding: 1.5rem;
  }
}
</style>