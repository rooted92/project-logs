# Pokémon App Project Log

## Project Overview
**Project Name**: Pokémon Vanilla  
**Deployed URL**: [Live on Vercel](https://pokemonvanilla.vercel.app)  
**Description**: A simple web app that allows users to browse and search Pokémon, view detailed information about each Pokémon, including evolutions and a random flavor text entry, and enjoy a responsive user interface.

---

## Challenges and Solutions

### 1. **Setting Up Tailwind CSS**
**Problem**: Configuring Tailwind CSS for the project and ensuring it worked with my HTML and JavaScript.
- **Challenge**: Understanding where to put the `tailwind.config.js` and ensuring the `input.css` file generated the correct `output.css`.

**Solution**:
1. Set up the `tailwind.config.js` in the root directory.
2. Created an `input.css` file in the `src` folder and used Tailwind directives (`@tailwind base; @tailwind components; @tailwind utilities;`).
3. Used the following command to build the CSS:
   ```bash
   pnpx tailwindcss -i ./src/input.css -o ./public/css/output.css --watch
   ```
4. Updated the `content` property in the `tailwind.config.js` to:
   ```javascript
   content: [
     "./src/**/*.{html,js}",
     "./public/**/*.{html,js}"
   ]
   ```
5. Verified it by applying utility classes and observing changes in the browser.

**New Skill**: Learned how to configure and build Tailwind CSS manually in a project.

---

### 2. **Relative Pathing Issues**
**Problem**: Navigation between pages and resource loading failed during deployment due to incorrect file paths.
- **Challenge**: Paths like `./pokemon-details.html` didn’t work correctly in certain environments.

**Solution**:
1. Made all paths **relative** (e.g., `./pokemon-details.html?id=5`) to ensure compatibility in different hosting environments.
2. Tested thoroughly with local dev servers like `live-server` and `pnpx serve public` to confirm path correctness.
3. Added `encodeURIComponent` to handle special characters in query parameters.

**New Skill**: Learned the importance of relative paths and how they behave differently in local vs. deployed environments.

---

### 3. **Filtering Pokémon by Search**
**Problem**: Filtering Pokémon based on user input returned inconsistent results or included duplicates.

**Solution**:
1. Used the `.filter()` method to match Pokémon names with the search query.
2. Ensured that typing a blank string (`''`) reset the results by fetching the initial chunk of Pokémon.
3. Applied debouncing to improve performance and prevent multiple API calls:
   ```javascript
   function debounce(func, delay) {
       let timer;
       return function (...args) {
           clearTimeout(timer);
           timer = setTimeout(() => func.apply(this, args), delay);
       };
   }
   ```

**New Skill**: Implemented and understood how debouncing optimizes input-based filtering.

---

### 4. **Fetching and Displaying Pokémon Details**
**Problem**: Pokémon ID (`id`) wasn’t being correctly passed to the details page, leading to 404 errors.

**Solution**:
1. Debugged the issue by logging `window.location.search` and `URLSearchParams` in the console.
2. Ensured the anchor tags (`<a>` elements) used relative paths with the correct `id` parameter:
   ```html
   <a href="./pokemon-details.html?id=${encodeURIComponent(id)}">
   ```
3. Added error handling to the details page to show a friendly error message if `id` is missing.

**New Skill**: Learned how to use `URLSearchParams` and debug issues related to query strings.

---

### 5. **Random Flavor Text with Duplicates**
**Problem**: Flavor text entries included duplicates, and some contained odd characters (e.g., `\n`, `\f`).

**Solution**:
1. Filtered the `flavor_text_entries` array to include only unique English entries:
   ```javascript
   const uniqueEntries = flavorTextEntries.filter((text, index, array) => array.indexOf(text) === index);
   ```
2. Cleaned up entries by replacing unwanted characters with `.replace()`:
   ```javascript
   return entries.map(text =>
       text.replace(/[
]/g, ' ')
           .replace(/…/g, '...')
           .replace(/\s+/g, ' ')
           .trim()
   );
   ```
3. Displayed a random entry on each page load:
   ```javascript
   const randomFlavorText = uniqueEntries[Math.floor(Math.random() * uniqueEntries.length)];
   ```

**New Skill**: Gained experience in cleaning data using JavaScript string methods and working with arrays to remove duplicates.

---

### 6. **Loading Spinner for Better UX**
**Problem**: Loading data dynamically resulted in blank screens for a moment, creating a poor user experience.

**Solution**:
1. Created a loading spinner using SVG and applied it while fetching data:
   ```javascript
   function loadingSpinner() {
       const spinner = document.createElement('div');
       spinner.className = 'flex items-center justify-center h-screen';
       spinner.innerHTML = `
           <svg class="animate-spin h-10 w-10 text-utOrange" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24">
               <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
               <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8v8z"></path>
           </svg>`;
       document.body.appendChild(spinner);
   }
   ```
2. Removed the spinner once the content was ready.

**New Skill**: Improved UX by implementing loading indicators.

---

### 7. **Deploying to Vercel**
**Problem**: Setting up the project for deployment on Vercel.

**Solution**:
1. Ensured all files were in the `public` directory and paths were relative.
2. Configured Vercel:
   - **Framework Preset**: Other
   - **Build Command**: None (static site)
   - **Output Directory**: `public`
3. Verified functionality after deployment and fixed any pathing issues.

**New Skill**: Learned how to deploy static sites using Vercel.

---

## Lessons Learned
1. **Importance of Debugging**:
   - Console logs were essential in identifying issues with query strings and file paths.

2. **Iterating Through Data**:
   - Gained a deeper understanding of array iterator methods (`filter`, `map`, `find`) and when to use them.

3. **Handling Deployment**:
   - Learned to handle relative paths, environment differences, and hosting static assets.

4. **Improving UX**:
   - Loading spinners and error messages significantly improved the user experience.

---

## Next Steps
1. Add tests to validate core functionality (e.g., Pokémon search, detail rendering).
2. Refactor code to improve readability and maintainability.
3. Explore adding features like favorite Pokémon or comparing stats.

---

## Repository
**GitHub Repo**: [pokemon-vanilla](https://github.com/rooted92/pokemon-vanilla)
