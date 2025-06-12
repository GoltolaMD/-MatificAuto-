# 📘 matificAuto — Automação de lições Matific

matificAuto é um bookmarklet em JavaScript que automatiza a conclusão de atividades no site Matific, com uma interface minimalista e estilizada em vermelho escuro (#8B0000). Ideal para testes educacionais, demonstrações ou otimizações em ambientes de aprendizagem automatizados.

# ⚙️ Funcionalidades
✅ Executa automaticamente as lições visíveis no Matific.

🕒 Ajuste de tempo de espera entre ações.

📊 Contador de lições completadas.

⛔ Botão para parar a execução a qualquer momento.

❌ Interface flutuante com botão de fechar.

🎨 Tema escuro com detalhes em vermelho escuro e bordas visíveis.

# 🖼️ Visual
A interface é posicionada no canto inferior esquerdo da tela, com fundo escuro (#1a1a1a), textos e botões em vermelho escuro, borda destacada e controles intuitivos para iniciar, pausar e configurar o comportamento da automação.

# Codigo
```javascript
javascript:(()=>{if(window._matificAuto){window._matificAuto.stop=true;document.getElementById("matific-ui")?.remove();delete window._matificAuto;return;}window._matificAuto={stop:false,count:0};const sleep=ms=>new Promise(r=>setTimeout(r,ms));const clicarCentro=()=>{const x=window.innerWidth/2,y=window.innerHeight/2,el=document.elementFromPoint(x,y);el?.scrollIntoView({behavior:"smooth",block:"center"});el?.click();};const esperarBotaoOK=async()=>{for(let i=0;i<20;i++){if(window._matificAuto.stop)return false;const okBtn=[...document.querySelectorAll("button")].find(b=>b.textContent.trim()==="OK");if(okBtn){okBtn.click();return true;}await sleep(500);}return false;};const completar=async()=>{window.scrollTo({top:49235,behavior:'smooth'});await sleep(1500);const delay=()=>{const val=parseFloat(document.getElementById("matific-delay")?.value)||1;return val*1000;};for(let i=0;i<100;i++){if(window._matificAuto.stop)break;clicarCentro();await sleep(delay());const btnCompletar=[...document.querySelectorAll("button")].find(b=>b.textContent.trim()==="Completar Lição");if(btnCompletar){btnCompletar.click();await sleep(1000);await esperarBotaoOK();window._matificAuto.count++;document.getElementById("matific-count").textContent=window._matificAuto.count;}window.scrollBy(0,-300);await sleep(500);}if(!window._matificAuto.stop)alert("✅ Todas as lições visíveis foram completadas!");};const ui=document.createElement("div");ui.id="matific-ui";ui.style.position="fixed";ui.style.bottom="20px";ui.style.left="20px";ui.style.zIndex="99999";ui.style.background="#1a1a1a";ui.style.color="#8B0000";ui.style.padding="12px";ui.style.borderRadius="12px";ui.style.boxShadow="0 0 12px rgba(139,0,0,0.5)";ui.style.fontFamily="sans-serif";ui.style.minWidth="210px";ui.style.border="2px solid #8B0000";ui.innerHTML=`<div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:8px"><span style="font-weight:bold;font-size:15px;color:#8B0000;">📘 matificAuto</span><button id="close-matific" style="border:none;background:none;font-size:15px;cursor:pointer;color:#8B0000;">❌</button></div><div style="margin-bottom:8px;font-size:14px;color:#8B0000;">⏱️ Esperar (s): <input id="matific-delay" type="number" min="0" value="1" style="width:50px;padding:2px;margin-left:4px;background:#333;color:#8B0000;border:1px solid #8B0000;border-radius:4px"/></div><div style="margin-bottom:10px;font-size:14px;color:#8B0000;">✅ Lições feitas: <span id="matific-count" style="font-weight:bold;color:#8B0000;">0</span></div><button id="start-matific" style="margin-right:6px;padding:6px 10px;font-size:14px;background:transparent;color:#8B0000;border:1px solid #8B0000;border-radius:6px;cursor:pointer;">▶️ Começar</button><button id="stop-matific" style="padding:6px 10px;font-size:14px;background:transparent;color:#8B0000;border:1px solid #8B0000;border-radius:6px;cursor:pointer;">⏹️ Parar</button>`;document.body.appendChild(ui);document.getElementById("start-matific").onclick=()=>{if(!window._matificAuto.running){window._matificAuto.stop=false;window._matificAuto.running=true;window._matificAuto.count=0;document.getElementById("matific-count").textContent="0";completar().finally(()=>window._matificAuto.running=false);}};document.getElementById("stop-matific").onclick=()=>{window._matificAuto.stop=true;};document.getElementById("close-matific").onclick=()=>{window._matificAuto.stop=true;document.getElementById("matific-ui")?.remove();delete window._matificAuto;};})();
```


# 🚀 Como usar
1. Copie o código JavaScript do bookmarklet aqui.

2. Cole na barra de favoritos do seu navegador como um novo favorito.

3. Acesse o site da Matific.

4. Clique no bookmarklet para abrir a interface.

5. Ajuste o tempo (em segundos) se desejar.

6. Clique em ▶️ Começar para iniciar ou ⏹️ Parar para interromper.

7. Clique em ❌ para fechar e remover a interface da tela.
