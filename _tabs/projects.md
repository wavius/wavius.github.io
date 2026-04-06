---
layout: page
icon: fas fa-microchip
order: 1
---

<div id="github-repos" class="repo-grid"></div>

<script>
  document.addEventListener('DOMContentLoaded', () => {
    const username = 'wavius';
    const container = document.getElementById('github-repos');
    
    async function fetchRepos() {
      try {
        const response = await fetch(`https://api.github.com/users/${username}/repos?sort=updated&per_page=100`);
        
        if (!response.ok) {
          throw new Error(`GitHub API returned ${response.status}`);
        }

        const repos = await response.json();

        if (repos.length === 0) {
          container.innerHTML = "<p>No public repositories found.</p>";
          return;
        }

        container.innerHTML = repos
          .filter(repo => !repo.fork && !repo.archived) // Professional filter
          .map(repo => `
            <div class="repo-card">
              <div class="repo-header">
                <i class="fab fa-github"></i>
                <a href="${repo.html_url}" target="_blank" class="repo-title">${repo.name}</a>
              </div>
              <p class="repo-desc">${repo.description || 'No description provided.'}</p>
              <div class="repo-meta">
                <span class="repo-lang"><b>${repo.language || 'Code'}</b></span>
                <span class="repo-stars">⭐ ${repo.stargazers_count}</span>
              </div>
            </div>
          `).join('');
      } catch (error) {
        console.error("Fetch error:", error);
        container.innerHTML = `
          <p style="grid-column: 1/-1; text-align: center; padding: 2rem; border: 1px dashed var(--main-border-color);">
            API limit reached or connection blocked. <br>
            <a href="https://github.com/${username}" class="btn btn-outline-primary mt-3">View my Projects on GitHub</a>
          </p>`;
      }
    }

    fetchRepos();
  });
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