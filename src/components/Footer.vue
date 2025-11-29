<template>
  <footer class="footer">
    <div class="container">
      <div class="footer-content">
        <div class="footer-info">
          <p>{{ translations.footer.copyright }}</p>
          <p>{{ translations.footer.madeWith }}</p>
        </div>
        <div class="footer-links">
          <a href="#" class="footer-link">Podmienky používania</a>
          <a href="#" class="footer-link">Ochrana súkromia</a>
          <a href="#" class="footer-link">Podpora</a>
        </div>
      </div>
    </div>
  </footer>
</template>

<script>
export default {
  name: 'Footer',
  props: {
    translations: {
      type: Object,
      required: true
    }
  }
}
</script>

<style scoped>
.footer {
  background: #2c3e50;
  color: white;
  padding: 2rem 0;
  margin-top: auto;
  border-top: 3px solid #34495e;
}

.footer-content {
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
  gap: 1rem;
}

.footer-info p {
  margin-bottom: 0.5rem;
  opacity: 0.9;
}

.footer-links {
  display: flex;
  gap: 1.5rem;
}

.footer-link {
  color: #bdc3c7;
  text-decoration: none;
  transition: color 0.3s ease;
}

.footer-link:hover {
  color: #3498db;
}

@media (max-width: 768px) {
  .footer-content {
    flex-direction: column;
    text-align: center;
  }
  
  .footer-links {
    flex-direction: column;
    gap: 1rem;
  }
}
</style>