# Financeiro Memory

Read this file for tasks about Contas a Pagar, cobranca bancaria,
remessa/retorno, bancos, and financial operational screens.

## Area Map

- Contas a Pagar edit/detail screen: `SgaAlm\SgaAlmCp2.dfm/.pas` (`fCp2`,
  caption "Titulo a Pagar"). Search/list screens are around
  `SgaAlm\SgaAlmCp.dfm/.pas` and `SgaAlm\SgaAlmCp1.dfm/.pas`.
- Cobranca bancaria remessa/retorno: mainly `SgaExp\SgaExpCob.pas`. Bradesco
  CNAB 400 uses format 4/34 path (`TituloRemessaBradUY3`). Protest instruction
  field is `BANCOBINSTPROT`, edited in `Sga\SgaEdBan.pas/.dfm`.
