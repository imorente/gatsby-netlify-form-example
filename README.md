# Integrating Netlify Form Handling in Gatsby

Example for integrating a basic contact form with Netlify’s form handling feature (based on the [default Gatsby starter](https://github.com/gatsbyjs/gatsby-starter-default))

Demo: https://gatsby-form-example.netlify.com

## Deploy

[![Deploy to Netlify](https://www.netlify.com/img/deploy/button.svg)](https://app.netlify.com/start/deploy?repository=https://github.com/imorente/gatsby-netlify-form-example)

## reCAPTCHA

This example site uses [react-google-recaptcha](https://github.com/dozoisch/react-google-recaptcha) to render the reCAPTCHA widget.

To make the reCAPTCHA example work in your own copy of this site, you’ll need to do the following:
1. [Sign up for a reCAPTCHA API key pair](http://www.google.com/recaptcha/admin) for your site.
2. [Log in to your Netlify account](https://app.netlify.com), and add the following
environment variables to your site’s Settings > Build & deploy > Build environment variables:
  - `SITE_RECAPTCHA_KEY` with your reCAPTCHA site key.
  - `SITE_RECAPTCHA_SECRET` with your reCAPTCHA secret key.

**Important**: the environment variables need to be called `SITE_RECAPTCHA_KEY` and `SITE_RECAPTCHA_SECRET` for the Netlify backend to find them. If you add a `GATSBY_` prefix to the variable names, the Netlify backend won't recognize them, the reCAPTCHA verification will fail, and your form submissions won't be stored.

3. Change the build command for your site to
```
echo SITE_RECAPTCHA_KEY=$SITE_RECAPTCHA_KEY >> .env.production && gatsby build
```
This will make the SITE_RECAPTCHA_KEY available to the Gatsby build in production.

To see the reCAPTCHA widget locally, add `SITE_RECAPTCHA_KEY=your-reCAPTCHA-API-site-key`
to your local [.env.development](https://www.gatsbyjs.org/docs/environment-variables/) file.

## Troubleshooting

### Forms stop working after upgrading to Gatsby v2
This can be caused by the offline-plugin. [Workaround](https://github.com/gatsbyjs/gatsby/issues/7997#issuecomment-419749232) is to use `?no-cache=1` in the POST url to prevent the service worker from handling form submissions (Thanks to [@phmu_office](https://twitter.com/phmu_office/status/1047810173417472000) for the heads up ✨)
