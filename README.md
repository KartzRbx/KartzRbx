<div align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=6,11,20&height=200&section=header&text=Mateus%20Franco&fontSize=60&fontColor=fff&animation=twinkling&fontAlignY=35&desc=Full%20Stack%20%7C%20Roblox%20Systems%20Architect&descAlignY=55&descSize=18" />
</div>

<div align="center">

[![Portfolio](https://img.shields.io/badge/🌐_Portfolio-v0--kartzdev.vercel.app-00D9FF?style=for-the-badge)](https://v0-kartzdev.vercel.app/)
[![Roblox](https://img.shields.io/badge/Roblox-KartzDev-00A2FF?style=for-the-badge&logo=roblox&logoColor=white)](https://www.roblox.com/users/5285698320/profile)
[![YouTube](https://img.shields.io/badge/YouTube-@Kartz__Dev-FF0000?style=for-the-badge&logo=youtube&logoColor=white)](https://www.youtube.com/@Kartz_Dev)
[![Discord](https://img.shields.io/badge/Discord-kartz-7289DA?style=for-the-badge&logo=discord&logoColor=white)](https://discord.gg/2QHPTRkQ)
[![Email](https://img.shields.io/badge/Email-gtofranco1@gmail.com-D14836?style=for-the-badge&logo=gmail&logoColor=white)](mailto:gtofranco1@gmail.com)

</div>

---

## 👨‍💻 Sobre Mim

```luau
local Kartz = {
    nome        = "Mateus Franco",
    idade       = 17,
    localização = "Brasil 🇧🇷",
    experiência = "6 anos",

    origem      = { "Desenvolvimento Web", "Front-end", "Back-end" },
    foco_atual  = "Roblox · Systems Architecture · Full Stack",

    ferramentas = {
        linguagens  = { "Luau", "TypeScript (RobloxTS)", "JavaScript", "HTML/CSS" },
        networking  = { "ZAP", "Networker" },
        dados       = { "ProfileStore", "DataStore2", "Replion" },
        workflow    = { "Rojo", "Git", "VS Code" },
        utilitários = { "Janitor", "Promise", "Signal" },
    },

    arquitetura = "Service-Oriented Architecture (SOA)",
    contato     = "gtofranco1@gmail.com",
}

print(`Olá! Sou {Kartz.nome}, desenvolvedor há {Kartz.experiência}. 🚀`)
```

Sou um **Desenvolvedor Full Stack Brasileiro** com **6 anos de experiência**, que começou no desenvolvimento web (HTML, CSS, JavaScript) e migrou para o ecossistema Roblox, onde atuo como **Systems Architect** — desenhando e implementando sistemas de alta complexidade com foco em performance, escalabilidade e código limpo.

Tenho vivência real em produção: trabalhei como **Lead Programmer** em projetos publicados, incluindo o **Anime Celestial X**, e mantenho projetos próprios ativos na plataforma.

---

## 🛠️ Stack Tecnológica

<div align="center">

### Linguagens
![Luau](https://img.shields.io/badge/Luau-00A2FF?style=for-the-badge&logo=roblox&logoColor=white)
![TypeScript](https://img.shields.io/badge/RobloxTS-3178C6?style=for-the-badge&logo=typescript&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)
![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)

### Roblox Ecosystem
![Roblox Studio](https://img.shields.io/badge/Roblox_Studio-00A2FF?style=for-the-badge&logo=roblox&logoColor=white)
![ZAP](https://img.shields.io/badge/ZAP_Networking-FF6B35?style=for-the-badge)
![ProfileStore](https://img.shields.io/badge/ProfileStore-4EA94B?style=for-the-badge)
![Rojo](https://img.shields.io/badge/Rojo-E3343A?style=for-the-badge)

### Ferramentas & Workflow
![Git](https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white)
![VS Code](https://img.shields.io/badge/VS_Code-007ACC?style=for-the-badge&logo=visual-studio-code&logoColor=white)
![Node.js](https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=node.js&logoColor=white)

</div>

---

## ⚡ ZAP — Networking de Alta Performance

> Utilizo o **[ZAP](https://zap.redblox.dev/)** como solução de networking nos meus projetos — uma alternativa ao RemoteEvent tradicional que empacota dados em **buffers binários**, reduzindo drasticamente o overhead de rede e tornando a engenharia reversa do jogo muito mais difícil.

**Vantagens que uso no dia a dia:**
- 📦 **Buffer Packing** — mesmos dados com fração da banda utilizada
- ⚡ **Performance superior** ao encoding genérico do Roblox
- 🔒 **Segurança** — validação automática de todos os dados recebidos do cliente
- 🧑‍💻 **DX excelente** — IDL legível e API intuitiva

```luau
-- Exemplo de definição ZAP (.zap)
-- events.zap
event TakeDamage = {
    from: Server,
    type: Reliable,
    call: SingleSync,
    data: struct {
        target: u16,
        damage: f32,
        source: enum { Bomb, Enemy, Fall },
    },
}

event UpdateCurrency = {
    from: Server,
    type: Reliable,
    call: SingleSync,
    data: struct {
        coins:   u32,
        gems:    u16,
        rebirth: u8,
    },
}
```

---

## 🗄️ Gerenciamento de Dados com ProfileStore

Utilizo uma **arquitetura de dados em camadas** com ProfileStore + Replion para replicação reativa, garantindo persistência segura e sincronização eficiente entre servidor e cliente.

```luau
-- DataService — inicialização e template de dados
local TEMPLATE = {
    coins       = 0,
    gems        = 0,
    rebirth     = 0,
    bomb_stage  = 1,
    island      = 1,
    potions     = {},
    ownedBombs  = {},
    totalDamage = 0,
    joinDate    = 0,
}

function DataService:init()
    self.dataservice:init({
        template         = TEMPLATE,
        profileStoreIndex = "PlayerData_v3",
        useMock          = RunService:IsStudio(),
    })
end

-- Atualização atômica com callback — garante consistência
function DataService:addCoins(player: Player, amount: number)
    self.dataservice:update(player, {"coins"}, function(current)
        return current + amount
    end)
end
```

---

## 🏗️ Arquitetura Orientada a Serviços

Todos os meus projetos seguem uma **SOA (Service-Oriented Architecture)** estrita — cada sistema é encapsulado em um serviço com responsabilidade única, comunicando-se via `networker` e gerenciando seu ciclo de vida com `Janitor`.

```luau
-- BombUpgradeService (Server) — padrão de serviço
local BombUpgradeService = {}
BombUpgradeService.__index = BombUpgradeService

local UPGRADE_COSTS: { [number]: number } = {
    [1] = 0,      [2] = 500,    [3] = 2500,
    [4] = 10000,  [5] = 50000,  [6] = 200000,
    [7] = 750000, [8] = 3000000
}

function BombUpgradeService:init()
    self.networker = networker.server.new("BombUpgrade", self, {
        self.requestUpgrade,
        self.skipWithRobux,
    })
end

function BombUpgradeService:requestUpgrade(player: Player, targetStage: number)
    local data      = self.dataservice:get(player)
    local cost      = UPGRADE_COSTS[targetStage]
    local current   = data.bomb_stage

    -- Validações
    if targetStage ~= current + 1 then return false, "INVALID_STAGE" end
    if data.coins < cost           then return false, "INSUFFICIENT_FUNDS" end
    if not UPGRADE_COSTS[targetStage] then return false, "MAX_STAGE" end

    -- Atualização atômica
    self.dataservice:update(player, {"coins"}, function(c) return c - cost end)
    self.dataservice:update(player, {"bomb_stage"}, function() return targetStage end)

    self.networker:fire(player, "RefreshBombs", targetStage)
    return true
end
```

---

## 🎯 Sistema de Inimigos — Detecção por Magnitude

```luau
-- EnemyService (Server) — detecção de detonação via Heartbeat
local DETONATION_RADIUS = 8
local DAMAGE_PER_HIT    = 25

function EnemyService:initDetonationLoop()
    self._janitor:add(RunService.Heartbeat:Connect(function()
        for enemyId, data in self._enemies do
            if not data.model or not data.model.Parent then continue end

            local rootPart = data.model:FindFirstChild("HumanoidRootPart")
            if not rootPart then continue end

            for _, bomb in self._activeBombs do
                local dist = (bomb.Position - rootPart.Position).Magnitude
                if dist <= DETONATION_RADIUS then
                    self:_dealDamage(data, bomb)
                end
            end
        end
    end), "Disconnect")
end

function EnemyService:_dealDamage(enemyData, bomb)
    local humanoid = enemyData.model:FindFirstChildOfClass("Humanoid")
    if not humanoid or humanoid.Health <= 0 then return end

    -- Kill attribution para crédito correto ao jogador
    local shooter = bomb:GetAttribute("Shooter")
    if shooter then
        enemyData.model:SetAttribute("LastHit", shooter)
    end

    humanoid:TakeDamage(DAMAGE_PER_HIT)
end
```

---

## 🌟 Projetos em Destaque

### 🌌 Anime Celestial X
> **Lead Programmer** — Desenvolvimento de sistemas de combate, progressão e multiplayer

[![Jogar](https://img.shields.io/badge/🎮_Jogar_no_Roblox-Anime_Celestial_X-00A2FF?style=for-the-badge)](https://www.roblox.com/pt/games/110483372589393/Anime-Celestial-X)

Responsável pela arquitetura back-end, sistemas de habilidades, balanceamento de progressão e integração de MarketplaceService para produtos Robux.

---

### 🏄 Brainrot Rider
Experiência de corrida aquática com simulação de física avançada, sistema de ondas dinâmicas e suporte multiplayer completo.

**Sistemas desenvolvidos:** Física de água, ranking em tempo real, sistema de pistas procedurais.

---

### ⛵ Build a Boat (Brainrot Edition)
Construção livre de barcos com partes temáticas + viagem com física real de flutuação.

**Sistemas desenvolvidos:** Grid building system, simulação de flutuabilidade, validação anti-exploit de construção.

---

### 💣 Bomb Clicker (Projeto Atual)
Sistema completo de progressão com **8 estágios de bomba**, multiplicadores de dano, sistema de rebirths (40 níveis), economias de ilha e integração de compras via Robux.

**Sistemas desenvolvidos:** BombUpgradeService, RebirthService, EnemyService, ClickService, FireCalculater com fórmula `1.06^level × islandMultiplier × potionMultiplier`.

---

## 📈 Jornada

```mermaid
timeline
    title Trajetória de Desenvolvimento
    2019 : Primeiros passos em HTML & CSS
         : Construção de landing pages
    2020 : JavaScript & lógica de programação
         : Primeiro contato com Lua no Roblox
    2021 : Primeiro jogo Roblox publicado
         : Aprendendo UI Design & UX
    2022 : Sistemas avançados em Luau
         : Arquitetura orientada a serviços
    2023 : RobloxTS & TypeScript
         : Integração ZAP Networking
         : Lead Programmer — Anime Celestial X
    2024 : Galaxy Roleplay · Brainrot Rider
         : ProfileStore · Replion · Rojo workflow
    2025 : Expandindo para sistemas de larga escala
         : Full Stack · Open Source contributions
```

---

## 🏆 Métricas & Conquistas

<div align="center">

| 📊 Estatísticas de Produção | |
|:---|:---:|
| 🗓️ Anos de experiência | **6 anos** |
| 🎮 Projetos publicados no Roblox | **4+** |
| 🧩 Sistemas arquitetados do zero | **15+** |
| 👥 Jogadores únicos (portfólio total) | **+3.000** |
| ⭐ Avaliação média dos jogos | **4.8 / 5** |
| 🕒 Horas jogadas (acumulado) | **+10k** |

</div>

---

## 💡 Filosofia de Desenvolvimento

> *"Código limpo não é um luxo — é respeito pelo próximo programador, que pode ser você mesmo daqui a seis meses."*

| Princípio | Aplicação Prática |
|:---|:---|
| 🏗️ **Separation of Concerns** | Cada serviço tem uma única responsabilidade |
| 🔒 **Server Authority** | Toda validação crítica acontece no servidor |
| 🧹 **Memory Management** | `Janitor` para limpeza garantida de conexões |
| ⚡ **Performance First** | ZAP buffers, magnitude checks vs. Touched, batch replication |
| 📦 **Atomic Updates** | Callbacks em `dataservice:update` para consistência de dados |

---

## 📊 GitHub Stats

<div align="center">
  <img src="https://github-readme-stats.vercel.app/api?username=KartzRbx&show_icons=true&theme=tokyonight&hide_border=true&bg_color=0D1117&title_color=00D9FF&icon_color=00D9FF&text_color=FFFFFF&count_private=true" height="165" />
  <img src="https://github-readme-stats.vercel.app/api/top-langs/?username=KartzRbx&layout=compact&theme=tokyonight&hide_border=true&bg_color=0D1117&title_color=00D9FF&text_color=FFFFFF" height="165" />
</div>

<div align="center">
  <img src="https://github-readme-streak-stats.herokuapp.com/?user=KartzRbx&theme=tokyonight&hide_border=true&background=0D1117&stroke=00D9FF&ring=00D9FF&fire=FF6B6B&currStreakLabel=FFFFFF" />
</div>

---

## 📞 Contato

<div align="center">

| Canal | Link |
|:---:|:---:|
| 🌐 Portfólio | [v0-kartzdev.vercel.app](https://v0-kartzdev.vercel.app/) |
| 🎮 Roblox | [KartzDev](https://www.roblox.com/users/5285698320/profile) |
| 💬 Discord | [kartz](https://discord.gg/2QHPTRkQ) |
| 📺 YouTube | [@Kartz_Dev](https://www.youtube.com/@Kartz_Dev) |
| 📧 Email | [gtofranco1@gmail.com](mailto:gtofranco1@gmail.com) |

</div>

---

<div align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=6,11,20&height=100&section=footer" />
  <br/>
  <b>⭐ Feito com dedicação por Mateus Franco — Systems Architect & Full Stack Developer desde 2019 ⭐</b>
</div>
