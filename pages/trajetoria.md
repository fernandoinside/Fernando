---
layout: page
title: "Trajetória Técnica"
description: "Uma linha do tempo detalhada das minhas principais conquistas, tecnologias e projetos desenvolvidos."
---

<div class="skills-page">
  <div class="skills-intro">
    <span class="section-tag">Carreira & Conquistas</span>
    <h1>Conhecimento em <span class="text-gradient">Ação</span></h1>
    <p>Mais do que teoria, minha carreira é pautada pela construção real de soluções complexas, de hardwares de IoT a orquestradores de IA.</p>
  </div>

  <div class="skills-timeline-container">
    {% for skill in site.data.skills_timeline %}
<div class="timeline-card-wrapper" style="animation-delay: {{ forloop.index | times: 100 }}ms">
  <div class="timeline-marker">
        <div class="marker-icon">{{ skill.icon }}</div>
        <div class="marker-line"></div>
      </div>
      
      <div class="skill-card">
        <div class="skill-card-header">
          <span class="skill-category">{{ skill.category }}</span>
          <h3>{{ skill.title }}</h3>
        </div>
        <div class="skill-card-body">
          <p>{{ skill.description }}</p>
          <div class="skill-tags">
            {% for tag in skill.tags %}
            <span class="skill-tag">#{{ tag }}</span>
            {% endfor %}
          </div>
        </div>
      </div>
    </div>
    {% endfor %}
  </div>

  <div class="skills-cta">
    <h2>Interessado em algum desses setores?</h2>
    <p>Posso replicar, escalar ou criar algo totalmente novo para sua necessidade.</p>
    <div class="cta-buttons">
      <a href="/pages/monte-seu-projeto" class="btn btn-primary">Monte seu Projeto</a>
      <a href="/pages/contato" class="btn btn-secondary">Entrar em Contato</a>
    </div>
  </div>
</div>

<style>
.skills-page {
  max-width: 1000px;
  margin: 0 auto;
  padding: 40px 20px;
}

.skills-intro {
  text-align: center;
  margin-bottom: 80px;
}

.skills-intro h1 {
  font-size: clamp(2.5rem, 6vw, 4rem);
  font-weight: 800;
  margin-bottom: 16px;
  background: linear-gradient(to right, var(--primary), var(--secondary));
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.skills-intro p {
  color: var(--muted);
  font-size: 1.2rem;
  max-width: 600px;
  margin: 0 auto;
}

.skills-timeline-container {
  position: relative;
  padding-left: 80px;
}

.skills-timeline-container::before {
  content: '';
  position: absolute;
  left: 39px;
  top: 0;
  bottom: 0;
  width: 2px;
  background: linear-gradient(to bottom, var(--primary), var(--secondary), transparent);
  opacity: 0.3;
}

.timeline-card-wrapper {
  position: relative;
  margin-bottom: 60px;
  opacity: 0;
  transform: translateY(20px);
  animation: fadeInUp 0.6s ease-out forwards;
}

{% for skill in site.data.skills_timeline %}
.timeline-card-wrapper:nth-child({{ forloop.index }}) {
  animation-delay: {{ forloop.index | times: 0.1 }}s;
}
{% endfor %}

.timeline-marker {
  position: absolute;
  left: -80px;
  width: 80px;
  display: flex;
  justify-content: center;
}

.marker-icon {
  width: 50px;
  height: 50px;
  background: var(--surface);
  border: 2px solid var(--primary);
  border-radius: 15px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.5rem;
  z-index: 2;
  box-shadow: 0 0 20px var(--primary-glow);
  transition: transform 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275);
}

.timeline-card-wrapper:hover .marker-icon {
  transform: scale(1.2) rotate(10deg);
  background: var(--primary);
  border-color: #000;
}

.skill-card {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: var(--radius-lg);
  padding: 32px;
  transition: all 0.3s ease;
  position: relative;
  overflow: hidden;
}

.skill-card::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 4px;
  height: 0;
  background: var(--primary);
  transition: height 0.3s ease;
}

.skill-card:hover {
  transform: translateX(10px);
  border-color: var(--primary-glow);
  background: rgba(15, 23, 42, 0.8);
}

.skill-card:hover::before {
  height: 100%;
}

.skill-category {
  font-size: 0.75rem;
  font-weight: 800;
  text-transform: uppercase;
  letter-spacing: 2px;
  color: var(--primary);
  display: block;
  margin-bottom: 8px;
}

.skill-card h3 {
  margin: 0 0 16px;
  font-size: 1.5rem;
}

.skill-card-body p {
  color: var(--muted);
  line-height: 1.6;
  margin-bottom: 24px;
}

.skill-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
}

.skill-tag {
  font-size: 0.8rem;
  background: rgba(255,255,255,0.05);
  padding: 4px 12px;
  border-radius: 100px;
  color: var(--secondary);
  border: 1px solid rgba(255,255,255,0.1);
}

.skills-cta {
  margin-top: 100px;
  text-align: center;
  padding: 60px;
  background: linear-gradient(rgba(56, 189, 248, 0.05), transparent);
  border-radius: var(--radius-lg);
  border: 1px solid var(--border);
}

.cta-buttons {
  display: flex;
  gap: 16px;
  justify-content: center;
  margin-top: 32px;
}

@keyframes fadeInUp {
  from { opacity: 0; transform: translateY(20px); }
  to { opacity: 1; transform: translateY(0); }
}

@media (max-width: 768px) {
  .skills-timeline-container {
    padding-left: 40px;
  }
  .skills-timeline-container::before {
    left: 19px;
  }
  .timeline-marker {
    left: -40px;
    width: 40px;
  }
  .marker-icon {
    width: 40px;
    height: 40px;
    font-size: 1.2rem;
  }
}
</style>
