---
# the default layout is 'page'
icon: fas fa-info-circle
order: 5
---

![Me](../assets/img/tabs/about/ME!!!.jpg){: w="200" .left}

Howdy, I'm David <span id="secret-trigger" style="color: #A020F0; cursor: default; user-select: none;">'wavius'</span> Ceuca, a second year Computer Engineering student at the University of Toronto, with a passion for hardware and electronics.

I have a background in PCB design, analog electronics, and embedded systems, with recent projects focusing more on FPGA development. My academic curiosity is currently leaning toward Analog IC design, though that may change in the future as I continue to learn about more interesting hardware.

<br>

I really love my girlfriend 🩵🩶, family, tennis, and cats 😻. Here are some doodles from my amazing girlfriend <3

![Cat](../assets/img/tabs/about/steph_cat.png){: w="500" .left}
![Jinx and Vi](../assets/img/tabs/about/jinx_vi_doodle.png){: w="500" .left}
![Jinx and Vi](../assets/img/tabs/about/steph_jinx.png){: w="500" .left}

<script>
  function initSecretTrigger() {
    const trigger = document.getElementById('secret-trigger');
    let clickCount = 0;
    let timer;
    if (trigger) {
      trigger.addEventListener('click', function() {
        clickCount++;
        clearTimeout(timer);
        
        if (clickCount === 3) {
          window.location.href = "{{ '/hidden/' | relative_url }}";
        }

        timer = setTimeout(() => {
          clickCount = 0;
        }, 2000);
      });
    }
  }
  initSecretTrigger();
  document.addEventListener('pjax:success', initSecretTrigger);
</script>