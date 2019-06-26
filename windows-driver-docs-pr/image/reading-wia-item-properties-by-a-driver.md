---
title: ドライバーによる WIA 項目のプロパティの読み取り
description: ドライバーによる WIA 項目のプロパティの読み取り
ms.assetid: 4e592c62-e8bf-4b25-9c65-5a0079d3a857
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 39de774903f6a80a7853e08e50b54d849053e7fb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376496"
---
# <a name="reading-wia-item-properties-by-a-driver"></a>ドライバーによる WIA 項目のプロパティの読み取り





WIA ミニドライバーする必要があります常に、プロパティ ドライバー項目ツリー内のベースとして使用の現在の設定。 読み取りとミニドライバーの項目のツリーへの書き込みアプリケーションは、ためことはありません最新でないことができます。 WIA ミニドライバーは、そのドライバーの項目のツリー内のプロパティからの読み取り、次の WIA サービス関数を使用する必要があります。

<a href="" id="wiasreadmultiple"></a>[**wiasReadMultiple**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasreadmultiple)  
WIA プロパティのすべての型を読み取る。 これは、既存のカスタム プロパティを含む、WIA アイテムに対して任意のプロパティを読み取る WIA ドライバーをできるようにする一般的な関数です。 呼び出しごとの複数のプロパティを読み取るために使用します。

<a href="" id="wiasreadpropstr"></a>[**wiasReadPropStr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasreadpropstr)  
文字列の読み取り WIA プロパティ (VT 入力\_BSTR)。

<a href="" id="wiasreadproplong"></a>[**wiasReadPropLong**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasreadproplong)  
読み取り WIA プロパティは、4 バイトの整数 (VT 入力\_I4)。

<a href="" id="wiasreadpropfloat"></a>[**wiasReadPropFloat**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasreadpropfloat)  
4 バイトの実数である読み取り WIA プロパティ (VT 入力\_R4)。

<a href="" id="wiasreadpropguid"></a>[**wiasReadPropGuid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasreadpropguid)  
Guid である読み取り WIA プロパティ (VT 入力\_CLSID)。

<a href="" id="wiasreadpropbin"></a>[**wiasReadPropBin**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasreadpropbin)  
符号なしバイトの文字列の読み取り WIA プロパティ (VT 入力\_ベクター |VT\_UI1)。

### <a name="reading-legal-values"></a>有効な値の読み取り

WIA 項目のプロパティには、コンテナーとアクセス権の種類を定義する属性が含まれています。 (詳細については、次を参照してください[WIA 項目に WIA プロパティを追加する](adding-wia-properties-to-a-wia-item.md)。)。コンテナーの種類は WIA\_PROP\_なし、WIA\_PROP\_リスト、および WIA\_PROP\_範囲。 アクセス権は WIA\_PROP\_読み取りおよび WIA\_PROP\_RW します。 既存のプロパティの検証中に WIA ミニドライバーは、有効な値を読み取る必要があるかどうかを確認する内部の更新設定を確認する必要があります。 WIA ミニドライバーを使用する必要があります、 [ **wiasGetPropertyAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasgetpropertyattributes)サービスをその WIA プロパティの現在の有効な値を読み取る関数。

 

 




