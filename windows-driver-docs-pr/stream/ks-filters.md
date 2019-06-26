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
ms.openlocfilehash: 186b51cdbc0574b3fb4aefcac05b59d2eebe4507
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382521"
---
# <a name="ks-filters"></a>KS のフィルター





フィルターは、データ ストリームに対して実行する処理タスクをカプセル化するノードのグループです。 [ピン](ks-pins.md)フィルターの入力と出力のコンジットとして機能します。

単純なフィルターには、1 つのデータ シンクの暗証番号 (pin) および 1 つのデータ ソースの暗証番号 (pin) が含まれます。 フィルターは、データ シンクの pin での着信データを受信するには、内部的には、処理してデータ ソースの暗証番号 (pin) を書き込みます。 次の図では、ピンが太い線セグメントとして表示されます。 フィルターが内部的には、データ シンクの暗証番号 (pin) を内部処理単位に接続する*ノード*、さらに、データ ソースのピンに接続されます。

![単純な ks フィルターを示す図](images/ks01.png)

別のデバイスは、結合またはピンの間のデータ フローを分割する場合があります。 たとえば、オーディオ ミキサーには、いくつかのデータ シンク ピンがサポートされています。 ミキサーは、1 つのストリームに結合し、そのストリームをデータ ソースの pin に書き込みます。 次の図は、データ フローを示しています。

![ミキサーを示す図](images/ks02.png)

グラフには、フィルターのピンの間の内部の関係について説明します。 複雑なフィルターには、フィルターを流れるデータを変換するいくつかのノードがカプセル化する可能性があります。

フィルターを使用してピンと内部のノード間の内部接続を指定する、 [KSPROPSETID\_トポロジ](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-topology)プロパティ セット。

[ **KSPROPERTY\_トポロジ\_接続**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-topology-connections)プロパティは、KS フィルターのノード間のすべての接続を照会します。 このプロパティの配列を返します[ **KSTOPOLOGY\_接続**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kstopology_connection)します。 各 KSTOPOLOGY\_接続構造は、フィルター内の接続を 1 つのデータ パスを表します。 上、一連の KSTOPOLOGY ミキサーの図で\_接続構造に次のようになります。

```cpp
//    FromNode,       FromNodePin,     ToNode,        ToNodePin,
{
 {  KSFILTER_NODE,        0,            0,               0     },
 {       0,               1,       KSFILTER_NODE,        1     }
}
```

 

 




