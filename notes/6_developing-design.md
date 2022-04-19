# Continuation: Figma > Code

## 

- Erase any temporary styles if you included them before.
- Open **global.css**
- Erase everything in the file.
- Add base styles.
    
        @import url("https://fonts.googleapis.com/css?family=Inter:400,600);

        *,  
        *::before,  
        *::after {  
            box-sizing: border-box;  
            margin: 0;  
            padding: 0;  
        }  
        
        img,  
        picture,  
        svg {  
            max-width: 100%;  
            display: block;  
        }  

- Add some root styles:

        :root {
            /* Colors */
            --bkg: 222 47.4% 11.2%;
            --bkg-alt: 226 58.3% 18.8%;
            --text: 226 100% 93.9%;
            --text-alt: 226 22.1% 73.3%;
            --muted: 230 39% 67.8%;
            --white: 255 100% 100%;
            --accent1: 241 76.8% 62.7%;
            --accent2: 330 85.2% 60.4%;
            --accent3: 0 90.6% 70.8%;
            --gradient: linear-gradient(
                94.55deg,
                hsl(var(--accent2)) -4.6%,
                hsl(var(--accent3)) 99.9%
            );
        }
        
        @media (min-width: 768px) {
            html {
                font-size: 130%;
            }
        }

- How to work with the colors using props.

        body {
            background-color: hsl(var(--bkg / 0.6));
        }

    - Now we can easily add opacity.

- Add more styles to the body tag.

        body {
            font-family: "Inter", sans-serif;
            font-weight: 400;
            line-height: 1.55;
            max-width: 2000px;
            margin: 0 auto;
            background-color: hsl(var(--bkg / 0.6));
            color: hsl(var(--text));
        }

- Go into the **index.astro** template and wrap the `<Navbar>, <main>, and <footer>`.

        <div class="wrapper>
            <Navbar />
            <main></main>
            <footer></footer>
        </div>

- Back into the **global.css**

        .wrapper {
            overflow: hidden;
            display: grid;
            grid-template-rows: auto 1fr auto;
            min-height: 100vh;
        }

        main {
            display: grid;
            gap: 3rem;
        }

- Instead of hard coding and createing our own css, we're going to use css OpenProps.

        main {
            display: grid;
            gap: var(--size-fluid-6);
            padding: var(--size-fluid-5) var(--size-fluid-2);
        }

- Add these utility classes:

        .container,
        .container-sm,
        .container-xs {
            width: 100%;
            margin: auto;
        }
        
        .container {
            max-width: 1500px;
        }
        
        .container-sm {
            max-width: 1200px;
        }

        .contiainer-xs {
            max-width: 900px;
        }  

        /* UTILS */

        .text-bkg {
            color: hsl(var(--bkg));
        }
        .text-bkg-alt {
            color: hsl(var(--bkg-alt));
        }
        .text-text {
            color: hsl(var(--text));
        }
        .text-text-alt {
            color: hsl(var(--text-alt));
        }
        .text-muted {
            color: hsl(var(--muted));
        }
        .text-white {
            color: hsl(var(--white));
        }
        .text-accent1 {
            color: hsl(var(--accent1));
        }
        .text-accent2 {
            color: hsl(var(--accent2));
        }
        .text-accent3 {
            color: hsl(var(--accent3));
        }
        .text-gradient {
            color: transparent;
            background: var(--gradient);
            background-clip: text;
        }
        .h1 {
            font-size: var(--font-size-fluid-3);
            font-weight: 600;
            line-height: 1.1;
        }
        .h2 {
            font-size: var(--font-size-fluid-2);
            font-weight: 600;
            line-height: 1.1;
        }
        .h3 {
            font-size: var(--font-size-fluid-1);
            font-weight: 600;
            line-height: 1.1;
        }
        small {
            font-size: var(--font-size-00);
        }

        .grid-sm {
            display: grid;
            place-items: center;
            gap: var(--size-fluid-1);
        }

        .grid-md {
            display: grid;
            place-items: center;
            gap: var(--size-fluid-3);
        }

        .grid-lg {
            display: grid;
            place-items: center;
            align-content: center;
            gap: var(--size-fluid-3);
        }

        .narrow {
            max-width: 80ch;
        }

- Let's style some components now:

        /* Button */

        .btn {
            color: hsl(var(--white));
            text-decoration: none;
            padding: var(--size-2) var(--size-fluid-4);
            border-radius: var(--radius-1);
            cursor: pointer;
        }

        .btn--primary {
            background-color: hsl(var(--accent1));
        }

        .btn--secondary {
            background: var(--gradient);
        }

        .btn--muted {
            background-color: hsl(var(--muted));
        }
        
        .btn--menu {
            background-color: transparent;
            border: none;
            display: grid;
            place-items: center;
            padding-inline: var(--size-2);
        }

        .btn--menu[aria-expanded="true"] + .nav-links {
            transform: translateY(0);
        }

        /* Navbar */

        .nav-container {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: var(--size-fluid-2);
        }

        .nav-links,
        .nav-wrapper {
            display: flex;
            align-items: center;
            gap: var(--size-3);
        }
        
        .nav-links {
            flex-direction: column;
            transform: translateY(-200%);
            position: absolute;
            background-color: hsl(var(--bkg));
            top: var(--size-fluid-5);
            left: 0;
            right: 0;
            text-align: center;
            padding: var(--size-3);
            border-bottom: 2px solid hsl(var(--muted));
        }

        li[role="none"],
        .nav-linkk {
            width: 100%;
            display: block;
            font-size: var(--font-size-1);
        }

        .logo {
            width: calc(var(--size-fluid-8) * 0.75);
        }

- Add media queries

        @media (min-width: 900px) {
            .nav-wrapper {
                gap: var(--size-4);
            }
            .btn--menu {
                display: none;
            }
            .nav-links {
                flex-direction: row;
                position: static;
                transform: translateY(0);
                border: none;
                padding: 0;
                inset: inital;
                background-color: transparent;
            }
            li[role="none"],
            .nav-link {
                width: initial;
                font-size: var(--font-size-0);
            }
        }


- Footer styles

        footer {
            display: grid;
            place-items: center;
            padding: var(--size-2);
            background-color: hsl(var(--bgk));
            color: hsl(var(--text-alt));
        }

        footer::after, 
        footer::berfore {
            height: 100px;
        }

- Create blur component

        .blur {
            position: relative; 
        }

        .blur::after, 
        .blur::before {
            content: '', 
            position: absolute;
            inset: 0;
            z-index: -1;
            filter: blur(35px);
            border-radius: 50% 50% 50%;
            background-color: hsl(var(--accent1) / 0.3);
        }

        .blur::after {
            background-color: hsl(var(--accent1) / 0.2);
            transform: rotate(-20deg);
        }
        .blur::before {
            background-color: hsl(var(--accent2) / 0.2);
            transform: rotate(20deg);
        }

        @media screen and (min-width: 768px) {
            .blur::after, 
            .blur::before {
                filter: blur(120px);
            }
        }


## Create Hero Section

- Go to the **index.astro** and create a **Hero** component.

        ---
        import Hero from '../components/Hero.astro'
        --- 
        <BaseLayout  title="Desgn Landing Page">
            <Hero />
        </BaseLayout>

- Add **Hero.astro** in the **components/** folder.

- Flesh it out.

        <header class="grid-lg">
            <div class="grid-sm>
                <h1 class="h1">Your Kind of Designer</h1>
                <p class="text-muted narrow">
                    lorem25
                </p>
            </div>
            <div class="grid-sm>
                ...
            </div>
        </header>

- Instead of creating the button by hand, we're going to create a component so we can reuse it throughout the site.

        ---
        import Button from './Button.astro';
        --- 

        <div class="grid-sm">
            <Button text="Contact Me" link="#" style="secondary">
        </div>

- Create **Button.astro** in the **/components** folder.

- Remember How to pass data down as props?

        ---
        const { text, link, style } = Astro.props;
        ---

        <a href-{link} class="btn btn--${style}">
            {text}
        </a>

- Back to the **Hero.astro** file

        <div class="grid-sm">
            <Button text="Contact Me" link="#" style="secondary">
            <small class="text-muted">No commitment contact</small>
        </div>

- Add this style for the text in the **Hero section**

        header {
            text-align: center;
        }

- In the **index.astro** file

- We're going to create the SVG section right below the hero.

        <section class="programmer container blur grid=sm">
            <Icon 
                name="programmer" 
                width="400px"
                class="programmer-icon"
                alt="Progammer Picture"
                aria-hidden="true"
            >
        </section>

- Styles for the **programmer section**.

        /* PROGRAMMER SECTION */

        .programmer::after,
        .programmer::before {
            opacity: 0.8;
        }

        .programmer-icon {
            width: var(--size-fluid-9);
            filter: drop-shadow(10px 10px 25px hsl(var(--accent2) / 0.2));
        }

- Challenge: Create your own component out of the **programmer section**.

### Cards sections

- We're going to call this section **"services"**
- Create a component, import it, and inject it into the template.
- Import icons in the component.

We're going to want to loop through some data for this setion, so create a folder called **"data"** with a file called **"services.json"**. 

- Here's the data that goes in that file.

        [
            {
                "icon": "feather:code",
                "name": "Custom Coding",
                "content" : "Vel eget eu vestibulum mauris et ut hendrerit aliquam vel nibh amet, vitae at purus dui semper vel facilisis enim"
            },
            {
                "icon": "feather:users",
                "name": "User Friendly",
                "content" : "Vel eget eu vestibulum mauris et ut hendrerit aliquam iquam vel nibh amet, vitae at purus dui semper vel facilisis enim vel nibh amet, vitae at purus dui semper vel facilisis enim"
            },
            {
                "icon": "feather:search",
                "name": "SEO Optimized",
                "content" : "Vel eget eu vestibulum mauris et ut hendrerit aliquam vel nibh amet, vitae at purus dui semper vel facilisis enim"
            },
            {
                "icon": "feather:trending-up",
                "name": "Built for Growth",
                "content" : "Vel eget eu vestibulum mauris et ut hendrerit aliquam vel nibh amet, vitae at vitae a vitae a purus dui semper vel facilisis enim"
            },
            {
                "icon": "feather:smartphone",
                "name": "Ready for Mobile",
                "content" : "Vel eget eu vestibulum mauris et ut hendrerit aliquam vel nibh amet, vitae at purus dui semper vel facilisis enim"
            },
            {
                "icon": "feather:home",
                "name": "Feels like you",
                "content" : "Vel eget eu vestibulum mauris et ut hendrerit aliquam vel nibh amet, vitae at purus dui semper vel facilisis enim"
            }
    ]

- Import data

        ---
        import data from '../data/services.json'
        ---

        <section class="services container-sm">
            <h2 class="sr-only>
                Services
            </h2>
            {
                data.map(service => (
                    <div class="service">
                        <div class="service--icon text-white>
                           <Icon
                                name={service.icon}
                                width="30"
                            />
                            <h3>
                                {service.name}
                            </h3>
                            <p class="text-muted">
                                {service.content}
                            </p>
                        </div>
                    </div>
                ))
            }
        </section>
    

- Now we have to style the services

        .sr-only {
            position: absolute;
            width: 1px;
            height: 1px;
            margin: -1px;
            overflow: hidden;
            clip: rect(0, 0, 0, 0);
            white-space: nowrap;
            border-width: 0;
        }

        .narrow {
            max-width: 80ch;
        }

        .services {
            display: flex;
            flex-wrap: wrap;
            align-items: start;
            gap: var(--size-fluid-3);
        }

        .service {
            flex; 1 1 300px;
            display: grid;
            gap: var(--size-2);
        }

        .service--icon {
            background-color: hsl(var(--muted));
            justify-self: start;
            padding: clamp(0.6rem, 3vw, 0.8rem);
            border-radius: 50%;
        }

        .service--icon svg {
            width: var(--size-fluid-2);
        }
