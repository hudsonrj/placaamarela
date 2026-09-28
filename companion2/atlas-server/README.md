# Atlas-server (opcional, nao faz parte do produto)

O produto da Placa Amarela e o firmware na placa. Este servidor nao e necessario
para usar o dispositivo. Foi um experimento de app e permanece aqui so como
referencia.

O motor principal é **local e determinístico**: uma pergunta por vez, descoberta
pequena, próxima ação mínima. Sem internet, sem chave, sem nuvem. A DeepSeek
continua opcional e só entra com consentimento.

## Subir

```powershell
cd companion2/atlas-server
node server.mjs
```

Abra `http://localhost:8787`. No telefone da mesma rede, use o IP desta máquina
e instale como aplicativo (PWA).

IA opcional:

```powershell
$env:DEEPSEEK_API_KEY = "chave-rotacionada"
node server.mjs
```

## O que o app faz

- Check-in do dia: crise / neutro / alta, humor, energia, sono
- Seis caminhos da placa: Como estou, Entender, Regular, Organizar, Decisão, Companhia
- Ferramentas reais: respirar, aterrar 5-4-3-2-1, adiar impulso, um passo, reunião, silêncio
- SOS permanente com SAMU 192 e CVV 188
- Mapa de descobertas e gatilhos
- Perfil adaptativo, local, apagável
- Funciona offline depois da primeira visita

## Endpoints

| Método | Caminho | Função |
| --- | --- | --- |
| `GET` | `/` | App |
| `GET` | `/health` | Status do motor |
| `GET` | `/api/state` | Estado `sistema_de_vida_v1` |
| `PUT` | `/api/state` | Grava estado |
| `POST` | `/api/journey` | Passo JSON para o app |
| `POST` | `/journey` | Protocolo `ATLAS/1` para a ESP32 |

Não publique a porta `8787` diretamente na internet. Em produção: HTTPS,
autenticação do dispositivo e limite de requisições.

O estado em `data/sistema.json` não deve ir para o git. Fica neste computador.

## Firmware

A Cheap Yellow Display continua independente. Se o Atlas estiver na mesma rede,
`POST /journey` devolve o protocolo antigo. Sem chave de IA, o dispositivo
recebe o motor local — o mesmo do telefone.
