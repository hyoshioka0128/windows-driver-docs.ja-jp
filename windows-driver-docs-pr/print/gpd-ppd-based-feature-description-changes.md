---
title: GPD/PPD ベース機能説明変更
description: GPD/PPD ベース機能説明変更
ms.assetid: 22333d78-f78f-4031-a9f3-50b43ec746b6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fd016a303f82016e5c9ba9453223c15585675717
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385180"
---
# <a name="gpdppd-based-feature-description-changes"></a>GPD/PPD ベース機能説明変更


Microsoft XPSDrv Unidrv/PScript5 ドライバーでは、ハード コーディングされた Unidrv/PScript5 機能は含まれません。 Core のドライバーの構成モジュールは、機能、オプション、または制約を処理する必要がある場合 GPD または PPD ファイルにすべての機能、オプション、および制約を指定する必要があります。 非 GPD または PPD 以外の機能、オプション、または制約のサポートを提供する構成プラグインを実装することもできます。

ルート GPD または PPD ファイル (これは、ドライバーのデータ ファイルとして INF ファイルで指定) は、core ドライバーの構成モジュールが解析されます。 このルート GPD または PPD ファイルには、GPD または PPD ファイルのモジュール形式デザインを有効にするその他の GPD または PPD ファイルを含めることができます。 ほか、

Msxpsinc.gpd と Msxpsinc.ppd ファイル、フィルター パイプラインの GPD と PPD ファイルを構築する方法を決定することができます。 私たち GPD または PPD のファイル フィルターの再利用性を最大化すると、フィルターをペアリングすることをお勧めします。

次のコード例では、フィルターを Unidrv ベース XPSDrv フィルター パイプラインでサポートする逆の順序の印刷機能を指定する GPD 例を示します。

```cpp
*Feature: ReverseOrderPrinting
 {
 *PrintSchemaKeywordMap: "JobPageOrder"

 *Option: FrontToBack
 {
 *PrintSchemaKeywordMap: "Standard"
 }

 *Option: BackToFront
 {
 *PrintSchemaKeywordMap: "Reverse"
 }
}
```

前の例では、2 つのカスタム オプションを使用して、"ReverseOrderPrinting"カスタム GPD 機能が定義されています。"FrontToBack"と"BackToFront"。 この例では、 **PrintSchemaKeywordMap**キーワード GPD カスタム機能またはオプション パブリック印刷スキーマのキーワードをマップします。

次のコード例では、XPSDrv の PScript5 ベースのフィルター パイプラインでフィルターをサポートするページの向き機能を指定する PPD 例を示します。

```cpp
*OpenUI *PageOrientation: PickOne
*DefaultPageOrientation: Portrait
*PageOrientation Portrait: ""
*PageOrientation Landscape: ""
*PageOrientation RotatedLandscape: ""
*CloseUI: *PageOrientation

*MSPrintSchemaKeywordMap: PageOrientation  *PageOrientation
*MSPrintSchemaKeywordMap: PageOrientation Portrait *PageOrientation Portrait
*MSPrintSchemaKeywordMap: PageOrientation Landscape *PageOrientation Landscape
*MSPrintSchemaKeywordMap: PageOrientation ReverseLandscape *PageOrientation RotatedLandscape
```

前の例では、次の 3 つの印刷スキーマ標準 PageOrientation オプションをサポートするために、フィルターの機能を指定する 3 つのカスタム オプションを使用してカスタム PPD 機能を定義します。

使用して、 **PrintSchemaKeywordMap**または**MSPrintSchemaKeywordMap**キーワード、これら GPD または PPD のカスタム機能またはオプションが適切に公開されて XML PrintCapabilities または PrintTickets を使用して、印刷スキーマのパブリックのキーワードをマップします。

Core ドライバーの DEVMODE 構造体では、これらのカスタム GPD または PPD 機能の設定はオプションの配列に格納されます。

**注**   For Windows 7、 **MxdcGetPDEVAdjustment**関数には、横置きに回転の新しいパラメーター。 詳細については、次を参照してください。 [ **MxdcXDCGetPDEVAdjustment**](https://msdn.microsoft.com/library/windows/hardware/ff557558)します。

 

## <a name="related-topics"></a>関連トピック
[**MxdcXDCGetPDEVAdjustment**](https://msdn.microsoft.com/library/windows/hardware/ff557558)  
[V4 プリンター ドライバーのローカライズ](v4-driver-localization.md)  



