# EXP 07 - IMAGE CAROUSEL

## AIM:

To create an image carousel using hooks.

## ALGORITHM:

1. Create a new React JS project using npx create-react-app react-carousel and cd into the project directory i.e. cd react-carousel.

2. Create two folder inside the src directory: assets, components.

3. Insert src/assets directory, import your images. Create necessary files inside the src/components directory.

4. The hooks useState() & useEffect() are used to change the state of sliderImage (i.e active or inactive) & to apply the effect

## CODE:
### SliderImage.js
java
import first from "../assets/first.jpg";
import second from "../assets/second.jpg";
import third from "../assets/third.jpg";

export default[
    {
        title: "FIRST SLIDE",
        description: "Welcome to the first slide of the carousel",
        urls: first,
    },
    {
        title: "SECOND SLIDE",
        description: "Welcome to the second slide of the carousel",
        urls: second,
    },
    {
        title: "THIRD SLIDE",
        description: "Welcome to the third slide of the carousel",
        urls: third,
    },
];


### Arrows.js
js
import React from "react";

function Arrows({prevSlide, nextSlide}){
    return(
        <div className="arrows">
            <span className="prev" onClick={prevSlide}>
                &#10094;
            </span>
            <span className="next" onClick={nextSlide}>
                &#10095;
            </span>
        </div>
    );
}

export default Arrows;


### Dots.js
java
import React from "react";

function Dots ({activeIndex, onClicks, sliderImage}){
    return(
        <div className="all-dots">
            {sliderImage.map((slide, index) => (
                <span
                  key = {index}
                  className={'${activeIndex === index ? "dot active-dot" : "dot"} '}
                  onClick={() => onClicks(index)} >
                </span>
            ))}
        </div>
    );
}

export default Dots;


### SliderContent.js
java
import React from "react";

function SliderContent ({ activeIndex, sliderImage}){
    return(
        <section>
            {sliderImage.map((slide, index) => (
                <div
                    key = {index}
                    className = {index === activeIndex ? "slides active" : "inactive"}>
                    <img className="slide-image" src={slide.urls} alt=""/>
                    <h2 className="slide-title">{slide.title}</h2>
                    <h3 className="slide-text">{slide.description}</h3>
                </div>
            ))}
        </section>
    );
}

export default SliderContent;


### Slider.js
java
import React, {useEffect, useState} from "react";
import SliderContent from "./SliderContent";
import Dots from "./Dots";
import Arrows from "./Arrows";
import SliderImage from "./SliderImage";
import "./slider.css";

const len = SliderImage.length - 1;

function Slider(props){
    const [activeIndex, setActiveIndex] = useState(0);

    useEffect(() => {
        const interval = setInterval (() => {
            setActiveIndex(activeIndex === len ? 0 : activeIndex+1);
        },10000);
        return () => clearInterval(interval);
    }, [activeIndex]);

    return(
        <div className="slider-container">
            <SliderContent activeIndex={activeIndex} sliderImage={SliderImage} />
            <Arrows
                prevSlide={() =>
                    setActiveIndex(activeIndex < 1 ? len : activeIndex - 1)
                } 
                nextSlide={() => 
                    setActiveIndex(activeIndex === len ? 0 : activeIndex + 1)
                }/>
            <Dots
                activeIndex={activeIndex}
                sliderImage={SliderImage}
                onClicks={(activeIndex) => setActiveIndex(activeIndex)}
            />
        </div>
    );
}

export default Slider;


### slider.css
java
* {
    box-sizing: border-box;
    margin: 0;
  }
  
  :root {
    --heights: 50vh;
    --widths: 100%;
  }
  
  .slider-container {
    height: var(--heights);
    width: var(--widths);
    position: relative;
    margin: auto;
    overflow: hidden;
  }
  
  .active {
    display: inline-block;
  }
  
  .inactive {
    display: none;
  }
  
  .slides {
    height: var(--heights);
    width: var(--widths);
    position: relative;
  }
  
  .slide-image {
    width: 100%;
    height: 100%;
    position: absolute;
    object-fit: cover;
  }
  
  .slide-title,
  .slide-text {
    width: 100%;
    height: 100%;
    color: white;
    font-size: 50px;
    position: absolute;
    text-align: center;
    top: 40%;
    z-index: 10;
  }
  
  .slide-text {
    top: 65%;
    font-size: 2rem;
  }
  
  .prev,
  .next {
    color: transparent;
    cursor: pointer;
    z-index: 100;
    position: absolute;
    top: 50%;
    width: auto;
    padding: 1rem;
    margin-top: -3rem;
    font-size: 40px;
    font-weight: bold;
    border-radius: 0px 5px 5px 0px;
  }
  
  .slider-container:hover .prev,.slider-container:hover .next {
    color: black
  }
  
  .slider-container:hover .prev:hover,
  .slider-container:hover .next:hover {
    color: white;
    background-color: rgba(0, 0, 0, 0.6);
    transition: all 0.5s ease-in;
  }
  
  .next {
    right: 0;
    border-radius: 5px 0px 0px 5px;
  }
  
  .all-dots {
    width: 100%;
    height: 100%;
    position: absolute;
    display: flex;
    top: 85%;
    justify-content: center;
    z-index: 200;
  }
  
  .dot {
    cursor: pointer;
    height: 1.5rem;
    width: 1.5rem;
    margin: 0px 3px;
    background-color: transparent;
    /* background-color: rgba(0, 0, 0, 0.3); */
    border-radius: 50%;
    display: inline-block;
  }
  
  .slider-container:hover .dot:hover {
    background-color: rgba(255, 255, 255, 0.5);
  }
  
  /* .active-dot {
    background-color: rgba(255, 255, 255, 0.5);
  } */
  
  .slider-container:hover .dot{
    background-color: rgba(0, 0, 0, 0.3);
  }
  .slider-container:hover .active-dot{
    background-color: rgba(255, 255, 255, 0.5);
  }
  
  .play-pause {
    color: black;
  }


### App.js
java
import Slider from "./components/Slider";

function App() {
  return <Slider />;
}

export default App;


## OUTPUT: 

### SLIDE 1:
![image](https://github.com/Aashima02/carousel/assets/93427086/3147f552-238f-44c8-ad1c-f9281ea755ea)


### SLIDE 2:
![image](https://github.com/Aashima02/carousel/assets/93427086/15049eef-8d65-4586-abe1-5f541bf456b4)


### SLIDE 3:
![image](https://github.com/Aashima02/carousel/assets/93427086/48b753e6-74ce-4b6c-b9f3-fd620d4ae9d8)

## RESULT:

So, an image carousel is created using hooks.
