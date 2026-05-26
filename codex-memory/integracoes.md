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
  `TRANSPORTADORPEDIDO.TRPALTODESEMP`; MDFe and e-Frete CIOT map from it.
