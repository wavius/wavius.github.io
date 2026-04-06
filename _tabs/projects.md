---
layout: page
title: Projects
icon: fas fa-microchip
order: 1
---

<div id="repo-container"></div>

<script src="https://cdn.jsdelivr.net/npm/repowidget/dist/repoWidget.min.js"></script>

<script>
  (function() {
    let retryCount = 0;
    function initRepoWidget() {
      const container = document.getElementById('repo-container');
      if (typeof createRepoWidget === 'function') {
        container.innerHTML = ''; 
        createRepoWidget({
          username: 'wavius',
          containerId: 'repo-container',
          maxRepos: 20,
          sortBy: 'stars',
          columns: { mobile: 1, tablet: 2, desktop: 3 },
          cardStyles: { 
            backgroundColor: 'var(--card-bg)', 
            borderRadius: '8px', 
            border: '1px solid var(--main-border-color)' 
          },
          textStyles: { 
            titleColor: 'var(--link-color)', 
            descriptionColor: 'var(--text-muted-color)' 
          }
        });
      } else if (retryCount < 10) {
        retryCount++;
        setTimeout(initRepoWidget, 200);
      }
    }
    initRepoWidget();
    document.addEventListener('pjax:success', initRepoWidget);
  })();
</script>

<style>
  #repo-container {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
    gap: 1.5rem;
    margin-top: 2rem;
    min-height: 200px;
  }
  .repo-widget {
    margin-bottom: 0 !important;
    width: 100% !important;
  }
</style>