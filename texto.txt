<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Loss Barber | @lzdocorte00</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
    <style>
        :root { --gold: #c5a059; --bg: #0a0a0a; --card-bg: #161616; --text: #ffffff; --border: #333333; }
        * { margin: 0; padding: 0; box-sizing: border-box; font-family: 'Oswald', sans-serif; }
        body { background-color: var(--bg); color: var(--text); overflow-x: hidden; scroll-behavior: smooth; }
        #brightness-overlay { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: black; pointer-events: none; z-index: 9999; opacity: 0; }

        /* TELA DE LOGIN */
        #login-screen { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: var(--bg); z-index: 5000; display: flex; justify-content: center; align-items: center; padding: 20px; }
        .login-box { background: var(--card-bg); padding: 40px; border-radius: 20px; border: 2px solid var(--gold); text-align: center; width: 100%; max-width: 400px; }
        .login-links { margin-top: 20px; border-top: 1px solid var(--border); padding-top: 15px; display: flex; flex-direction: column; gap: 12px; }
        .login-links a { color: var(--gold); text-decoration: none; font-size: 0.9rem; font-weight: bold; }

        /* HEADER */
        header { height: 50vh; background: linear-gradient(rgba(0,0,0,0.8), rgba(0,0,0,0.8)), url('https://images.unsplash.com/photo-1512690118299-a61250133440?auto=format&fit=crop&w=1350&q=80'); background-size: cover; background-position: center; display: flex; justify-content: center; align-items: center; border-bottom: 4px solid var(--gold); }
        .logo-area h1 { font-size: 3.5rem; color: var(--gold); letter-spacing: 5px; text-transform: uppercase; }

        /* IMPACTO */
        .impact-section { padding: 80px 10%; text-align: center; }
        .impact-section h2 { color: var(--gold); font-size: 2.5rem; margin-bottom: 20px; text-transform: uppercase; }
        .impact-section p { font-size: 1.2rem; line-height: 1.8; opacity: 0.9; }

        /* AGENDA */
        .calendar-container { max-width: 500px; margin: 0 auto; background: var(--card-bg); padding: 35px; border-radius: 20px; border: 1px solid var(--gold); text-align: center; }
        .input-field { width: 100%; padding: 15px; background: #000; color: white; border: 1px solid var(--border); margin-bottom: 15px; border-radius: 8px; outline: none; }
        .btn-gold { background: var(--gold); color: #000; border: none; padding: 18px; font-size: 1.1rem; font-weight: bold; cursor: pointer; width: 100%; text-transform: uppercase; border-radius: 8px; }

        /* STATUS / CANCELAR */
        .status-box { margin-bottom: 20px; padding: 20px; background: rgba(197, 160, 89, 0.1); border: 1px solid var(--gold); border-radius: 10px; display: none; }
        .btn-cancel { background: #ff4444; color: white; border: none; padding: 12px; width: 100%; border-radius: 8px; cursor: pointer; margin-top: 10px; font-weight: bold; }

        /* MENU 3 SETAS */
        .menu-trigger { position: fixed; top: 20px; right: 20px; background: var(--gold); border: none; padding: 12px; border-radius: 5px; z-index: 4001; cursor: pointer; color: #000; }
        .settings-side { position: fixed; top: 0; right: -320px; width: 300px; height: 100%; background: var(--gold); z-index: 4000; transition: 0.4s; padding: 30px; color: white; }
        .settings-side.active { right: 0; }

        /* SAC / RECLAME AQUI */
        .reclame-section { padding: 60px 10%; background: #050505; text-align: center; border-top: 1px solid var(--border); }
        .reclame-btn { color: #ff4444; text-decoration: none; border: 2px solid #ff4444; padding: 15px 30px; display: inline-block; border-radius: 8px; font-weight: bold; margin-bottom: 20px; }

        .rating-area { margin-top: 25px; padding: 20px; border: 2px dashed var(--gold); display: none; }
        .stars i { font-size: 2rem; color: #333; cursor: pointer; }
        .stars i.active { color: var(--gold); }
        
        footer { padding: 40px; text-align: center; background: #000; border-top: 1px solid var(--border); }
        .social-link { color: var(--gold); font-size: 1.8rem; text-decoration: none; transition: 0.3s; }
    </style>
</head>
<body>

    <div id="brightness-overlay"></div>

    <div id="login-screen">
        <div class="login-box">
            <h1 style="color:var(--gold)">LOSS BARBER</h1>
            <p style="margin-bottom: 20px; opacity: 0.8;">Barbearia Delivery Premium</p>
            <input type="text" id="login-nome" class="input-field" placeholder="Seu Nome">
            <button class="btn-gold" onclick="fazerLogin()">ENTRAR NO SITE</button>
            <div class="login-links">
                <a href="https://instagram.com/lzdocorte00" target="_blank">
                    <i class="fab fa-instagram"></i> Siga @lzdocorte00
                </a>
                <a href="https://wa.me/5551982143042?text=Olá, preciso de ajuda com o site." target="_blank">
                    <i class="fas fa-headset"></i> SAC: Suporte ao Cliente
                </a>
            </div>
        </div>
    </div>

    <button class="menu-trigger" onclick="document.getElementById('settings-menu').classList.toggle('active')">
        <i class="fas fa-bars"></i>
    </button>

    <div class="settings-side" id="settings-menu">
        <button onclick="document.getElementById('settings-menu').classList.remove('active')" style="background:none; border:none; color:white; font-size:1.5rem; float:right;">&times;</button>
        <h3>MENU</h3><br>
        <label>Ajustar Brilho:</label>
        <input type="range" style="width:100%" min="0" max="0.8" step="0.1" value="0" oninput="document.getElementById('brightness-overlay').style.opacity = this.value">
        <br><br>
        <button onclick="fazerLogout()" style="background: none; border: 1px solid white; color: white; width: 100%; padding: 10px; cursor: pointer;">SAIR DA CONTA</button>
    </div>

    <header><div class="logo-area"><h1>LOSS BARBER</h1></div></header>

    <section class="impact-section">
        <h2>Você não precisa sair de casa</h2>
        <p>Receba o tratamento de uma barbearia de elite no seu sofá. Praticidade total para o homem moderno que valoriza seu tempo e estilo.</p>
    </section>

    <section style="padding: 40px 0;">
        <div class="calendar-container">
            <div id="status-agendado" class="status-box">
                <p><strong>HORÁRIO RESERVADO!</strong></p>
                <p id="detalhe-agendamento" style="margin: 10px 0;"></p>
                <button class="btn-cancel" onclick="cancelarAgendamento()">CANCELAR AGORA</button>
            </div>

            <div id="form-agendar">
                <h2 style="color:var(--gold); margin-bottom: 20px;">AGENDE SEU CORTE</h2>
                <input type="date" id="data-agenda" class="input-field" onchange="renderHorarios()">
                <select class="input-field" id="horarios"><option value="">Selecione a Data</option></select>
                <input type="text" id="user-address" class="input-field" placeholder="Seu Endereço">
                <button class="btn-gold" onclick="finalizarAgendamento()">RESERVAR VIA WHATSAPP</button>
            </div>

            <div id="rating-area" class="rating-area">
                <h3>O que achou do atendimento?</h3>
                <div class="stars" id="star-box">
                    <i class="fas fa-star" onclick="avaliar(1)"></i><i class="fas fa-star" onclick="avaliar(2)"></i><i class="fas fa-star" onclick="avaliar(3)"></i><i class="fas fa-star" onclick="avaliar(4)"></i><i class="fas fa-star" onclick="avaliar(5)"></i>
                </div>
            </div>
        </div>
    </section>

    <section class="reclame-section">
        <h2 style="color:#ff4444; margin-bottom: 10px;">RECLAME AQUI</h2>
        <p style="margin-bottom: 20px;">Problemas com o atendimento? Fale com a gerência.</p>
        <a href="https://wa.me/5551982143042?text=Quero registrar uma reclamação." class="reclame-btn">CHAMAR NO WHATSAPP</a>
    </section>

    <footer>
        <a href="https://instagram.com/lzdocorte00" target="_blank" class="social-link">
            <i class="fab fa-instagram"></i>
        </a>
        <p style="margin-top: 10px; font-size: 0.8rem; opacity: 0.6;">@lzdocorte00 | Loss Barber 2026</p>
    </footer>

    <script>
        const horariosBase = ["10:00", "11:00", "13:00", "14:00", "15:00", "16:00", "17:00", "18:00", "19:00"];
        
        window.onload = function() {
            const hoje = new Date().toISOString().split('T')[0];
            document.getElementById('data-agenda').setAttribute('min', hoje);
            if(localStorage.getItem('usuario_nome')) {
                document.getElementById('login-screen').style.display = 'none';
                checarStatus();
            }
        };

        function fazerLogin() {
            const nome = document.getElementById('login-nome').value;
            if(!nome) return alert("Digite seu nome.");
            localStorage.setItem('usuario_nome', nome);
            location.reload();
        }

        function renderHorarios() {
            const select = document.getElementById('horarios');
            const data = document.getElementById('data-agenda').value;
            select.innerHTML = '<option value="">Horário</option>';
            const ocupados = JSON.parse(localStorage.getItem('horarios_ocupados') || "[]");
            horariosBase.forEach(h => {
                const opt = document.createElement('option');
                opt.value = h;
                opt.text = ocupados.includes(`${data}-${h}`) ? h + " (OCUPADO)" : h;
                if(ocupados.includes(`${data}-${h}`)) opt.disabled = true;
                select.add(opt);
            });
        }

        function finalizarAgendamento() {
            const d = document.getElementById('data-agenda').value;
            const h = document.getElementById('horarios').value;
            const end = document.getElementById('user-address').value;
            if(!d || !h || !end) return alert("Preencha tudo!");

            const id = `${d}-${h}`;
            let ocup = JSON.parse(localStorage.getItem('horarios_ocupados') || "[]");
            ocup.push(id);
            localStorage.setItem('horarios_ocupados', JSON.stringify(ocup));
            localStorage.setItem('meu_agendamento', id);
            
            if(confirm("Deseja um lembrete 30 min antes?")) alert("Lembrete ativado!");

            window.open(`https://wa.me/5551982143042?text=Novo Agendamento (@lzdocorte00): ${d} às ${h} em ${end}`, '_blank');
            location.reload();
        }

        function checarStatus() {
            const meu = localStorage.getItem('meu_agendamento');
            if(!meu) return;
            const partes = meu.split('-');
            const agendData = `${partes[0]}-${partes[1]}-${partes[2]}`;
            const agendHora = partes[3];
            const agora = new Date();
            const hoje = agora.toISOString().split('T')[0];
            const horaH = agora.getHours().toString().padStart(2, '0') + ":" + agora.getMinutes().toString().padStart(2, '0');

            if (agendData > hoje || (agendData === hoje && agendHora > horaH)) {
                document.getElementById('status-agendado').style.display = 'block';
                document.getElementById('detalhe-agendamento').innerText = `Marcado para: ${agendData.split('-').reverse().join('/')} às ${agendHora}`;
                document.getElementById('form-agendar').style.display = 'none';
            } else {
                if(!localStorage.getItem('avaliado_' + meu)) document.getElementById('rating-area').style.display = 'block';
            }
        }

        function cancelarAgendamento() {
            if(confirm("Tem certeza que deseja cancelar?")) {
                const meu = localStorage.getItem('meu_agendamento');
                let ocup = JSON.parse(localStorage.getItem('horarios_ocupados') || "[]");
                localStorage.setItem('horarios_ocupados', JSON.stringify(ocup.filter(i => i !== meu)));
                localStorage.removeItem('meu_agendamento');
                location.reload();
            }
        }

        function avaliar(n) {
            alert("Avaliação recebida! Obrigado.");
            localStorage.setItem('avaliado_' + localStorage.getItem('meu_agendamento'), n);
            location.reload();
        }

        function fazerLogout() { localStorage.clear(); location.reload(); }
    </script>
</body>
</html>
