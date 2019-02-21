---
title: ドライバーによって WIA 項目プロパティの読み取り
description: ドライバーによって WIA 項目プロパティの読み取り
ms.assetid: 4e592c62-e8bf-4b25-9c65-5a0079d3a857
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 05404be0525ece2288f5a2836952c712c79bcd7b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532688"
---
# <a name="reading-wia-item-properties-by-a-driver"></a>ドライバーによって WIA 項目プロパティの読み取り





WIA ミニドライバーする必要があります常に、プロパティ ドライバー項目ツリー内のベースとして使用の現在の設定。 読み取りとミニドライバーの項目のツリーへの書き込みアプリケーションは、ためことはありません最新でないことができます。 WIA ミニドライバーは、そのドライバーの項目のツリー内のプロパティからの読み取り、次の WIA サービス関数を使用する必要があります。

<a href="" id="wiasreadmultiple"></a>[**wiasReadMultiple**](https://msdn.microsoft.com/library/windows/hardware/ff549300)  
WIA プロパティのすべての型を読み取る。 これは、既存のカスタム プロパティを含む、WIA アイテムに対して任意のプロパティを読み取る WIA ドライバーをできるようにする一般的な関数です。 呼び出しごとの複数のプロパティを読み取るために使用します。

<a href="" id="wiasreadpropstr"></a>[**wiasReadPropStr**](https://msdn.microsoft.com/library/windows/hardware/ff549341)  
文字列の読み取り WIA プロパティ (VT 入力\_BSTR)。

<a href="" id="wiasreadproplong"></a>[**wiasReadPropLong**](https://msdn.microsoft.com/library/windows/hardware/ff549330)  
読み取り WIA プロパティは、4 バイトの整数 (VT 入力\_I4)。

<a href="" id="wiasreadpropfloat"></a>[**wiasReadPropFloat**](https://msdn.microsoft.com/library/windows/hardware/ff549320)  
4 バイトの実数である読み取り WIA プロパティ (VT 入力\_R4)。

<a href="" id="wiasreadpropguid"></a>[**wiasReadPropGuid**](https://msdn.microsoft.com/library/windows/hardware/ff549325)  
Guid である読み取り WIA プロパティ (VT 入力\_CLSID)。

<a href="" id="wiasreadpropbin"></a>[**wiasReadPropBin**](https://msdn.microsoft.com/library/windows/hardware/ff549308)  
符号なしバイトの文字列の読み取り WIA プロパティ (VT 入力\_ベクター |VT\_UI1)。

### <a name="reading-legal-values"></a>有効な値の読み取り

WIA 項目のプロパティには、コンテナーとアクセス権の種類を定義する属性が含まれています。 (詳細については、次を参照してください[WIA 項目に WIA プロパティを追加する](adding-wia-properties-to-a-wia-item.md)。)。コンテナーの種類は WIA\_PROP\_なし、WIA\_PROP\_リスト、および WIA\_PROP\_範囲。 アクセス権は WIA\_PROP\_読み取りおよび WIA\_PROP\_RW します。 既存のプロパティの検証中に WIA ミニドライバーは、有効な値を読み取る必要があるかどうかを確認する内部の更新設定を確認する必要があります。 WIA ミニドライバーを使用する必要があります、 [ **wiasGetPropertyAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff549257)サービスをその WIA プロパティの現在の有効な値を読み取る関数。

 

 




