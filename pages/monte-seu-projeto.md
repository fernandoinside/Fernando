---
layout: page
title: "Monte seu Projeto"
description: "Configure sua ideia passo a passo e receba uma proposta preliminar."
---

<div class="builder-container">
  <div class="builder-intro">
    <span class="section-tag">Construtor de Soluções</span>
    <h1>Vamos construir algo <span class="text-gradient">Incrível</span>?</h1>
    <p>Preencha os detalhes abaixo para que eu possa entender a complexidade e os requisitos do seu projeto.</p>
  </div>

  <div id="project-builder" class="builder-card">
    <div class="builder-progress">
      <div id="progress-bar" class="progress-fill" style="width: 0%"></div>
    </div>

    <form id="builder-form">
      {% for step in site.data.project_builder.steps %}
      <div class="builder-step {% if forloop.first %}active{% endif %}" data-step="{{ forloop.index }}">
        <span class="step-number">Passo {{ forloop.index }} de {{ site.data.project_builder.steps | size }}</span>
        <h2>{{ step.title }}</h2>
        <p class="step-desc">{{ step.description }}</p>

        <div class="step-content">
          {% if step.type == "textarea" %}
            <textarea name="{{ step.id }}" placeholder="{{ step.placeholder }}" required></textarea>
          
          {% elif step.type == "checkbox" %}
            <div class="options-grid">
              {% for option in step.options %}
              <label class="option-item">
                <input type="checkbox" name="{{ step.id }}" value="{{ option.label }}">
                <span class="option-box">
                  <span class="option-label">{{ option.label }}</span>
                </span>
              </label>
              {% endfor %}
            </div>

          {% elif step.type == "radio" %}
            <div class="options-grid">
              {% for option in step.options %}
              <label class="option-item">
                <input type="radio" name="{{ step.id }}" value="{{ option.label }}" required>
                <span class="option-box">
                  <span class="option-label">{{ option.label }}</span>
                </span>
              </label>
              {% endfor %}
            </div>

          {% elif step.type == "select" %}
            <select name="{{ step.id }}" required>
              <option value="" disabled selected>Selecione uma opção</option>
              {% for option in step.options %}
                <option value="{{ option.label }}">{{ option.label }}</option>
              {% endfor %}
            </select>
          {% endif %}
        </div>

        <div class="step-nav">
          {% if forloop.first == false %}
          <button type="button" class="btn btn-secondary prev-step">Anterior</button>
          {% endif %}
          
          {% if forloop.last %}
          <button type="submit" class="btn btn-primary">Gerar Proposta</button>
          {% else %}
          <button type="button" class="btn btn-primary next-step">Próximo</button>
          {% endif %}
        </div>
      </div>
      {% endfor %}
    </form>

    <div id="builder-result" class="builder-result hidden">
      <div class="result-header">
        <span class="success-icon">✨</span>
        <h2>Sua Proposta Preliminar</h2>
      </div>
      <div id="result-content" class="result-content">
        <!-- Preenchido via JS -->
      </div>
      <div class="result-actions">
        <button onclick="window.print()" class="btn btn-secondary">Baixar PDF</button>
        <a href="/pages/contato" class="btn btn-primary">Falar com Fernando</a>
      </div>
    </div>
  </div>
</div>

<style>
.builder-container {
  max-width: 800px;
  margin: 0 auto;
  padding: 40px 20px;
}

.builder-intro {
  text-align: center;
  margin-bottom: 40px;
}

.builder-card {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: var(--radius-lg);
  padding: 40px;
  position: relative;
  min-height: 400px;
}

.builder-progress {
  height: 6px;
  background: rgba(255,255,255,0.05);
  border-radius: 3px;
  margin-bottom: 40px;
  overflow: hidden;
}

.progress-fill {
  height: 100%;
  background: linear-gradient(to right, var(--primary), var(--secondary));
  transition: width 0.4s cubic-bezier(0.4, 0, 0.2, 1);
}

.builder-step {
  display: none;
  animation: fadeIn 0.4s ease-out;
}

.builder-step.active {
  display: block;
}

.step-number {
  color: var(--primary);
  font-weight: 700;
  text-transform: uppercase;
  font-size: 0.85rem;
  letter-spacing: 1px;
}

.builder-step h2 {
  margin: 12px 0 8px;
  font-size: 2rem;
}

.step-desc {
  color: var(--muted);
  margin-bottom: 32px;
}

.step-content textarea {
  width: 100%;
  min-height: 150px;
  background: rgba(0,0,0,0.2);
  border: 1px solid var(--border);
  border-radius: var(--radius-md);
  color: white;
  padding: 16px;
  font-family: inherit;
  resize: vertical;
}

.options-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 16px;
}

.option-item input {
  display: none;
}

.option-box {
  display: flex;
  align-items: center;
  padding: 20px;
  background: rgba(255,255,255,0.03);
  border: 2px solid var(--border);
  border-radius: var(--radius-md);
  cursor: pointer;
  transition: all 0.2s ease;
  height: 100%;
}

.option-item input:checked + .option-box {
  border-color: var(--primary);
  background: var(--primary-glow);
  transform: translateY(-2px);
}

.option-label {
  font-weight: 600;
}

select {
  width: 100%;
  padding: 16px;
  background: rgba(0,0,0,0.2);
  border: 1px solid var(--border);
  border-radius: var(--radius-md);
  color: white;
  appearance: none;
}

.step-nav {
  margin-top: 40px;
  display: flex;
  gap: 16px;
  justify-content: flex-end;
}

.btn {
  padding: 12px 32px;
  border-radius: var(--radius-md);
  font-weight: 700;
  cursor: pointer;
  transition: all 0.2s;
  border: none;
}

.btn-primary {
  background: var(--primary);
  color: #000;
}

.btn-secondary {
  background: rgba(255,255,255,0.05);
  color: white;
  border: 1px solid var(--border);
}

.builder-result {
  animation: scaleIn 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275);
}

.result-header {
  text-align: center;
  margin-bottom: 32px;
}

.success-icon {
  font-size: 3rem;
  display: block;
  margin-bottom: 16px;
}

.result-content {
  background: rgba(0,0,0,0.3);
  padding: 32px;
  border-radius: var(--radius-md);
  margin-bottom: 32px;
  border: 1px solid var(--primary-glow);
}

.result-item {
  margin-bottom: 24px;
}

.result-item h4 {
  color: var(--primary);
  margin: 0 0 8px;
  font-size: 0.9rem;
  text-transform: uppercase;
}

.result-item p {
  margin: 0;
  font-size: 1.1rem;
}

.hidden { display: none; }

@keyframes fadeIn {
  from { opacity: 0; transform: translateX(10px); }
  to { opacity: 1; transform: translateX(0); }
}

@keyframes scaleIn {
  from { opacity: 0; transform: scale(0.9); }
  to { opacity: 1; transform: scale(1); }
}
</style>

<script>
document.addEventListener('DOMContentLoaded', () => {
  const form = document.getElementById('builder-form');
  const steps = document.querySelectorAll('.builder-step');
  const progressBar = document.getElementById('progress-bar');
  const resultDiv = document.getElementById('builder-result');
  const resultContent = document.getElementById('result-content');
  let currentStep = 1;

  const updateProgress = () => {
    const percent = ((currentStep - 1) / (steps.length - 1)) * 100;
    progressBar.style.width = `${percent}%`;
  };

  const showStep = (n) => {
    steps.forEach(step => step.classList.remove('active'));
    document.querySelector(`.builder-step[data-step="${n}"]`).classList.add('active');
    updateProgress();
  };

  document.querySelectorAll('.next-step').forEach(btn => {
    btn.addEventListener('click', () => {
      const currentInputs = steps[currentStep-1].querySelectorAll('input, textarea, select');
      let valid = true;
      currentInputs.forEach(input => {
        if (input.hasAttribute('required') && !input.value) valid = false;
      });
      
      if (valid) {
        currentStep++;
        showStep(currentStep);
      } else {
        alert('Por favor, preencha o campo obrigatório.');
      }
    });
  });

  document.querySelectorAll('.prev-step').forEach(btn => {
    btn.addEventListener('click', () => {
      currentStep--;
      showStep(currentStep);
    });
  });

  form.addEventListener('submit', (e) => {
    e.preventDefault();
    const formData = new FormData(form);
    const data = {};
    
    formData.forEach((value, key) => {
      if (!data[key]) {
        data[key] = value;
      } else {
        if (!Array.isArray(data[key])) data[key] = [data[key]];
        data[key].push(value);
      }
    });

    // Gerar HTML do Resumo
    let html = `
      <div class="result-item">
        <h4>Objetivo do Projeto</h4>
        <p>${data.objective}</p>
      </div>
      <div class="result-item">
        <h4>Stack Tecnológica</h4>
        <p>${Array.isArray(data.stack) ? data.stack.join(', ') : data.stack}</p>
      </div>
      <div class="result-item">
        <h4>Recursos Chave</h4>
        <p>${Array.isArray(data.features) ? data.features.join(', ') : data.features}</p>
      </div>
      <div class="result-item">
        <h4>Modelo e Prazo</h4>
        <p>${data.model} | Entrega em ${data.timeline}</p>
      </div>
      <div class="result-item">
        <h4>Observações Adicionais</h4>
        <p>${data.budget}</p>
      </div>
      <div class="result-highlight" style="margin-top: 32px; padding-top: 24px; border-top: 1px solid var(--border);">
        <p><strong>Diagnóstico Fernando Machado:</strong> Com base nas tecnologias (${Array.isArray(data.stack) ? data.stack[0] : data.stack}) e foco em ${Array.isArray(data.features) ? data.features[0] : data.features}, seu projeto é viável e pode ser estruturado como ${data.model}.</p>
      </div>
    `;

    form.classList.add('hidden');
    resultContent.innerHTML = html;
    resultDiv.classList.remove('hidden');
    progressBar.style.width = '100%';
  });
});
</script>
