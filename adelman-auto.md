# Adelman Auto Project Log

## Project Overview
**Project Name**: Adelman Auto Website  
**Deployed URL**: [Live on Vercel](https://adelman-auto.vercel.app/)  
**Description**: A mobile auto repair website showcasing services, reviews, accessibility, and ease of contact. It features a responsive design, Tailwind CSS styling, and integration with external tools like Getform for email submissions.

---

## Challenges and Solutions

### 1. **Issue with Small Icon Size in Embla Carousel**
**Problem**: Icons in the Embla carousel were too small, and applying Tailwind height classes caused the icons to disappear.

**Solution**:
1. Wrapped the icon inside a container and applied a `font-size` class like `text-xl` or `text-2xl` to scale the icon proportionally.
2. Used this code:
   ```tsx
   <i className="icon-[material-symbols--arrow-back-ios-new] text-2xl" role="img" aria-hidden="true"></i>
   ```

**New Skill**: Learned how to manage icon sizing using Tailwind CSS utilities effectively.

---

### 2. **React Slick Installation Errors**
**Problem**: Installing React Slick caused peer dependency errors, and the `react-slick` library was incompatible with React 19.

**Solution**:
1. Uninstalled React Slick and installed Embla Carousel with its auto-scroll plugin:
   ```bash
   pnpm remove react-slick slick-carousel
   pnpm add embla-carousel-react embla-carousel-auto-scroll
   ```

**New Skill**: Identified compatibility issues and migrated to a better-supported library for modern React setups.

---

### 3. **Auto-Scroll Functionality with Embla Carousel**
**Problem**: Needed a continuously auto-scrolling carousel for car brand logos.

**Solution**:
1. Integrated `embla-carousel-auto-scroll` and configured it with the `useEmblaCarousel` hook.
2. Used this implementation:
   ```tsx
   const [emblaRef] = useEmblaCarousel({ loop: true }, [autoScroll({ delay: 3000 })]);
   return (
     <div className="embla" ref={emblaRef}>
       <div className="embla__container">
         {logos.map((logo, index) => (
           <div className="embla__slide" key={index}>{logo}</div>
         ))}
       </div>
     </div>
   );
   ```

**New Skill**: Implemented auto-scrolling carousels with modern React libraries.

---

### 4. **Portrait Image Cropping Issue**
**Problem**: The profile image of Paul Adelman appeared cropped in an undesirable way due to its portrait orientation.

**Solution**:
1. Used `object-cover` with Tailwind's `object-position` utilities:
   ```tsx
   <Image src='/paul-adelman.jpg' alt='Paul Adelman' className='rounded-full object-cover object-top w-40 h-40' />
   ```

**New Skill**: Adjusted image focus and cropping dynamically using utility classes.

---

### 5. **Coverage Component Not Rendering**
**Problem**: The `Coverage` component did not appear in the DOM.

**Solution**:
1. Verified imports and re-exported the `Coverage` component properly.
2. Correctly included it in the `Hero` component:
   ```tsx
   import Coverage from './Coverage';

   const Hero = () => (
     <section>
       <Coverage />
     </section>
   );
   ```

**New Skill**: Debugged rendering issues with Next.js components effectively.

---

### 6. **Accessibility Statement Page Creation**
**Problem**: Needed to draft an accessibility statement for the site.

**Solution**:
1. Created a professional `AccessibilityPage` component in React:
   ```tsx
   const AccessibilityPage = () => (
     <section>
       <h1>Accessibility Statement</h1>
       <p>We are committed to ensuring accessibility for all users...</p>
     </section>
   );
   ```

**New Skill**: Gained experience in writing accessibility statements aligned with WCAG 2.1 standards.

---

### 7. **External Links Accessibility**
**Problem**: External links lacked proper security and accessibility attributes.

**Solution**:
1. Added `rel="noopener noreferrer"` and `aria-label` attributes:
   ```tsx
   <a href="https://www.yelp.com" target="_blank" rel="noopener noreferrer" aria-label="Leave a review on Yelp">Yelp</a>
   ```

**New Skill**: Ensured secure and accessible links for all external references.

---

### 8. **Responsive Design for About Section**
**Problem**: The "About Me" section's layout did not scale well on smaller screens.

**Solution**:
1. Used responsive Tailwind utilities (`md:flex-row`, `flex-col`):
   ```tsx
   <div className="flex flex-col md:flex-row">
     <div>Left Content</div>
     <div>Right Content</div>
   </div>
   ```

**New Skill**: Improved responsiveness using Tailwind's layout utilities.

---

## Next Steps
1. Add animations for smoother user interactions.
2. Explore further backend integrations (e.g., databases for quotes).
3. Improve SEO with dynamic meta tags and structured data.