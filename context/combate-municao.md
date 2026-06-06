# Consumo de munição em ataque à distância

Status: active
Atualizado: 2026-06-06
Doc: ECOSSISTEMA § A.7 resourceCosts | rules/attack.ts

## Por quê
- Arco/flechas no inventário não eram debitadas ao atacar — estado mecânico inconsistente com 5e.

## O quê (bullets)
- `backend/src/rules/ammunition.ts`: mapa arma→munição (`longbow`→`arrow`, crossbows→`crossbow-bolt`, etc.), checagem de estoque, `buildAmmunitionCost`.
- `validateWeaponAttack`: rejeita sem munição; inclui `resourceCosts` no `rollRequest.metadata`.
- `loadSnapshot`: inventário PENAI passa `quantity` para o snapshot de regras.
- `resolvePenaiStructuredRoll`: hint "Gasta 1× flecha" ao aplicar custo.
- Regra: 1 munição por rolagem de ataque (hit or miss); cancelar roll pendente não consome.

## Armadilhas
- Snapshot legado sem `quantity` assume 1 por stack (`quantity ?? 1`).
- Mapeamento por `weaponIndex`; armas homebrew com `ammunition` caem no fallback `arrow` se não estiver no mapa.

## Comandos / paths
- Testes: `node --test --import tsx src/__tests__/ammunition.spec.ts src/__tests__/rules.integration.spec.ts`
- Código: `rules/ammunition.ts`, `rules/attack.ts`, `GameMaster/combat/rollResolution.ts`
