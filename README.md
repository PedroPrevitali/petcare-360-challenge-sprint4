# PetCare 360 – Challenge Sprint 4 (2TDS)

Entrega da Sprint 4: plano de testes manuais (Parte A) e testes automatizados (Parte B).

## Links de entrega

- **Azure Boards (correção dos testes manuais):** https://dev.azure.com/RM564184/PetCare%20360
- **Vídeo da configuração e execução da automação:** https://drive.google.com/drive/folders/1VYR9ZJOHKHoq208pjn-EbeMGVv92cRS_

## Parte A – Testes manuais
Planejados no Azure Boards (casos TC-SYS, TC-FE e TC-CT), com entradas, saídas esperadas e passos, usando dados controlados.

## Parte B – Testes automatizados (Postman)
Ferramenta: Postman (a solução é app mobile + API .NET 10 + Oracle 19c).

Arquivos em [`postman/`](postman/):
- `PetCare360.postman_collection.json` – coleção com 13 requisições e 40 asserções
- `PetCare360.postman_environment.json` – ambiente "PetCare 360 - Local" (`baseUrl`)

| # | Caso automatizado | Verifica |
|---|-------------------|----------|
| 1 | Smoke `GET /health/ready` | 200 e "Healthy" (API + Oracle) |
| 2 | Tutor: `POST`, `GET`, `GET` inexistente | 201 + id; 200; 404 |
| 3 | Pet Thor: `POST /api/Pets` | 201, id, nome |
| 4 | Clínica e consulta (02/11/2026 14:30) | 201, situação "Agendada"; clínica inexistente rejeitada |
| 5 | `GET /api/Pets/{id}/historico` | 200 e consulta no histórico |

Todas as requisições validam também o tempo de resposta (< 2000 ms). A pasta "99 - Limpeza" remove os dados criados.

### Como executar
1. No Postman: **Import** dos dois arquivos de `postman/`.
2. Selecione o ambiente **PetCare 360 - Local** e ajuste `baseUrl` (padrão `http://localhost:5260`).
3. Suba a API e o Oracle e execute com **Run collection**.
4. Opcional: `npx newman run postman/PetCare360.postman_collection.json -e postman/PetCare360.postman_environment.json`
