# Integracoes Memory

Read this file for tasks about SgaWS, eSocial, portal bridge, web services,
external API integrations, and shared service signatures.

## SgaWS / eSocial / Portal

- SgaWS method signature changes in `SgaWS\SgaWsCGIImpl` or
  `SgaWS\SgaWsCGIIntf` may require matching updates in
  `SgaESocial\SgaESocial\Class1.cs`.
- `TValores` from `SgaWS\SgaWsCGIIntf.pas` is also consumed by the portal
  bridge under
  `Portal\DelphiSgaWS\DelphiSgaWS\DelphiSgaWS\Service References\SgaWsCGI`;
  keep `Reference.cs` and `ISgaWsCGIservice.wsdl` in sync with added fields.

## Transport / External Mapping

- Transportador do pedido high-performance marker is
  `TRANSPORTADORPEDIDO.TRPALTODESEMP`; MDFe, e-Frete CIOT, and
  Pamcard Roadcard map from it through shared CIOT helpers.

## CIOT / Pamcard Roadcard

- Pamcard Roadcard CIOT v9.2 changes are implemented mainly in
  `Sga\SgaRoadcard.pas` and shared CIOT helpers in `SgaExp\SgaExpCiot.pas`.
- Current Pamcard contract generation treats all operations as carga lotacao;
  carga fracionada fields are intentionally not sent yet.
- Payment model uses `DefineIndicadorPagamentoCiot`: one parcel with total
  liquid equal to total means a vista, otherwise a prazo. E-Frete V2 and
  Pamcard should share this rule.
- For Pamcard `InsertFreightContract`, do not send
  `viagem.pedagio.cartao.numero`; v9.2 ignores/removes this field.
