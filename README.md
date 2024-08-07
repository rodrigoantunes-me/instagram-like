# Instagram-Style Like Animation 🥇

[![dev.to](https://img.shields.io/badge/dev.to-0A0A0A?style=for-the-badge&logo=devdotto&logoColor=white)](https://dev.to/rodrigoantunes/instagram-style-like-animation-3bb3)

## Demo

[![CodePen](https://img.shields.io/badge/Codepen-000000?style=for-the-badge&logo=codepen&logoColor=white)](https://codepen.io/rodrigoant/pen/PorjPdK)

## Post 

This is a quick way I found to congratulate Brazil's top Olympic medalist, [Rebeca Andrade](https://www.instagram.com/rebecarandrade), and, of course, share something I learned during the making of this effect.

### HTML

The markup is pretty straightforward, so I don't think there is much to say, other than highlighting the semantic use of HTML elements for structure and clarity, and the use of `<strong>` tags so you don't have to handle it in the CSS.

### CSS

I noticed there is a little random direction of the rotation every time the effect runs, so I passed a dynamic value to the CSS, similar to how we do with props in React.

```css
.heart {
  animation-name: like;
  animation-duration: 1s;
  animation-fill-mode: forwards;
}

@keyframes like {
  0% {
    opacity: 0;
    transform: scale(0)
  }

  40% {
    opacity: .8;
    transform: scale(1.2) rotate(var(--random-rotation-deg))
                   /* dynamic value here 👆 */
  }

  60% {
    opacity: 1;
    transform: scale(1)
  }

  100% {
    opacity: 0;
    transform: scale(.9) translateY(-500px)
  }
}

```

### Javascript

Here's how I created the element, give it the `.heart` class (which contains the animation-name), and generated the `random-rotation-deg` value.

```js
const image = document.querySelector('.image');

// listen for the 'dblclick' event
image.addEventListener('dblclick', () => {
  const rotation = Math.floor(Math.random() * 80) - 40;
  // this function returns a value between -40 and 40

  const heart = document.createElement('div');
  heart.classList.add('heart');
  heart.textContent = '🩷';
  heart.style.setProperty('--random-rotation-deg', `${rotation}deg`);
  // then, I pass this value so it can be read inside the CSS

  image.appendChild(heart);
  heart.onanimationend = () => heart.remove();
});

```

This method dynamically creates a heart element on double-click, applies a random rotation to it, and animates it using CSS keyframes.

For asset management, I'm using [Cloudinary](https://cloudinary.com/) which offers 25 GB of storage in the free plan — more than enough for small projects.

Once again, Congratulations to Rebeca Andrade, Simone Biles and Jordan Chiles.