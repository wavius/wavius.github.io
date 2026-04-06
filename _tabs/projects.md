---
layout: page
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
      
      // Check if library is ready
      if (typeof createRepoWidget === 'function') {
        console.log("RepoWidget ready, initializing...");
        container.innerHTML = ''; // Clear previous
        
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
        // If not ready, wait 200ms and try again
        retryCount++;
        setTimeout(initRepoWidget, 200);
      }
    }

    // Run on load
    initRepoWidget();

    // Fix for Chirpy Pjax navigation
    document.addEventListener('pjax:success', () => {
      retryCount = 0;
      initRepoWidget();
    });
  })();
</script>