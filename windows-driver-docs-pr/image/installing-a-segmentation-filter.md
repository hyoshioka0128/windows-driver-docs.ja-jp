---
title: セグメンテーション フィルターのインストール
description: セグメンテーション フィルターのインストール
ms.assetid: 39f96c16-2408-460c-8aa3-08b6a6584bef
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5d4168a7a93729ed5d605aa09f026b236419f3e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378940"
---
# <a name="installing-a-segmentation-filter"></a>セグメンテーション フィルターのインストール





セグメント化、フィルターは、WIA ドライバーと共にインストールする必要があります。 これを行うには、ドライバーの INF ファイルに追加の数が少ないを行う必要があります。 INF の次の例では、セグメント化フィルターを含めるように、既存のドライバーの INF ファイルを変更する方法を示します。

```INF
[MyDriver.AddReg]
...
HKCR,CLSID\<UiClassId>\shellex\SegmentationFilter\<FilterClassId>
...
HKCR,CLSID\<FilterClassId>,,,"My Segmentation Filter"
HKCR,CLSID\<FilterClassId>\InProcServer32,,,%11%\Mysegfilter.dll
HKCR,CLSID\<FilterClassId>\InProcServer32,ThreadingModel,,"Both"
...
 
[MyDriver.CopyFiles]
...
Mysegfilter.dll
...
 
[SourceDisksFiles.x86]
...
Mysegfilter.dll=1
...
```

*&lt;UiClassId&gt;*  、WIA ドライバーから返される値は、\_DIP\_UI\_CLSID プロパティ。 *&lt;FilterClassId&gt;* セグメント化フィルターの実装のクラス ID です。 *Mysegfilter.dll* dll は、セグメント化フィルターの実装が含まれています。

最初のエントリで、デバイスの[ **INF AddReg ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)レジスタ、セグメント化フィルター ドライバーの拡張機能として、次の 3 つのエントリは、COM コンポーネントとして、セグメント化フィルターを登録します。

ドライバーが Microsoft によって提供される、どちらも、デバイスの WIA セグメント化フィルターを使用している場合[ **INF CopyFiles ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-copyfiles-directive)、 [ **INF SourceDisksFiles セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-sourcedisksfiles-section)も最後の 3 つのレジストリ エントリが必要になります。 唯一の要件は、ミニドライバーが、WIA を実装する\_IP\_セグメンテーション プロパティ。

COM **ThreadingModel**あります**両方**します。

INF ファイルの詳細については、次を参照してください。 [WIA デバイスの INF ファイル](inf-files-for-wia-devices.md)します。

 

 




