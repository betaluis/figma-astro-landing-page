# Infinite Slider

- Create a component called **Reviews** 
- Add some data in the **data/** folder.
- Name it "reviews.json" and add this:

        [
            {
                "name": "John Doe",
                "content": "iquam vel nibh amet, vitae at purus dui semper vel facilisis enim",
                "avatar": "/assets/avatar-1.jpeg",
                "active": true
            },
            {
                "name": "Christian Jones",
                "content": "iquam vel nibh amet, vitae at purus dui semper vel facilisis enim",
                "avatar": "/assets/avatar-2.jpeg"
            },
            {
                "name": "Clarence Robinson",
                "content": "iquam vel nibh amet, vitae at purus dui semper vel facilisis enim vel facilisis enim",
                "avatar": "/assets/avatar-3.jpeg"
            },
            {
                "name": "Kathleen Alday",
                "content": "iquam amet, vitae at purus dui semper vel facilisis enim",
                "avatar": "/assets/avatar-4.jpeg"
            },
            {
                "name": "Tina Givens",
                "content": "iquam vel nibh amet, vitae at purus enim enim dui semper vel facilisis enim",
                "avatar": "/assets/avatar-5.jpeg"
            }
        ]

- Make sure you go to this [link](https://www.uifaces.co/browse-avatars) and get the images you want. x
- Drop the images into the **public/assets/** folder. 
- The images have to be named according to the data above.
- Import the data.

### Another way we can reference scripts in Astro is by doing the following:

- Create a reviews.js file in the **src/js/** directory.

        console.log("I'm a script");

- Go back to **Reviews.astro** and place the following at the bottom of the file.

        <script src={Astro.resolve('../js/reviews.js')} hoist type="module"></script>
        
- Now to flesh out the reviews section:

        <section class="reviews-wrapper blur container-sm>
            <h2 class="sr-only">Reviews</h2>
            <div class="reviews-container container-xs>
                <button 
                    class="reviews-btn grid-sm reviews-btn--prev" 
                    id="prev" 
                    aria-label="Previous Review"
                >
                    <Icon 
                        name="feather:chevron-left" 
                        width="50" 
                    />
                </button>
                <div class="reviews">
                    // ........... reviews go here.
                </div>
                <div class="indicator-container">
                    ...
                </div>
                <button 
                    class="reviews-btn grid-sm reviews-btn--next"
                    id="next"
                    aria=label="Next Review"
                >
                    <Icon 
                        name="feather:chevron-right"
                        width="50"
                    />
                </button>
            </div>
        </section>

- Map through the data inside the **indicator-container**.
- This is going to be the dots at the bottom that indicate where we are in the reviews slider. 

        <div class="indicator-contiainer">
            {
                data.map((review) => (
                    <button class="indicator ${review?.active && 'active'}"></button>
                ))
            }
        </div>

- Inside the `<div class="reviews">` : 

        <div class="reviews">
            { 
                data.map(review => (
                    <div class="review grid-sm">
                        <img src={review.avatar}
                             alt={review.name}
                             class="review-avatar"
                        >
                        <p class="review-content">{review.content}</p>
                        <p class="review-content text-gradient h3">{review.name}</p>
                    </div>
                ))
            }
        </div>

- We need to do some duplication of the first and last image in the slider.
- Copy the `{ data.map... }` and duplicate it both above and below.
- Now slice the first one to duplicate the first image:

        {
            data.slice(data.length - 1).map(review => (
                ...same as previous code.
            ))
        }
- Slice the third one to duplicate the last image:

        {
            data.slice(0,1).map(review => (
                ...same as the code above.
            ))
        }

- This will make more sense as we work through the CSS.
- Let's do that now:

        /* REVIEWS */

        .reviews-wrapper {
            background-color: hsl(var(--bkg));
        }

        .reviews-wrapper::after,
        .reviews-wrapper::before {
            inset-inline: 20%;
        }

        .review-container {
            overflow: hidden;
            position: relative;
            width: calc(100vw - var(--size-fluid-2));
            background-color: hsl(var(--bkg));
        }

        .reviews {
            display: flex;
            margin: var(--size-fluid-4) 0 var(--size-fluid-5);
            transform: translateX(-100%);
            transition: transform 300ms ease-in-out;
        }

        .review {
            flex: 1 0 100%;
        }

        .review-avatar {
            max-width: var(--size-fluid-5);
            border-radius: 50%; 
        }

        .review-content {
            max-width: 80%;
        } 

        .reviews-btn {
            position: absolute;
            z-index: 10;
            top: 0;
            bottom: 0;
            background-color: hsl(var(--bgk));
            border: none;
            padding: var(--size-1);
            width: var(--size-fluid-4);
            cursor: pointer;
            transition: all 300ms var(--ease-squish-2);
        }

        .reviews-btn--prev {
            left: 0;
        }
        .reviews-btn--prev:is(:hover, :focus) {
            left: calc(var(--size-1) * -1);
            color: hsl(var(--text));
        }

        .reviews-btn--next {
            right: 0;
        }
        .reviews-btn--next:is(:hover, :focus) {
            right: calc(var(--size-1) * -1);
            color: hsl(var(--text));
        }
        
        .indicator-container {
            position: absolute;
            left: 50%;
            bottom: var(--size-5);
            display: flex;
            justify-content: center;
            gap: var(--size-3);
            transform: translateX(-50%);
        }

        .indicator {
            background: transparent;
            border: 0.15em solid hsl(var(--text-alt));
            border-radius: 50%;
            padding: 0.3rem;
            height: var(--size-fluid-1);
            cursor: pointer;
            aspect-ratio: 1/1;
        }

        .indicator.active {
            background: hsl(var(--text-alt));
        }

- Back to the **reviews.js** file to create the logic.
- Grab several elements we're going to need:

        const reviewsSlider = document.querySelector('.reviews');
        const reviewBtns = document.querySelectorAll('.review-btn');
        const reviews = [ ...document.querySelectorAll('.review')];
        const indicators = [...document.querySelectorAll('.indicator')];

- Create a variable called **isMoving** to prevent the user from clicking multiple times and messing up the timing of the transitions.

        let isMoving;

- Create a variable called **currentIndex** to keep track of the item we're currently in. Set the default to "1". Why 1? Because we want to start on the second item of the array. (remember we duplicated the first and last items.)

        let currentIndex = 1;

- Create event listeners

        reviewsBtns.forEach(btn => {
            btn.addEventListener('click', handleReviewBtnClick);
        });

- Create the function we're passing in to the listener:
- First, check if **isMoving**, if it is, return. If it's not moving, reset it back to true for the first time.

        const handleReviewBtnClick = (e) => {
            if (isMoving) return;
            isMoving = true;
        }

- Second, within the same statement, check if the current target is **next**. (The current target would be the arrow buttons)
- You're going to accomplish this check with a ternary statement.
- Depending on which button is click, the **currentIndex** should increase by one or decrease by one.

        e.currentTarget.id === 'next' ? 
            currentIndex++ : 
            currentIndex--; 

- Third, we're going to call on a function called **moveSlider()**. We haven't created this function, so let's do that now.
- This function takes the **reviewsSlider** and adds a style to it.
- You want to add "transform: translateX" and either move 100% or -100% based on the **currentIndex**. 

        const moveSlider = () => {
            reviewsSlider.style.tranform = `translateX(-${currentIndex * 100}%)`;
        }

- Now in the **moveSlider** function we're going to call on a function called **showActiveIndicator** and we need to set that one up as well.
- In this function we're going to loop through each indicator and remove any **"active"** class.
- Create a let variable called **activeIndicator** and check for a few possibilities.
    - If the current index equals 0, which means it's the first item's index in the array (duplicate) OR the last review's index (not duplicate) make the activeIndicator equal the last indicator (circle indicator)
    - Else if the curent index equals the last review's index OR the current index is equal the second item's index (which is the first not duplicated one) then the activeIndicator equals zero. 
    - Else make the activeIndicator equal the current index minus one.
- Now grab from the indicators the **activeIndicator**, and add the class **"active"**.

        const showActiveIndicator = () => {
            indicators.forEach(ind => ind.classList.remove('active'));
            let activeIndicator;
            if (currentIndex === 0 || currentIndex === reviews.length - 2) {
                activeIndicator = indicators.length - 1;
            } else if (currentIndex === reviews.length - 1 || currentIndex === 1) {
                activeIndicator = 0;
            } else {
                activeIndicator = currentIndex - 1;
            }
            indicators[activeIndicator].classList.add('active');
        }

- Add another event listeners for all the indicators.

        indicators.forEach(ind => {
            ind.addEvenetListener('click', handleIndicatorClick)
        })

- Make the **handleIndicatorClick** function.
- You can copy the **handleReviewsClick** because it's going to similar.

        const handleIndicatorClick = e => {
            if (isMoving) return;
            isMoving = true;
            currentIndex = indicators.indexOf(e.target) + 1;
            moveSlider();
        }

- One more event lister on the reviews slider. 
- It activates when the transition is over so we can make **isMoving** equal to false when the transition is over.

        reviewsSlider.addEventListerner('transitionend', () => {
            isMoving = false;
            if(currentIndex === 0) {
                currentIndex = reviews.length - 2;
                reviewsSlider.style.transitionDuration = '1ms';
                return moveSlider();
            }
            if (currentIndex === reviews.length - 1) {
                currentIndex = 1;
                reviewsSlider.style.transitionDureation = '1ms';
                return moveSlider();
            }
            reviewsSlider.style.transitionDuration = '300ms';
        })
