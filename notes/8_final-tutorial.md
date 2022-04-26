# Final Section (Pricing)

- Make another component called Pricing. 
- Make a file in /data called "pricing.js"
- Copy the data below in that file.

          const pricingData = [
        {
          price: "$1000",
          plan: "Starter Plan",
          description: "Landing page to maximize conversion rate",
          details: [
            "Custom Branding",
            "Single Landing page",
            "SEO-optimized",
            "One Email inbox",
            "Contact Form",
          ],
          button: {
            text: "Learn more",
            url: "#",
            style: "muted",
          },
          subtext: "$500 up front + $500 upon completion",
        },
        {
          price: "$1400",
          plan: "Pro Plan",
          description: "Personalized site to showcase your brand",
          details: [
            "Starter Plan+",
            "Up to 5 pages",
            "Social feed integrations",
            "CMS for custom content",
            "Custom analytics",
          ],
          button: {
            text: "Sign up",
            url: "#",
            style: "secondary",
          },
          subtext: "$700 up front + $700 upon completion",
          featured: true,
        },
        {
          price: "$2000",
          plan: "Writer’s Plan",
          description: "Personalized site with accompanying blog",
          details: [
            "Pro Plan+",
            "Full-featured blog",
            "Search functionality",
            "Two email inboxes",
            "Free domain name (1 year)",
          ],
          button: {
            text: "Learn more",
            url: "#",
            style: "muted",
          },
          subtext: "$1000 up front + $1000 upon completion",
        },
      ];

      export default pricingData;

- Pull in the data into the pricing component just like you would a JSON.
- Import Icon from astro
- Create a section.
- Create a div with an `h2` and a `p` inside of it.
  - h2 = A price for everyone.
  - p = Three tiers to meet your needs.


## Now we're going to loop through the cards

- Below the grid div create another div.pricing-container.container-sm.blur
- Map through the data.
- For each card create a div.pricing-card.${card?.featured && featured}.grid-sm
- anohter div inside of it.
- A paragraph in side of that div. p.pricing-card-price with content {card.price}
- h3 below it with classes pricing-card-pill and "h3". Content = {card.plan}
- Under the `div` with the `h3 and p` inside of it, create another paragraph.
  - class = pricing-card-description, text-muted
  - content = {card.description}
- Now create a `<ul>`
  - class = pricing-card-feature-container
- In this list we're going to map through the features.
- return an `<li>`
  - class = pricing-card-feature
- Check if the card has a featured property. Use ternary. 
  - If it does...`<Icon>`
    - name = feather:check-circle
    - width = 24
    - class = text-accent2 or text-alt
- Also create a span for some text inside of the `<li>`
  - The span's content = {feature}
- Now we need to pull down our button component. (import)
  - text={card.button.text}
  - link={card.button.url}
  - style={card.button.style}
- Create a small tag under button
  - class = text-muted
  - content = {card.subtext}
- Styles:

      /* Pricing */

      .pricing-wrapper {
        display: grid;
        gap: var(--size-fluid-5);
      }

      .pricing-container {
        display: flex;
        flex-wrap: wrap;
        gap: var(--size-3);
        align-items: center;
        justify-content: center;
      }

      .pricing-container::before,
      .pricing-container::after {
        inset: 15%;
      }

      .pricing-card {
        padding: var(--size-3) var(--size-5);
        border: 1px solid hsl(var(--text-alt));
        background-color: hsl(var(--bkg));
      }

      .pricing-card.featured {
        border-color: hsl(var(--accent2));
        position: relative;
      }
      .pricing-card.featured::before {
        content: "Most Popular";
        position: absolute;
        top: calc(var(--size-fluid-1) * -.05);
        transform: translateY(-50%);
        background: var(--gradient);
        font-size: var(--font-size-00);
        text-transform: uppercase; 
        text-align: center;
        border-radius: var(--size-2);
        padding: 0 var(--size-2);
      }

      /* Media Query */

      @media screen and (min-width: 1167px) {
        .pricing-card.featured {
          transform: scale(1.15);
          border: 4px solid hsl(var(--accent2));
          padding: var(--size-5) var(--size-6);
          margin: 2rem 0;
        }
      }


      .pricing-card-price {
        font-size: var(--size-fluid-2);
        font-weight: bold;
        text-align: center;
      }
      .pricing-card-pill {
        background-color: hsl(var(--text-alt));
        color: hsl(var(--bkg));
        text-transform: uppercase;
        text-align: center;
        font-size: var(--font-size-00);
        border-radius: var(--size-2);
        padding: 0 var(--size-2);
      }
      .pricing-card-description {
        font-size: var(--font-size-0);
        text-align: center;
      }
      .pricing-card-feature-container {
        list-style: none;
        font-size: var(--font-size-0);
        display: grid;
        gap: var(--size-2);
        margin-bottom: var(--size-2);
      }

      .pricing-card-feature {
        display: flex;
        gap: var(--size-2);
      }

## Client section

- Create component called Clients
- Pass in some data at the top of the file as a javascript array with the icons that we're going to be using.

        const data = [
          {
            "icon" :"simple-icons:amd",
            "alt" :"AMD Logo",
          },
          {
            "icon" :"simple-icons:500px",
            "alt" :"500 Logo",
          },
          {
            "icon" :"simple-icons:abbvie",
            "alt" :"Abbvie Logo",
          },
          {
            "icon" :"simple-icons:bbc",
            "alt" :"BBC Logo",
          },
          {
            "icon" :"simple-icons:astonmartin",
            "alt" :"Aston Martin Logo",
          },
          {
            "icon" :"simple-icons:asda",
            "alt" :"Asada Logo",
          },
        ]

- Create a `<section>`
  - class = clients grid-sm
  - `<h2 class="h3 clients--heading">`
    - content = Happy Clients
- Icons come from icones.js.org
  - simple icons
- create a div.client-logo-container
- Map through the data.
- Return an Icon component with a...
  - name={i.icon}
  - width="120"
  - height="85"
  - class=client-logo text-muted
  - alt={i.alt}
- Next, just style.
        
        /* Clients */

        .clients--heading {
          font-weight: normal;
        }
        .client-logo-container {
          display: flex;
          flex-wrap: wrap;
          justify-content: center;
          gap: 0 var(--size-fluid-3);
        }
        .client-logo {
          flex: 0 1 var(--size-fluid-5);
        }

## Contact section

- Create and import component called CTA
- Import Button
- header = section
- h2 = class of h2 content = Let us tell your story
- less text
- Styles: