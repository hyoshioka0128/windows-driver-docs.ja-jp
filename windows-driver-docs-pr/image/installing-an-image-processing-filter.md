---
title: 画像処理フィルターのインストール
description: 画像処理フィルターのインストール
ms.assetid: bce6405f-0377-4e50-b898-28c6cdb962be
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f33e27ca3c5341326922589674415fe017145b02
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360034"
---
# <a name="installing-an-image-processing-filter"></a>画像処理フィルターのインストール





イメージのフィルター処理は通常、WIA ドライバーと共にインストールされます。 ドライバーとドライバーのイメージ処理フィルターをインストールするには、ドライバーの INF ファイルを少数の追加を行う必要があります。 次の例では、イメージ処理フィルターを含めるように、既存のドライバーの INF ファイルを変更する方法の例を示します。

```INF
[MyDriver.AddReg]
...
HKCR,CLSID\<UiClassId>\shellex\ImageProcessingFilter\<FilterClassId>
...
HKCR,CLSID\<FilterClassId>,,,"My Image Processing Filter"
HKCR,CLSID\<FilterClassId>\InProcServer32,,,%11%\Myimgfilter.dll
HKCR,CLSID\<FilterClassId>\InProcServer32,ThreadingModel,,"Apartment"
...

[MyDriver.CopyFiles]
...
Myimgfilter.dll
...

[SourceDisksFiles.x86]
...
Myimgfilter.dll=1
...
```

*&lt;UiClassId&gt;* 値は、ドライバー、WIA から返されるクラス ID\_DIP\_UI\_CLSID プロパティ、および*&lt;FilterClassId&gt;* フィルターの実装を処理するイメージのクラス ID です。 この例で*Myimgfilter.dll*イメージ処理フィルターの実装が含まれています。

最初のエントリで、 **AddReg**セクションは、ドライバーの拡張機能として、イメージ処理フィルターを登録して、次の 3 つのエントリは、COM コンポーネントとして、イメージ処理フィルターを登録します。

推奨される前例 INF スニペットで示すように**ThreadingModel**フィルターの INF ファイルを処理するイメージの値が**アパートメント**します。

**注**  ドライバーのインストールが完了--付加価値のあるコンポーネントと、フィルターをインストールすることはできます。

 

 

 




