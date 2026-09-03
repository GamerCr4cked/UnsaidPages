---
layout: default
title: UnsaidPages
---

<div class="home-header">
  <h1>Unsaid<span>Pages</span></h1>
  <p>Stories that were felt, not just written.</p>
</div>

<div class="category-grid">

  <a href="{{ '/stories' | relative_url }}" class="category-card">
    <span class="cat-icon">📖</span>
    <h2>Stories</h2>
    <p class="cat-desc">Real feelings, fictional people. Hinglish stories that hit where it hurts.</p>
    <span class="cat-count">{{ site.pages | where: "layout", "story" | where_exp: "item", "item.translation != true" | size }} Stories</span>
  </a>

  <div class="category-card coming-soon-card">
    <span class="cat-icon">🔮</span>
    <h2>Coming Soon</h2>
    <p class="cat-desc">Nayi kahaniyan jald hi aayengi…</p>
    <span class="cat-count">Stay Tuned</span>
  </div>

</div>

<div class="recently-read-section" id="recentlyRead" style="display:none;">
  <h2 class="section-title">Recently Read</h2>
  <div class="recently-read-list" id="recentlyReadList"></div>
</div>

<script>
(function() {
  var history = JSON.parse(localStorage.getItem('readingHistory') || '[]');
  if (!history.length) return;
  var section = document.getElementById('recentlyRead');
  var list = document.getElementById('recentlyReadList');
  var baseUrl = '{{ "/" | relative_url }}stories/';
  section.style.display = '';
  list.innerHTML = history.map(function(h) {
    var ago = (function(t) {
      var m = Math.floor((Date.now() - t) / 60000);
      if (m < 1) return 'Just now';
      if (m < 60) return m + 'm ago';
      var hr = Math.floor(m / 60);
      if (hr < 24) return hr + 'h ago';
      return Math.floor(hr / 24) + 'd ago';
    })(h.time);
    return '<a href="' + baseUrl + h.slug + '" class="recent-item">' +
      '<span class="recent-title">' + h.title + '</span>' +
      '<span class="recent-time">' + ago + '</span>' +
      '</a>';
  }).join('');
})();
</script>
