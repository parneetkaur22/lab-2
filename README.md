# lab-2

<link rel="stylesheet" href="https://unpkg.com/tachyons@4.8.0/css/tachyons.min.css"/>
<a class="f6 link dim ba bw2 ph3 pv2 ma5 dib black" href="#0">Add 1 Hero</a>

<main class="mw6 center">
    
  </main>
<script>
    
    let heroes = [
  {'name' : 'Prof. Xavier', 'twitter' : '@profx', 'pic' : 'http://www.animatedimages.org/data/media/450/animated-marvel-avatar-image-0004.gif'},
  {'name' : 'Spiderman', 'twitter' : '@spidey', 'pic' : 'http://www.animatedimages.org/data/media/450/animated-marvel-avatar-image-0008.gif'},  
  {'name' : 'Wolverine', 'pic' : 'http://www.animatedimages.org/data/media/450/animated-marvel-avatar-image-0011.gif', 'twitter' : '@logan' }
];


let moreHeroes = [
   {'name' : 'Cyclops', 'twitter' : '@oneye', 'pic' : 'http://www.animatedimages.org/data/media/450/animated-marvel-avatar-image-0005.gif'},
   {'name' : 'Storm', 'twitter' : '@rainsitpours', 'pic' : 'http://www.animatedimages.org/data/media/450/animated-marvel-avatar-image-0007.gif'},
   {'name' : 'Phoenix', 'twitter' : '@jeangrey', 'pic' : 'http://www.animatedimages.org/data/media/450/animated-marvel-avatar-image-0016.gif'}
];
    
    let main = document.querySelector('main');
    function render(heroes) {
     main.innerHTML =`${heroes.map( (hero, index) => `

<article class="dt w-100 bb b--black-05 pb2 mt2" href="#0">
      <div class="dtc w2 w3-ns v-mid">
        <img src="${hero.pic}"/>
      </div>
      <div class="dtc v-mid pl3">
        <h1 class="f6 f5-ns fw6 lh-title black mv0">${hero.name}</h1>
        <h2 class="f6 fw4 mt0 mb0 black-60">@${hero.twitter}</h2>
      </div>
      <div class="dtc v-mid">
        <form class="w-100 tr">
          <button data-id=${index}class="f6 button-reset bg-white ba b--black-10 dim pointer pv1 black-60" type="submit">${hero.following ? 'Following' : '+Follow'}</button>
        </form>
      </div>
    </article>
`).join('')} 

      `;
        let btn_follow = Array.from(document.querySelectorAll('[data-id]')); 
        btn_follow.map( btn => btn.addEventListener('click', function(e){
        e.preventDefault();
            
            if(heroes[this.dataset.id].following=== true){
                delete heroes[this.dataset.id].following;
                console.info(`Unfollowed ${heroes[this.dataset.id].name}`);
            }else{
                    heroes[this.dataset.id].following = true;
                    console.info(`Following ${heroes[this.dataset.id].name}`);
        }
                                                   
            } ));
    
    }
    
   
    function* idMaker() {
  var index = 0;
  while (index < moreHeroes.length)
    yield moreHeroes[index++];
}

var gen = idMaker();
    let btn_add1Hero= document.querySelector('a');
    btn_add1Hero.addEventListener('click', function(event){
        event.preventDefault();
        let tempObj = gen.next();
        tempObj.done ? console.warm('no more heroes') : heroes.push(tempObj.value);
        render(heroes);
    })
    render(heroes);
    
</script>
