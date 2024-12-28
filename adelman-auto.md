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

### 9. **Email Integration: SendGrid to Postmark to Resend**
**Problem**: Initially attempted to use SendGrid for transactional emails but encountered issues with email deliverability and setup. Switched to Postmark, but integration was still cumbersome.

**Solution**: Transitioned to using React-Email with Resend, which streamlined email template creation and delivery.
- Used React-Email to design and render email templates.
- Integrated Resend’s API for sending verification emails.

**New Skill**: Successfully implemented React-Email for modular and reusable email templates with Resend’s reliable email API.

---

### 10. **Database Choice: Supabase to MongoDB**
**Problem**: Initially set up Supabase for handling data storage but found it to be too complex for the project's needs.

**Solution**: Migrated to MongoDB, which was more suited for managing reviews and structured data.
- Used Mongoose to define schemas and handle database interactions.
- Set up a `Review` schema for user-submitted reviews with email verification.

**Schema Definition**:
```typescript
const reviewSchema = new Schema({
  created_at: { type: Date, default: Date.now },
  first_name: { type: String, required: true },
  last_name: { type: String, required: true },
  city: { type: String, required: true },
  review: { type: String, required: true },
  rating: { type: Number, required: true, min: 1, max: 5 },
  email: { type: String, required: true },
  is_verified: { type: Boolean, default: false },
  verification_token: { type: String, required: true, unique: true },
});
```
**New Skill**: Learned to transition from Supabase to MongoDB efficiently and manage database schemas with Mongoose.
---

### 11. **Environment Variables and Production Issues**
**Problem**: On production, the app was fetching data from a default `test` database despite the correct `MONGODB_URI` pointing to `adelman_auto`.

**Solution**:
- Identified that the issue was caused by stale environment variables.
- Deleted and re-added the `MONGODB_URI` environment variable in Vercel.
- Redeployed the app to ensure the new variables were correctly loaded.

**New Skill**: Debugged environment variable issues and verified MongoDB connections in production environments.
---

### 12. **Form Submission and Verification Flow**
**Problem**: Needed a secure way to handle user-submitted reviews with email verification.

**Solution**:
- Implemented a POST endpoint for review submissions:
```typescript
export async function POST(request: NextRequest) {
  const { first_name, last_name, city, review, rating, email } = await request.json();
  const verificationToken = crypto.randomBytes(32).toString('hex');
  const newReview = new Review({
    first_name, last_name, city, review, rating, email, verification_token: verificationToken,
  });
  await newReview.save();
  // Send verification email
}
```
- Created a GET endpoint to handle email verification by updating the `is_verified` field.

**New Skill**: Learned to transition from Supabase to MongoDB efficiently and manage database schemas with Mongoose.
---

## Next Steps
1. Add animations for smoother user interactions.
2. Explore additional backend integrations, such as scheduling APIs for appointments.
3. Improve SEO with dynamic meta tags and structured data.