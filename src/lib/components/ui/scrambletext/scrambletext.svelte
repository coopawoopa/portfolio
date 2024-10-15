<script>
    import { onMount } from 'svelte';
    import { TimelineLite, Expo } from 'gsap';
  
    onMount(() => {
      var tl = new TimelineLite({
        onComplete: function () {
          // this.restart();
        },
      });
  
      tl.set('p', { autoAlpha: 0 });
  
      tl.to('#scramble', 1.5, {
        scrambleText: {
          text: 'Creative Cornucopia.',
          chars: 'lowerCase',
          revealDelay: 0.25,
          tweenLength: true,
        },
      });
      tl.to('#scramble', 2, { css: { color: 'orange' }, ease: Expo.easeOut }, '-=1.5');
      tl.to('.intro', 1, { autoAlpha: 1 }, 0);
      tl.to('.white', 1, { autoAlpha: 1 }, 1.5);
  
      // second line
      tl.to(
        '#scramble',
        1.5,
        {
          scrambleText: {
            text: 'Digital Surrealist.',
            chars: 'lowerCase',
            revealDelay: 0.25,
            tweenLength: true,
          },
        },
        '+=1.5'
      );
      tl.to('#scramble', 2, { css: { color: '#FF69B4' }, ease: Expo.easeOut }, '-=1.5');
  
      // third line
      tl.to(
        '#scramble',
        1,
        {
          scrambleText: {
            text: 'Fantastical Scribe.',
            chars: 'lowerCase',
            revealDelay: 0.5,
            tweenLength: true,
          },
        },
        '+=1.5'
      );
      tl.to('#scramble', 2, { css: { color: '#7FFFD4' }, ease: Expo.easeOut }, '-=1.5');
  
      // fourth line
      tl.to(
        '#scramble',
        1,
        {
          scrambleText: {
            text: 'Exponential all the way.',
            chars: 'lowerCase',
            revealDelay: 0.5,
            tweenLength: true,
          },
        },
        '+=1.5'
      );
      tl.to('#scramble', 2, { css: { color: '#00FF7F' }, ease: Expo.easeOut }, '-=1.5');
  
      // end
      tl.to('.intro', 0.5, { autoAlpha: 0 }, '+=1');
      tl.to('.white', 0.5, { autoAlpha: 0 }, '+=0.25');
  
      // play timeline
      tl.play();
  
      /*
      $('.intro').click(function() {
              tl.restart();
              console.log("clicked")
      });
      */
    });
  </script>
  
  <style>
  
    p {
      color: #40d194;
      font-family: arial;
      font-size: 3.5rem;
      letter-spacing: -0.125rem;
      line-height: 3.75rem;
      font-weight: bold;
    }
  
    .white {
      color: #fff;
      margin-top: -2.5rem;
    }
  
    span {
      transition: all 0.1s ease;
      font-size: 10px;
    }
  </style>

    <p class="white">Fedor Agafonov</p>
  <p class="intro">
    <span id="scramble">Profolio</span>
  </p>

  