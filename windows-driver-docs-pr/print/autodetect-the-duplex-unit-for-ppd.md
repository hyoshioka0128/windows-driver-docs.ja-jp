---
title: PPD の Duplex ユニットを自動検出する
description: PPD の Duplex ユニットを自動検出する
ms.assetid: bbecceb1-ba1d-4d2d-9a7b-e43f49345ca2
keywords:
- 自動検出の両面印刷ユニット WDK のプリンターの自動構成
- PPD ファイル WDK 自動構成、両面印刷ユニットを自動検出しています
- ボックスの自動構成サポート WDK のプリンターが両面印刷ユニットを自動検出しています
- 両面印刷ユニットを検出します。
- 両面印刷ユニット WDK プリンターの自動構成
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d808c550e226e0fc0eeb236aca9d0df79867936e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345947"
---
# <a name="autodetect-the-duplex-unit-for-ppd"></a>PPD の Duplex ユニットを自動検出する


次の 2 つの例は、PPD ファイルと GDL ファイル内の対応」の説明に従って、両面印刷ユニット機能間の 1 つの可能なマッピングを示します。 この最初の例は、PPD ファイルから抜粋です。

```PPD
*OpenUI *DuplexUnit: Boolean
*DefaultDuplexUnit: True
*DuplexUnit True/Installed: ""
*DuplexUnit False/Not Installed: ""
*?DuplexUnit: "
  save
    currentpagedevice /Duplex known
    {(True)}{(False)}ifelse = flush
  restore
"
*End
*CloseUI: *DuplexUnit
```

次の例では、GDL ファイルからの抜粋し、前の例では、両面印刷ユニット機能に対応する DuplexUnit 機能定義を示しています。

```GDL
*Feature: DuplexUnit
{
  *FeatureType: PRINTER_PROPERTY

  *% *BidiQuery and *BidiResponse constructs must have the same names
  *BidiQuery: DuplexUnit
  {
    *QueryString: "\Printer.Configuration.DuplexUnit:Installed"
  }
  *BidiResponse: DuplexUnit
  {
    *ResponseType: BIDI_BOOL
    *ResponseData: ENUM_OPTION (DuplexUnit)
  }

  *Option: False
  {
    *BidiValue: BOOL(FALSE)
  }
  *Option: True
  {
    *BidiValue: BOOL(TRUE)
  }
}
```

 

 




