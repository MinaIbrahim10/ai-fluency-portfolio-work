# Make It Do Something

## Live Feature

I added one dynamic feature to my portfolio: a working contact form.

Live site:
https://minaibrahim.tech

The form sends real submissions through Formspree and forwards them to my email inbox.

## Plain-Words Explainer

A backend is the part of a web application that handles data and actions behind the page. My portfolio itself is hosted as a frontend, so the contact form needs an external service to receive and process submissions.

When someone fills in their name, email, and message and clicks Send Message, the React form sends that data to my Formspree endpoint. Formspree acts as the backend: it receives the submission, processes it, and forwards it to my email. The visitor then sees a success message on the website.

So the data flow is:

visitor → contact form → Formspree backend → my inbox

The main thing I learned is that the form visible on the page is only the frontend. Something still has to receive the submitted data and do something with it, and in this case Formspree provides that backend service.

## End-to-End Test

I submitted a real test message through the live form on minaibrahim.tech.

The submission reached my inbox through Formspree, confirming that the feature works end to end.
