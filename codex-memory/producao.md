# Producao Memory

Read this file for tasks about production, production daily entries,
automation, equipment configuration, CEQ, production events, and
`ProdutosProduzidos`.

## Diaria de Producao Automatica

- Current automation entry point is `SgaPro\SgaProDia.pas`,
  `ProcessarProDiaAuto`.
- Equipment configuration product is `CFGEQUIPAMENTO.CEQPPRO`, referencing
  `PRODUCAOPRODUTO.PPROCOD`.
- Destination stock item is `ITEMCFGEQUIPAMENTO.ICEQESTQ`, referencing
  `ESTOQUE.ESTQCOD`.
- `ProcessarProDiaAuto.EncontraCeq` finds configuration by joining
  `CFGEQUIPAMENTO` to `ITEMCFGEQUIPAMENTO` (`ICEQCEQ = CEQCOD`) and filtering
  `ITEMCFGEQUIPAMENTO.ICEQESTQ`.
- `ProdutosProduzidos` can use optional `TAUTCONSULTA` fields `OPERADOR`,
  `OPERADORAUX`, and `ENCARREGADO`; missing/null/zero falls back to
  `ParamAutMoaFunCod`. Header function fields keep the value only when all
  generated periods agree, otherwise they fall back to `ParamAutMoaFunCod`.
- `ProdutosProduzidos` closes the previous stock/function group at the current
  row timestamp when `ESTOQUE` or function fields change. This preserves
  boundary groups such as 07-11, 11-12, and 12-15.
- No-production event parameter is `ParamAutMoaEvdSemProdCod` (PAR 3045).
- Automation execution time parameter is `ParamAutMoaHoraExecucao` (PAR 3046),
  edited on the production automation tab as a time field.
- No-production equipment configuration is per equipment in
  `EQUIPAMENTO.EQPAUTOMCEQSEMPROD`, edited on the equipment automation tab.
- When `ProdutosProduzidos` returns no rows, create a no-production daily item
  for the whole turno.
- When `cdsEstqProd` production ranges do not fully cover `iniTurno` to
  `fimTurno`, create no-production daily items for uncovered gaps before,
  between, or after production ranges.
- Positive-time gaps inside an existing produced daily item are filled with
  no-production events by `SgaProDia3.ConsultaEvd`.
- In `ProcessarProDiaAuto`, if horimeter-derived total plus event time exceeds
  the item period, clear `HorimValido`/`DPRHRSN` and fall back to period hours.
- Before creating a daily entry, `ProcessarProDiaAuto` checks existing
  `DIARIAPROD` rows overlapping the automation period for the same
  company/branch/equipment. Duplicate skips are logged with `SgaGravaLog` and
  include equipment, date, existing daily ref, and period.
