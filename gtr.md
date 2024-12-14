# GTR Mobile Fleet Repair Website Project Log

## Project Overview
**Project Name**: GTR Mobile Fleet Repair Website  
**Deployed URL**: [Live on Vercel](https://gtr-website.vercel.app/)  
**Description**: A professional landing page for GTR Mobile Fleet Repair, featuring a clean, minimalist design that highlights services, contact options, and coverage areas. Built with Next.js, React, Tailwind CSS, and TypeScript.

---

## Challenges and Solutions

### 1. **Defining a Color Palette and Layout**
**Problem**: Creating a cohesive and visually appealing design that aligned with the business's needs.  
- **Challenge**: Using a dark background while ensuring accessibility and readability.  

**Solution**:
1. Defined a modern, accessibility-friendly color palette with shades of black, white, gray, and purple.
2. Used Tailwind CSS utility classes for consistent spacing, typography, and gradients.
3. Tested on different devices to maintain responsiveness and readability.

**New Skill**: Enhanced understanding of designing for accessibility and working with custom Tailwind CSS configurations.

---

### 2. **Interactive Google Maps Integration**
**Problem**: Showcasing multiple counties served by the business.  
- **Challenge**: Highlighting specific areas while balancing simplicity and performance.  

**Solution**:
1. Embedded a dynamic Google Map using the `iframe` method to show Sonoma and Napa counties.
2. Explored the Google Maps JavaScript API for potential future interactive features, like highlighting service areas with polygons or circles.

**New Skill**: Gained familiarity with embedding and customizing Google Maps.

---

### 3. **Dynamic Breadcrumb Navigation**
**Problem**: Providing intuitive navigation for deeper pages like "Accessibility."  
- **Challenge**: Replacing "Back to Home" buttons with a more elegant breadcrumb system.

**Solution**:
1. Built a breadcrumb component using Next.js's `useRouter` to dynamically display the navigation path.
2. Styled the breadcrumb with Tailwind CSS for a clean, user-friendly interface.

**New Skill**: Improved skills in dynamic routing and user-friendly navigation patterns in Next.js.

---

### 4. **Optimizing Call-to-Action Buttons**
**Problem**: Ensuring users could quickly contact the business, regardless of their device.  
- **Challenge**: Designing a mobile-first approach while maintaining usability on desktop.

**Solution**:
1. Added a sticky "Call Now" button for mobile users.
2. Ensured accessibility and responsiveness by testing on both mobile and desktop environments.
3. Styled the button with a gradient background (`bg-gradient-to-r`) for visual emphasis.

**New Skill**: Learned to prioritize CTAs for mobile-first design and improve user engagement.

---

### 5. **Accessibility Features**
**Problem**: Ensuring the website meets accessibility standards.  
- **Challenge**: Providing an accessible experience while maintaining design consistency.

**Solution**:
1. Added an Accessibility Statement link to the footer.
2. Used Tailwind CSS utility classes like `sr-only`, `focus:outline-none`, and `hover:` styles to improve usability for all users.
3. Ensured sufficient color contrast for all text and backgrounds.

**New Skill**: Integrated accessibility best practices into a modern web design.

---

### 6. **Custom Footer Design**
**Problem**: Including links and credits in a clean, non-intrusive way.  
- **Challenge**: Highlighting "Accessibility" and "Website by [Your Name]" while keeping the footer minimal.

**Solution**:
1. Added an "Accessibility" link and a credit link to the footer with hover effects (`hover:text-lg`) for interactivity.
2. Styled the footer using Tailwind CSS for simplicity and responsiveness.

**New Skill**: Improved skills in creating minimalist, user-friendly footers.

---

## Lessons Learned
1. **Prioritizing Usability**:
   - Focused on quick access to key actions, like contacting the business, especially on mobile devices.

2. **Responsive Design**:
   - Balanced mobile-first principles with a professional desktop layout.

3. **Accessibility Awareness**:
   - Integrated accessibility-friendly features and created a dedicated Accessibility Statement page.

4. **Dynamic Navigation**:
   - Used breadcrumbs to improve navigation and replace traditional back buttons.

---

## Next Steps
1. Add a form for service quotes or scheduling (integrated with a third-party service or custom backend).
2. Highlight certifications and reviews to build trust with potential clients.
3. Implement basic SEO optimizations for search visibility.
4. Explore interactive Google Maps with custom polygons for highlighting service areas.