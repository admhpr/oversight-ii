<template>
  <main>
      <ContentSearch path="articles"/>
      <nav>
          <ContentNavigation v-slot="{ navigation }">
          <ul>
              <li v-for="link of navigation" :key="link._path">
              <NuxtLink :to="link._path">{{ link.title }}</NuxtLink>
              </li>
          </ul>
          </ContentNavigation>
      </nav>
      <ContentDoc />
      <ContentList path="/articles" v-slot="{ list }">
          <div v-for="article in list" :key="article._path">
          <h2>{{ article.title }}</h2>
          <p>{{ article.description }}</p>
          </div>
      </ContentList>
  </main>
</template>