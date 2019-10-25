---
title: GPD/PPD ベース機能説明変更
description: GPD/PPD ベース機能説明変更
ms.assetid: 22333d78-f78f-4031-a9f3-50b43ec746b6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b9ccbab27fefb9eeca0a433e47a01e8b3b891fa
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844581"
---
# <a name="gpdppd-based-feature-description-changes"></a>GPD/PPD ベース機能説明変更


Microsoft XPSDrv Unidrv/PScript5 ドライバーには、ハードコーディングされた Unidrv/PScript5 機能は含まれていません。 コアドライバー構成モジュールが機能、オプション、または制約を処理する必要がある場合は、GPD または PPD ファイル内のすべての機能、オプション、および制約を指定する必要があります。 非 GPD または非 PPD の機能、オプション、または制約をサポートする構成プラグインを実装することもできます。

ルート GPD または PPD ファイル (INF ファイルでドライバーのデータファイルとして指定されています) が、コアドライバー構成モジュールで解析されます。 このルート GPD または PPD ファイルには、GPD または PPD ファイルのモジュール形式の設計を可能にする他の GPD または PPD ファイルを含めることができます。 また、

Msgpd と Msxp の GPD ファイルでは、フィルターパイプラインのファイルと PPD ファイルの作成方法を決定できます。 フィルターを GPD または PPD ファイルと組み合わせて、フィルターの再利用性を最大化することをお勧めします。

次のコード例は、GPD の例を示しています。この例では、フィルターが Unidrv ベースの XPSDrv フィルターパイプラインでサポートしている逆順印刷機能を指定しています。

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

前の例では、"ReverseOrderPrinting" カスタム GPD 機能が、"FrontToBack" と "BackToFront" の2つのカスタムオプションを使用して定義されています。 この例では、 **PrintSchemaKeywordMap**キーワードを使用して、GPD カスタム機能またはオプションをパブリック印刷スキーマキーワードにマップします。

次のコード例は、PScript5 ベースの XPSDrv フィルターパイプラインでフィルターがサポートするページの向き機能を指定するための PPD の例を示しています。

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

前の例では、3つのカスタムオプションを持つカスタムの PPD 機能を定義して、3つの Print Schema standard PageOrientation オプションをサポートするフィルターの機能を指定しています。

**PrintSchemaKeywordMap**または**MSPrintSchemaKeywordMap**キーワードを使用すると、これらの GPD または PPD のカスタム機能やオプションは、マップされたパブリック印刷スキーマキーワードを使用して、XML PrintCapabilities または printtickets で適切に公開されます。

コアドライバーの DEVMODE 構造体では、これらのカスタム GPD または PPD 機能の設定がオプション配列に格納されます。

**注**   Windows 7 では、 **Mxdcgetpdevadjustment**関数に、横方向の回転用の新しいパラメーターがあります。 詳細については、「 [**MxdcXDCGetPDEVAdjustment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mxdc/nf-mxdc-mxdcgetpdevadjustment)」を参照してください。

 

## <a name="related-topics"></a>関連トピック
[**MxdcXDCGetPDEVAdjustment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mxdc/nf-mxdc-mxdcgetpdevadjustment)  
[V4 プリンタードライバーのローカライズ](v4-driver-localization.md)  



