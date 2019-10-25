---
title: ドライバーによる WIA 項目のプロパティの読み取り
description: ドライバーによる WIA 項目のプロパティの読み取り
ms.assetid: 4e592c62-e8bf-4b25-9c65-5a0079d3a857
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7995023f08a606e0844959d99ea696a19a7934c3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840762"
---
# <a name="reading-wia-item-properties-by-a-driver"></a>ドライバーによる WIA 項目のプロパティの読み取り





WIA ミニドライバーは、常に、独自のドライバー項目ツリー内のプロパティを現在の設定の基礎として使用する必要があります。 アプリケーションはミニドライバーの項目ツリーから読み取りおよび書き込みを行っているため、最新の状態ではありません。 WIA ミニドライバーは、次の WIA サービス機能を使用して、そのドライバー項目ツリーのプロパティから読み取る必要があります。

<a href="" id="wiasreadmultiple"></a>[**wiasReadMultiple**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasreadmultiple)  
すべての WIA プロパティの種類を読み取ります。 これは、wia ドライバーがカスタムプロパティを含む、WIA 項目上に存在するすべてのプロパティを読み取ることを可能にする一般的な関数です。 これは、呼び出しごとに複数のプロパティを読み取るために使用できます。

<a href="" id="wiasreadpropstr"></a>[**wiasReadPropStr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasreadpropstr)  
文字列である WIA プロパティを読み取ります (「VT\_BSTR)」を参照してください。

<a href="" id="wiasreadproplong"></a>[**wiasReadPropLong p)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasreadproplong)  
4バイトの整数である WIA プロパティを読み取ります (「VT\_I4)」を参照してください。

<a href="" id="wiasreadpropfloat"></a>[**wiasReadPropFloat**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasreadpropfloat)  
4バイトの実数 (型 VT\_R4) である WIA プロパティを読み取ります。

<a href="" id="wiasreadpropguid"></a>[**wiasReadPropGuid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasreadpropguid)  
Guid である WIA プロパティを読み取ります (「VT\_CLSID」と入力します)。

<a href="" id="wiasreadpropbin"></a>[**wiasReadPropBin**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasreadpropbin)  
符号なしバイトの文字列である WIA プロパティを読み取ります (型 VT\_VECTOR |VT\_UI1)。

### <a name="reading-legal-values"></a>有効な値の読み取り

WIA 項目プロパティには、コンテナーとアクセス権の種類を定義する属性が含まれています。 (詳細については、「wia の[プロパティを Wia 項目に追加する](adding-wia-properties-to-a-wia-item.md)」を参照してください)。コンテナーの種類は、WIA\_PROP\_NONE、WIA\_PROP\_LIST、および WIA\_PROP\_RANGE です。 アクセス権は、WIA\_PROP\_READ および WIA\_PROP\_RW です。 既存のプロパティの検証中に、WIA ミニドライバーは、内部更新設定を確認して、有効な値を読み取る必要があるかどうかを判断する必要があります。 WIA ミニドライバーでは、 [**Wiasgetpropertyattributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetpropertyattributes)サービス関数を使用して、wia プロパティの現在の有効な値を読み取る必要があります。

 

 




