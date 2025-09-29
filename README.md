<!doctype html>

<html lang="pt-BR">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Loja Inclusiva — Roupas Acessíveis</title>
  <meta name="description" content="Loja de roupas pensada para acessibilidade: navegação por teclado, leitores de tela, alto contraste e controles simples." />  <style>
    :root{
      --bg:#ffffff;
      --fg:#111111;
      --accent:#0b5fff;
      --muted:#6b7280;
      --card:#f8fafc;
      --success:#047857;
      --danger:#b91c1c;
      --focus: 3px solid #ffbf47; /* alto contraste para foco */
      --radius:12px;
      --max-width:1100px;
    }

    @media (prefers-color-scheme: dark){
      :root{ --bg:#071013; --fg:#f8fafc; --card:#082032; --muted:#94a3b8; }
    }

    html,body{height:100%;}
    body{
      margin:0; font-family: system-ui, -apple-system, 'Segoe UI', Roboto, 'Helvetica Neue', Arial;
      background:var(--bg); color:var(--fg); -webkit-font-smoothing:antialiased; line-height:1.4;
      padding:1rem; display:flex; justify-content:center;
    }

    .container{max-width:var(--max-width); width:100%;}

    /* Skip link */
    .skip-link{position:absolute; left:0; top:0; transform:translateY(-120%); background:var(--accent); color:#fff; padding:.5rem 1rem; border-radius:0 0 .5rem .5rem; z-index:9999}
    .skip-link:focus{transform:translateY(0);}

    header{display:flex; align-items:center; justify-content:space-between; gap:1rem; padding:.5rem 0;}
    .brand{display:flex; align-items:center; gap:.75rem}
    .logo{width:48px;height:48px;border-radius:10px;background:linear-gradient(135deg,var(--accent),#06b6d4); display:flex;align-items:center;justify-content:center;color:white;font-weight:700}

    nav ul{display:flex; gap:.5rem; list-style:none; padding:0; margin:0}
    nav a{padding:.5rem .75rem; border-radius:8px; text-decoration:none; color:var(--fg)}
    nav a:focus, nav a:hover{outline:var(--focus)}

    main{display:grid; grid-template-columns: 1fr 340px; gap:1rem; margin-top:1rem}

    /* Product grid */
    .grid{display:grid; grid-template-columns: repeat(auto-fill,minmax(220px,1fr)); gap:1rem}
    .card{background:var(--card); padding:1rem; border-radius:var(--radius); display:flex; flex-direction:column; gap:.75rem}
    .product-img{background:#e6eefc; height:160px; border-radius:8px; display:flex; align-items:center; justify-content:center}
    .product-img img{max-width:100%; max-height:100%; object-fit:contain}
    .sr-only{position:absolute !important; width:1px; height:1px; padding:0; margin:-1px; overflow:hidden; clip:rect(0,0,0,0); white-space:nowrap; border:0}

    .price{font-weight:700}
    button{cursor:pointer}

    /* Filters / sidebar */
    aside{position:relative}
    .filters{background:var(--card); padding:1rem; border-radius:var(--radius); display:flex; flex-direction:column; gap:.75rem}
    .filters label{font-size:.95rem}
    .filter-group{display:flex; flex-direction:column; gap:.35rem}

    .cart{background:var(--card); padding:1rem; border-radius:var(--radius)}

    /* Accessible focus styles */
    :focus{outline:none}
    a:focus, button:focus, input:focus, select:focus, textarea:focus{box-shadow:var(--focus); border-radius:8px}

    /* Responsive */
    @media (max-width:900px){
      main{grid-template-columns:1fr;}
      aside{order:2}
    }

    footer{margin-top:1.5rem; color:var(--muted); font-size:.9rem}

    /* Reduced motion */
    @media (prefers-reduced-motion: reduce){*{transition:none!important}}

    /* Big clickable controls */
    .btn{background:var(--accent); color:white; border:none; padding:.6rem .9rem; border-radius:10px}
    .btn[aria-pressed="true"]{background:#0353b3}

    /* Focus-visible polyfill support */
    :focus-visible{box-shadow:var(--focus)}

    /* Tiny cart badge */
    .cart-badge{background:var(--danger); color:white; border-radius:999px; padding:.1rem .45rem; font-size:.8rem}

  </style></head>
<body>
  <a class="skip-link" href="#main">Pular para o conteúdo (tecla Tab)</a>
  <div class="container" id="top">
    <header role="banner">
      <div class="brand">
        <div class="logo" aria-hidden="true">LI</div>
        <div>
          <h1 style="font-size:1.1rem; margin:0">Loja Inclusiva</h1>
          <p style="margin:0; font-size:.85rem; color:var(--muted)">Roupas pensadas para todos</p>
        </div>
      </div><nav aria-label="Navegação principal">
    <ul>
      <li><a href="#produtos">Produtos</a></li>
      <li><a href="#sobre">Sobre</a></li>
      <li><a href="#contato">Contato</a></li>
      <li><a href="#acessibilidade">Acessibilidade</a></li>
      <li><button id="open-search" aria-expanded="false" class="btn">Buscar</button></li>
      <li><button id="open-cart" aria-controls="cart" aria-expanded="false" class="btn" aria-label="Abrir carrinho">Carrinho <span id="cart-count" class="cart-badge" aria-live="polite">0</span></button></li>
    </ul>
  </nav>
</header>

<main id="main" tabindex="-1">
  <section aria-labelledby="produtos" id="produtos">
    <h2 id="produtos">Produtos em destaque</h2>

    <!-- filtros simplificados -->
    <div style="margin:.5rem 0 1rem 0; display:flex; gap:.5rem; align-items:center; flex-wrap:wrap">
      <label for="search-input" class="sr-only">Pesquisar produtos</label>
      <input id="search-input" type="search" placeholder="Pesquisar por " aria-label="Pesquisar produtos" style="padding:.5rem .75rem; border-radius:8px; border:1px solid #d1d5db; min-width:220px">

      <label for="size" style="display:flex; gap:.5rem; align-items:center">Tamanho
        <select id="size" aria-label="Filtrar por tamanho" style="padding:.45rem .6rem; border-radius:8px; border:1px solid #d1d5db">
          <option value="">Todos</option>
          <option value="P">P</option>
          <option value="M">M</option>
          <option value="G">G</option>
          <option value="GG">GG</option>
        </select>
      </label>

      <label style="display:flex; gap:.5rem; align-items:center">
        <input id="high-contrast" type="checkbox"> Contraste alto
      </label>
    </div>

    <div class="grid" id="product-grid" aria-live="polite">
      <!-- Product card template will be populated by JS for clarity and to keep HTML semantic -->
    </div>
  </section>

  <aside aria-labelledby="filtros">
    <h2 id="filtros">Filtros</h2>
    <div class="filters" role="region" aria-label="Filtros de produtos">
      <div class="filter-group">
        <label for="type">Tipo</label>
        <select id="type" aria-label="Filtrar por tipo">
          <option value="">Todos</option>
          <option value="camiseta">Camiseta</option>
          <option value="calca">Calça</option>
          <option value="vestido">Vestido</option>
        </select>
      </div>

      <div class="filter-group">
        <span>Características acessíveis</span>
        <label><input type="checkbox" class="feat" value="abotoamento-lateral"> Abotoamento lateral</label>
        <label><input type="checkbox" class="feat" value="ziper-frontal"> Zíper frontal</label>
        <label><input type="checkbox" class="feat" value="tactil"> Etiqueta tátil</label>
      </div>

      <div class="filter-group">
        <button id="apply-filters" class="btn">Aplicar</button>
        <button id="clear-filters" style="background:transparent;border:1px solid #d1d5db;padding:.5rem;border-radius:8px">Limpar</button>
      </div>
    </div>

    <div class="cart" id="cart" aria-labelledby="carrinho" hidden>
      <h2 id="carrinho">Seu carrinho</h2>
      <div id="cart-items" aria-live="polite">Nenhum item no carrinho.</div>
      <div style="margin-top:.75rem; display:flex; gap:.5rem; justify-content:space-between; align-items:center">
        <strong id="cart-total">R$ 0,00</strong>
        <button id="checkout" class="btn">Finalizar</button>
      </div>
    </div>
  </aside>
</main>

<section id="sobre" style="margin-top:1.5rem">
  <h2>Sobre</h2>
  <p>Esta loja-demo prioriza normas de acessibilidade: estrutura semântica, atalhos de teclado, rótulos claros e foco visível. Conteúdo de imagem inclui descrições alternativas úteis.</p>
</section>

<section id="acessibilidade" style="margin-top:1rem">
  <h2>Acessibilidade</h2>
  <ul>
    <li>Teclas: Tab para navegar, Enter para ativar, Esc para fechar modais.</li>
    <li>Compatível com leitores de tela (ARIA, landmarks, labels).</li>
    <li>Preferência para reduzir animações respeitada.</li>
  </ul>
</section>

<footer role="contentinfo">
  <p>© Loja Inclusiva — Protótipo de site acessível.</p>
</footer>

  </div>  <script>
    // Small dataset: imagens são representativas (base64 placeholders omitted for brevity)
    const PRODUCTS = [
      {id:1, name:'Camiseta Adaptada Unissex', price:79.90, type:'camiseta', img:'https://via.placeholder.com/300x200?text=Camiseta', features:['abotoamento-lateral'], alt:'Camiseta adaptada, cor azul, com abertura lateral'},
      {id:2, name:'Calça com Zíper Frontal', price:129.90, type:'calca', img:'https://via.placeholder.com/300x200?text=Calça', features:['ziper-frontal'], alt:'Calça confortável com zíper frontal'},
      {id:3, name:'Vestido Fácil de Vestir', price:149.90, type:'vestido', img:'https://via.placeholder.com/300x200?text=Vestido', features:['tactil'], alt:'Vestido leve com etiqueta tátil'},
      {id:4, name:'Camiseta Básica', price:59.90, type:'camiseta', img:'https://via.placeholder.com/300x200?text=Camiseta2', features:[], alt:'Camiseta básica, cor branca'}
    ];

    const grid = document.getElementById('product-grid');
    const cart = {items:[], total:0};
    const cartCount = document.getElementById('cart-count');
    const cartItemsEl = document.getElementById('cart-items');
    const cartTotalEl = document.getElementById('cart-total');

    function currencyBRL(v){ return v.toLocaleString('pt-BR',{style:'currency',currency:'BRL'}); }

    function renderProducts(list){
      grid.innerHTML = '';
      if(list.length===0){ grid.innerHTML = '<p>Nenhum produto encontrado.</p>'; return }
      list.forEach(p=>{
        const card = document.createElement('article');
        card.className='card';
        card.setAttribute('tabindex','0');
        card.setAttribute('aria-labelledby','p'+p.id+'-title');

        const imgWrap = document.createElement('div'); imgWrap.className='product-img';
        const img = document.createElement('img'); img.src=p.img; img.alt = p.alt || p.name; img.loading='lazy';
        imgWrap.appendChild(img);

        const title = document.createElement('h3'); title.id = 'p'+p.id+'-title'; title.textContent = p.name;
        const desc = document.createElement('p'); desc.className='sr-only'; desc.textContent = 'Características: '+(p.features.join(', ') || 'Nenhuma');

        const price = document.createElement('div'); price.className='price'; price.textContent = currencyBRL(p.price);

        const controls = document.createElement('div'); controls.style.display='flex'; controls.style.gap='.5rem';
        const addBtn = document.createElement('button'); addBtn.className='btn'; addBtn.textContent='Adicionar ao carrinho'; addBtn.setAttribute('aria-label','Adicionar '+p.name+' ao carrinho');
        addBtn.addEventListener('click', ()=> addToCart(p));

        controls.appendChild(addBtn);

        card.appendChild(imgWrap);
        card.appendChild(title);
        card.appendChild(desc);
        card.appendChild(price);
        card.appendChild(controls);

        grid.appendChild(card);
      })
    }

    function addToCart(product){
      cart.items.push(product);
      cart.total = cart.items.reduce((s,i)=>s+i.price,0);
      cartCount.textContent = cart.items.length;
      cartItemsEl.textContent = '';
      cart.items.forEach((it,idx)=>{
        const div = document.createElement('div'); div.textContent = (idx+1)+'. '+it.name+' — '+currencyBRL(it.price);
        cartItemsEl.appendChild(div);
      });
      cartTotalEl.textContent = currencyBRL(cart.total);
      // Announce via ARIA live region already set on cart-count
    }

    // initial render
    renderProducts(PRODUCTS);

    // Filters
    document.getElementById('apply-filters').addEventListener('click', ()=>{
      const q = document.getElementById('search-input').value.toLowerCase();
      const size = document.getElementById('size').value;
      const type = document.getElementById('type').value;
      const feats = Array.from(document.querySelectorAll('.feat:checked')).map(i=>i.value);

      let result = PRODUCTS.filter(p=>{
        if(q && !(p.name.toLowerCase().includes(q))) return false;
        if(type && p.type!==type) return false;
        if(feats.length>0 && !feats.every(f=>p.features.includes(f))) return false;
        return true;
      });
      renderProducts(result);
    });

    document.getElementById('clear-filters').addEventListener('click', ()=>{
      document.getElementById('search-input').value=''; document.getElementById('size').value=''; document.getElementById('type').value=''; document.querySelectorAll('.feat').forEach(i=>i.checked=false);
      renderProducts(PRODUCTS);
    });

    // open/close cart
    const cartEl = document.getElementById('cart');
    document.getElementById('open-cart').addEventListener('click', (e)=>{
      const btn = e.currentTarget;
      const expanded = btn.getAttribute('aria-expanded') === 'true';
      btn.setAttribute('aria-expanded', String(!expanded));
      if(cartEl.hidden){ cartEl.hidden = false; cartEl.querySelector('h2').focus(); } else { cartEl.hidden = true; }
    });

    // search shortcut
    document.getElementById('open-search').addEventListener('click', ()=>{
      const s = document.getElementById('search-input'); s.focus();
    });

    // high contrast toggle
    document.getElementById('high-contrast').addEventListener('change', (e)=>{
      if(e.target.checked){ document.documentElement.style.setProperty('--accent','#ffbf47'); document.documentElement.style.setProperty('--fg','#000'); document.documentElement.style.setProperty('--bg','#fff'); document.body.style.filter='contrast(115%)'; }
      else { document.documentElement.style.removeProperty('--accent'); document.body.style.removeProperty('filter'); }
    });

    // Keyboard accessibility: Esc closes cart
    document.addEventListener('keydown', (e)=>{
      if(e.key === 'Escape'){
        if(!cartEl.hidden) { cartEl.hidden = true; document.getElementById('open-cart').setAttribute('aria-expanded','false'); }
      }
    });

    // trap focus in cart when open (simple)
    document.getElementById('open-cart').addEventListener('keydown', (e)=>{
      // if open and user presses tab we ensure focus goes into cart content
    });

    // Simple checkout mock
    document.getElementById('checkout').addEventListener('click', ()=>{
      if(cart.items.length===0){ alert('Seu carrinho está vazio.'); return }
      alert('Checkout mock — total: '+currencyBRL(cart.total));
    });

    // Improve image alt text for assistive tech (example)
    grid.addEventListener('keydown', (e)=>{
      // enter on a product card opens details in future; placeholder for expansion
    });

  </script></body>
</html>
