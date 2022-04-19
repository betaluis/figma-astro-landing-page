# Structure & Components

Everything you're going to use to build the site is going to be in the "src/" folder. 

Any pages placed in the "pages/" folder with the `.astro` extension will have its own route.

Astro docs recommend to create a folder called "layouts" in the "src/" folder.

- Download extension called "Astro"
- Create folder "layouts"
- Create "BaseLayout.astro"
    - Template for any page on this site.
- Delete everyting in "index.astro"
- Copy the default template into the `BaseLayout` component.

        <html lang="en">
        <html>
            <head>
                <meta charset="UTF-8">  
                <meta name="viewport" content="width=device-width">
                <title>{title}</title>
                <link rel="icon" type="image/x-icon" href="/favicon.ico" />
                <link 
                    rel="stylesheet"
                    href="{Astro.resolve("../styles/global.css")}
                >
            </head>
            <body>
                 <main> 
                    
                </main>
            </body>
        </html>

- Import BaseLayout into `index.astro`.

        ---
        import BaseLayout from '../layouts/BaseLayout.astro'
        ---

        <BaseLayout>
        </BaseLayout>

- Add a title prop.

        import BaseLayout from '../Layouts/BaseLayout.astro';
        
        <BaseLayout title="Desgn Landing Page">
        </Baselayout>

- How do you grab the title prop in the "BaseLayout"?

        // At the top of the file.
        ---
        const { title } = Astro.props;
        ---

- You could event give it a default title like so:

        ---
        const { title = "This is a page title" } = Astro.props;
        ---

- Add a `<slot />` to add content inside of the BaseLayout from other pages.

        <body>
            <main> 
                <slot />        
            </main>
        </body>


## Building Footer Component

- Add a footer tag to the layout.

        <body>
            <main>
                <slot />
            </main>
            <footer class="blur">
                <small>
                    Copyright &copy; 
                    <span id="copyrightYear"></span>
                </small>
            </footer>
        </body>

- Grab the `copyrightYear` id and give it a `new Date()`:

        <footer class="blur">
            <small>
                Copyright &copy;
                <span id="copyrightYear"></span>
            </small>
        </footer>
        <script>
            document.querySelector('#copyrightYear')
                .textContent = new Date().getFullYear();
        </script>

    - This is one of the ways to use JavaScript in "Astro".


## Building Navbar Component

- First you'll want to import the named component to the `index.astro`.

        ---
        import Navbar from '../components/Navbar.astro';
        const { title } = Astro.props; 
        ---

- Create `Navbar.astro` under "components/".

- Inject the component in the `index.astro` template.

        <body>
            <Navbar />
            <main></main>
            <footer></footer>
        </body>

- In the **Navbar.astro** file, import icon.

        ---
        import Icon from 'astro-icon';
        ---

- You can also pull data from an array in Astro.

        ---
        import { Icon } from 'astro-icon';
        const navLinks = [
            {
                name: "Home",
                url: "/",
                style: "transparent",
            },
            {
                name: "Pricing",
                url: "#",
                style: "transparent",
            },
            {
            {
                name: "About",
                url: "#",
                style: "transparent",
            },
                name: "Contact Me",
                url: "#",
                style: "primary",
            },
        ]
        ---

- Create **icons** folder in the **src/**

    - Now we can jsut add .svg icons in this folder. 
    - Export icons from figma and place them in this folder.

- Continue building out the navbar and add the logo.

        <nav>
            <div class="container nav-container">
                <Icon name="logo" width={225} class="logo" />
            </div>
        </nav>

- Adding navbar links.
    
        <nav>
            <div class="container nav-container">
                <Icon name="logo" width={225} class="logo" />
                <div class="nav-wrapper">
                    <button 
                        class="btn btn--menu" 
                        id="menu-btn" 
                        arai-expanded="false" 
                        aria-label="Open mobile nav"
                    >

                    </button>
                    <ul>
                        
                    </ul>
                </div> 
            </div>
        </nav>

- At this point we can add another "menu" icon from one of the packs that "astro-icons" offers. (Still working in the navbar but scoping it down for readability)  
    - You get the icons from [here](https://www.icones.js.org).
        - Search for "Feather Icons"
        - Search for "menu"
        - Copy it and place it in our code. <br /> <br />
- Same syntax even though it's not a local icon.

        <button 
            class="btn btn--menu" 
            id="menu-btn" 
            arai-expanded="false" 
            aria-label="Open mobile nav"
        >
            <Icon name="feather:menu" width={25} />
        </button>

- Let's continue on to the `<ul>`.
- Now we get to map through the data that we added at the top of this file.

        <ul class="nav-links" role="navigation">
            {
                navLinks.map(link => () (
                    <li role="none">
                        <a href={link.url} 
                            class="btn btn--${link.style} 
                            nav-link"
                        > 
                        {link.name}
                        </a>
                    </li>
                ))
            }
        </ul>

- Create a script at the bottom of the file.

        <script>
            const navBtn = document.querySelector('#menu-btn');
        </script>

- Add event listener and check if **aria-expanded** is true or false.

        <script>
            const navBtn = document.querySelector('#menu-btn');
            
            navBtn.addEventListener('click', () => {
                navBtn.setAttribute('aria-expanded', 
                    navBtn.getAttribute('aria-expanded') === 'false' ?
                        'true' : 'false');
            })
        </script> 


    - The event listener is a click event.
    - Whenever the navBtn is clicked, which is the menu button, it will set the **aria-expanded** attibute to either true or false, but this is based on a condition. 
    - If the **aria-expanded** is "false" then it will set it to "true", and vice versa. This is accomplished above using a ternary conditional.
    - We can use this to style the mobile navigation.