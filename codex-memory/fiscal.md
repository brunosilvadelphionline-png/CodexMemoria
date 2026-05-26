# Fiscal Memory

Read this file for tasks about NF-e, NFSe, CT-e, CFOP, natureza, SPED, XML, and
electronic documents.

## Area Map

- CT-e XML: `SgaExp\SgaExpCe.pas`, procedure `CeXmlEnvio`. Natureza flag 73
  (`Sga\SgaEdNop.pas/.dfm`, `CteSubstituto`) emits `infCteSub`.
- NFSe WebISS: `SgaExp\SgaExpNseWebIss.pas`,
  `SgaExp\SgaExpNseWebIss202.pas`, shared description in
  `SgaExp\SgaExpNf8.pas`, function `MontaDiscriminacaoNfse`.

## Durable Rules

- CFOP 5922/6922 without natureza flag 217 emits NF-e as nota de debito
  (`finNFe=6`, `tpNFDebito=06`) and requires liquidation before sending.
  Helper: `NfCfopDebitoPagtoAntecipado` in `SgaExp\SgaExpNf.pas`.
- NF-e saida XML import parameter `ParamNeSaidaCondPgtoCli` (PAR 3039) is on
  `Parametros do Sistema > Sped Fiscal > Doc.Eletronicos > NF-e` and copies
  payment/cobranca data from the effective client when the XML has no duplicate
  payment terms.
