---
layout: page
icon: fas fa-microchip
order: 1
---

<div id="repo-container" class="repo-grid"></div>

<script src="https://cdn.jsdelivr.net/npm/repowidget/dist/repoWidget.min.js"></script>

<script>
  // Standard Template Implementation
  createRepoWidget({
    username: 'wavius',
    containerId: 'repo-container',
    maxRepos: 100,
    sortBy: 'stars',
    columns: { mobile: 1, tablet: 2, desktop: 3 },
    // Styling handled here as requested
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

  document.addEventListener('pjax:success', function() {
    document.getElementById('repo-container').innerHTML = '';
    createRepoWidget({
      username: 'wavius',
      containerId: 'repo-container',
      maxRepos: 100,
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
  });
</script>