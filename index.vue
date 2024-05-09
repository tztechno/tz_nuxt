<template>
  <div>
    <header>
      <hr>
      <h1>My Apps</h1>
      <hr>
    </header>

    <main>
      <!-- サイドバー -->
      <div class="sidebar">
        <h2>Sidebar</h2>
        <li><nuxt-link to="https://tztechno.github.io/tz_js_20240217_leaflet/emap_now4.html"> Recent Earthquake </nuxt-link></li>
        <li><nuxt-link to="https://app-tarrot-reading-mlnessbppgllzg2dns5pfc.streamlit.app"> Tarot Rreading </nuxt-link></li>
        <li><nuxt-link to="https://app-tags-remover-sbkxegmeb9kavsurgowb6d.streamlit.app/"> Tags Remover </nuxt-link></li>
      </div>

      <hr>
      <section id="main-content">
        <article>
          <li><nuxt-link to="https://tztechno.github.io/tz_js_20240217_leaflet/emap_now4.html"> Recent Earthquake </nuxt-link></li>
          <p>Displays earthquakes that occurred around Japan in the past month, color-coded by magnitude. Large earthquakes often occur within the range of earthquake swarms, so by checking this, you can find out the danger range.</p>

          <li><nuxt-link to="https://app-tarrot-reading-mlnessbppgllzg2dns5pfc.streamlit.app"> Tarot Rreading </nuxt-link></li>
          <p>You can do tarot reading by yourself. Cards predict your past, present, and future.</p>

          <li><nuxt-link to="https://app-tags-remover-sbkxegmeb9kavsurgowb6d.streamlit.app/"> Tags Remover  </nuxt-link></li>
          <p>Remove unnecessary line breaks, tabs, and spaces hidden in your text. Please use it when copying and pasting sentences.</p>
        </article>
      </section>
    </main>

    <footer>
      <hr>
      <p>2024 My Apps</p>
      <hr>
    </footer>
  </div>
</template>