<template>
  <div>
    <b-navbar toggleable="lg" type="dark" variant="info">
      <b-navbar-brand>Nuxt Diary App</b-navbar-brand>

      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>
      <b-collapse id="nav-collapse" is-nav>
        <b-navbar-nav>
          <b-nav-item :route="{path: '/posts'}">posts list</b-nav-item>
          <no-ssr>
            <b-nav-item :route="{path: '/'}">
              <span>login</span>
            </b-nav-item>
          </no-ssr>
          <b-nav-item right :route="{path: 'posts/new'}">
            add post
          </b-nav-item>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
  </div>
</template>