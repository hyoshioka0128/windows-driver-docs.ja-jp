---
title: セグメント化フィルターのインストール
description: セグメント化フィルターのインストール
ms.assetid: 39f96c16-2408-460c-8aa3-08b6a6584bef
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a8422cb60810455087efbcf2be9fce69539d3651
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551397"
---
# <a name="installing-a-segmentation-filter"></a>セグメント化フィルターのインストール





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

最初のエントリで、デバイスの[ **INF AddReg ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546320)レジスタ、セグメント化フィルター ドライバーの拡張機能として、次の 3 つのエントリは、COM コンポーネントとして、セグメント化フィルターを登録します。

ドライバーが Microsoft によって提供される、どちらも、デバイスの WIA セグメント化フィルターを使用している場合[ **INF CopyFiles ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546346)、 [ **INF SourceDisksFiles セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547472)も最後の 3 つのレジストリ エントリが必要になります。 唯一の要件は、ミニドライバーが、WIA を実装する\_IP\_セグメンテーション プロパティ。

COM **ThreadingModel**あります**両方**します。

INF ファイルの詳細については、[WIA デバイスの INF ファイル](inf-files-for-wia-devices.md)を参照してください。

 

 




