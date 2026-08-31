# Break Your Own Site

## Live Portfolio

https://minaibrahim.tech

## Goal

I deliberately tested my portfolio beyond the happy path to find real weaknesses before launch.

## Where It Breaks

### 1. Invalid Email

**Test:**
Entered an invalid email such as `abc`.

**Result:**
The browser correctly blocked submission and asked for a valid email.

**Triage:**
Passed. No fix required.

---

### 2. Garbage Name and Message

**Test:**
Submitted values such as:

- Name: `@@@`
- Message: `!!!!!`

**Before:**
The form accepted the submission.

**Triage:**
Fix-now.

**Fix:**
I added client-side validation that requires:

- a name containing real letters
- a meaningful message of at least 10 characters
- non-empty trimmed values

**After:**
Garbage submissions are blocked with clear validation messages.

---

### 3. Rapid Double Submission

**Test:**
Filled the form correctly and tried to press Send twice very quickly.

**Result:**
The submit button became disabled while the request was being sent.

Only one submission reached my inbox.

**Triage:**
Passed. No fix required.

---

### 4. Cross-Browser Check

I tested the live portfolio using:

- Chrome
- Samsung Internet

The site layout, scrolling, navigation, and contact form worked correctly in both.

**Triage:**
Passed. No fix required.

---

### 5. Link Audit

I manually checked the main portfolio links, including:

- Book a Call
- ORCID
- Hotel 1000
- Download CV
- ResearchGate
- GitHub repositories
- TensorFlow links

The tested links opened successfully.

**Triage:**
Passed. No broken primary link was found.

## SEO and Social Metadata

The site already had basic SEO metadata including:

- page title
- description
- keywords
- author
- robots
- Open Graph title and description
- Twitter card metadata

During this hardening pass I added:

- canonical URL
- Open Graph URL
- Open Graph image
- Open Graph image alt text
- Twitter social-preview image

This completed the basic social-share metadata using the existing portfolio preview image.

## Speed Check

I ran Google PageSpeed Insights on the live site.

### Mobile

- Performance: 86
- Accessibility: 100
- Best Practices: 100
- SEO: 100
- Total Blocking Time: 0 ms
- Cumulative Layout Shift: 0
- Largest Contentful Paint: 3.2 s

### Desktop

- Performance: 99
- Accessibility: 100
- Best Practices: 100
- SEO: 100
- First Contentful Paint: 0.8 s
- Largest Contentful Paint: 0.8 s
- Total Blocking Time: 0 ms
- Cumulative Layout Shift: 0

## Performance Finding

PageSpeed identified that the profile image did not have explicit width and height attributes.

**Triage:**
Fix-now.

**Fix:**
I added explicit dimensions to the profile image to improve image layout information for the browser.

Other recommendations such as additional cache optimization, render-blocking-request reduction, and unused JavaScript reduction were classified as optimization opportunities rather than launch-blocking failures.

## Findability

I checked the site's search visibility.

The site now has strong basic on-page SEO and receives a Lighthouse SEO score of 100.

However, search-engine indexing and ranking are not instant.

### Known Limitation

The portfolio may not appear immediately for every search query because indexing and ranking are controlled by external search engines and can take time.

This is documented as a known limitation rather than hidden or treated as a functional failure.

## Triage Summary

### Fix-Now

1. Garbage name/message submissions were accepted.
   - Fixed with stronger form validation.

2. Social-share metadata was incomplete.
   - Added canonical URL, Open Graph URL/image, image alt text, and Twitter image.

3. Profile image lacked explicit dimensions.
   - Added explicit width and height.

### Known Limitations

1. Search-engine indexing and ranking may take time.

2. Remaining PageSpeed recommendations are performance optimization opportunities, not current functional failures.

## Hardening Review

After completing the fixes, I sent the hardened portfolio and the "where it breaks" list to another person for review.

The reviewer said:

1. There were no additional must-fix issues and the fixes looked good.
2. Everything looked good from their perspective.
3. The site appeared ready to launch.

I did not defend the existing implementation or create artificial problems after the review.

No new must-fix was identified.

## Result

The portfolio was tested beyond the happy path, real weaknesses were found and fixed, known limitations were documented, SEO/social metadata was completed, speed was measured, cross-browser behavior was checked, links were audited, and a final hardening review found no remaining launch-blocking issue.

Live site:

https://minaibrahim.tech
