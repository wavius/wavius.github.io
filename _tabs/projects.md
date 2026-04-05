---
layout: page
icon: fas fa-microchip
order: 1
---

<div id="github-repos" class="repo-grid"></div>

<script>
  async function fetchRepos() {
    const username = 'wavius';
    const container = document.getElementById('github-repos');
    
    try {
      const response = await fetch(`https://api.github.com/users/${username}/repos?sort=updated&per_page=100`);
      const repos = await response.json();

      container.innerHTML = repos
        .filter(repo => !repo.fork) // This hides forks to keep it professional
        .map(repo => `
          <div class="repo-card">
            <div class="repo-header">
              <i class="fa-brands fa-github"></i>
              <a href="${repo.html_url}" target="_blank" class="repo-title">${repo.name}</a>
            </div>
            <p class="repo-desc">${repo.description || 'No description provided.'}</p>
            <div class="repo-meta">
              <span class="repo-lang">${repo.language || 'Plain Text'}</span>
              <span class="repo-stars">⭐ ${repo.stargazers_count}</span>
            </div>
          </div>
        `).join('');
    } catch (error) {
      container.innerHTML = `<p>Oops! Couldn't load the repos. <a href="https://github.com/wavius">View them on GitHub instead.</a></p>`;
    }
  }

  window.onload = fetchRepos;
</script>

<style>
  .repo-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
    gap: 1.5rem;
    margin-top: 2rem;
  }
  .repo-card {
    background: var(--card-bg);
    border: 1px solid var(--main-border-color);
    border-radius: 8px;
    padding: 1.25rem;
    transition: transform 0.2s ease;
  }
  .repo-card:hover {
    transform: translateY(-4px);
    border-color: var(--link-color);
  }
  .repo-header {
    display: flex;
    align-items: center;
    gap: 10px;
    margin-bottom: 0.5rem;
  }
  .repo-title {
    font-weight: bold;
    font-size: 1.1rem;
    color: var(--link-color) !important;
    text-decoration: none;
  }
  .repo-desc {
    font-size: 0.9rem;
    color: var(--text-muted-color);
    margin-bottom: 1rem;
    height: 2.7rem;
    overflow: hidden;
    display: -webkit-box;
    -webkit-line-clamp: 2;
    -webkit-box-orient: vertical;
  }
  .repo-meta {
    font-size: 0.8rem;
    display: flex;
    gap: 15px;
    opacity: 0.8;
  }
</style>