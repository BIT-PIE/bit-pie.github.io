# BIT-PIE

## Project Setup

```sh
npm install
```

### Compile and Hot-Reload for Development

```sh
npm run dev
```

### Compile and Minify for Production

```sh
npm run build
```

### How to update the content

- Update Teaser

  1. Put the new teaser image in `public/images/` directory.
  2. Change the `teaserLink` in `src/App.vue` to the new image path.

- Update News

  1. Edit the `src/js/news.js` file to add or modify news items.

- Update Team
  
  1. Edit the `src/js/team.js` file to add or modify team members.
  2. Ensure that each member has an avatar image in the `public/images/people/` directory. Using the member's name as the filename is recommended. Compress the image below 300KB for optimal performance.

- Update Publications

  1. Edit the `src/js/publications.js` file to add or modify publications. The publication is presented in the order of the list in the file.

- Update Photos

  1. Put the new photo in `public/images/lab/` directory.
  2. Edit the `src/js/photos.js` file to add or modify photo entries. Using `lab-YYMMDD-NUM` as the filename is recommended, where `YYMMDD` is the date and `NUM` is a number starting from 1, e.g., `lab-240101-01.jpg`. Compress the image below 600KB for optimal performance.
