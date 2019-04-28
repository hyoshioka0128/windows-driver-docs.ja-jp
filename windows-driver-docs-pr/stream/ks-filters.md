---
title: KS のフィルター
description: KS のフィルター
ms.assetid: caf46279-17f3-4bb4-8b8a-a1673f9fa28f
keywords:
- WDK のカーネルがストリームをフィルター処理します。
- ストリーミング KS フィルター WDK カーネル
- ミキサー WDK カーネルのストリーミング
- カーネル、WDK のストリームをフィルター処理します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 014f22a144730dcfae711a5508f4b024cd5cb211
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370249"
---
# <a name="ks-filters"></a>KS のフィルター





フィルターは、データ ストリームに対して実行する処理タスクをカプセル化するノードのグループです。 [ピン](ks-pins.md)フィルターの入力と出力のコンジットとして機能します。

単純なフィルターには、1 つのデータ シンクの暗証番号 (pin) および 1 つのデータ ソースの暗証番号 (pin) が含まれます。 フィルターは、データ シンクの pin での着信データを受信するには、内部的には、処理してデータ ソースの暗証番号 (pin) を書き込みます。 次の図では、ピンが太い線セグメントとして表示されます。 フィルターが内部的には、データ シンクの暗証番号 (pin) を内部処理単位に接続する*ノード*、さらに、データ ソースのピンに接続されます。

![単純な ks フィルターを示す図](images/ks01.png)

別のデバイスは、結合またはピンの間のデータ フローを分割する場合があります。 たとえば、オーディオ ミキサーには、いくつかのデータ シンク ピンがサポートされています。 ミキサーは、1 つのストリームに結合し、そのストリームをデータ ソースの pin に書き込みます。 次の図は、データ フローを示しています。

![ミキサーを示す図](images/ks02.png)

グラフには、フィルターのピンの間の内部の関係について説明します。 複雑なフィルターには、フィルターを流れるデータを変換するいくつかのノードがカプセル化する可能性があります。

フィルターを使用してピンと内部のノード間の内部接続を指定する、 [KSPROPSETID\_トポロジ](https://msdn.microsoft.com/library/windows/hardware/ff566598)プロパティ セット。

[ **KSPROPERTY\_トポロジ\_接続**](https://msdn.microsoft.com/library/windows/hardware/ff565802)プロパティは、KS フィルターのノード間のすべての接続を照会します。 このプロパティの配列を返します[ **KSTOPOLOGY\_接続**](https://msdn.microsoft.com/library/windows/hardware/ff567148)します。 各 KSTOPOLOGY\_接続構造は、フィルター内の接続を 1 つのデータ パスを表します。 上、一連の KSTOPOLOGY ミキサーの図で\_接続構造に次のようになります。

```cpp
//    FromNode,       FromNodePin,     ToNode,        ToNodePin,
{
 {  KSFILTER_NODE,        0,            0,               0     },
 {       0,               1,       KSFILTER_NODE,        1     }
}
```

 

 




