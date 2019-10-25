---
title: KS のフィルター
description: KS のフィルター
ms.assetid: caf46279-17f3-4bb4-8b8a-a1673f9fa28f
keywords:
- WDK カーネルストリーミングをフィルター処理します
- KS は WDK カーネルストリーミングをフィルター処理します
- ミキサー WDK カーネルストリーミング
- カーネルストリーミング WDK、フィルター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 677ce74374cc7a0e91b84ade977d8b9fadd78533
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842516"
---
# <a name="ks-filters"></a>KS のフィルター





フィルターは、データストリームに対して実行される処理タスクをカプセル化するノードのグループです。 [ピン](ks-pins.md)は、フィルターの入力および出力のパイプとして機能します。

単純なフィルターには、1つのデータシンクピンと1つのデータソースピンを含めることができます。 フィルターは、受信したデータをデータシンクの pin で受信し、内部で処理して、データソースの pin に書き込みます。 次の図では、ピンが太い線のセグメントとして表示されています。 内部的には、フィルターはデータシンクの pin を内部処理ユニット (*ノード*) に接続します。このノードは、データソースの pin に接続されています。

![単純な ks フィルターを示す図](images/ks01.png)

別のデバイスがピン間でデータフローを結合または分割する場合があります。 たとえば、オーディオミキサーでは、複数のデータシンクピンがサポートされています。 ミキサーは、これらを1つのストリームに結合し、そのストリームをデータソースの pin に書き込みます。 次の図は、データフローを示しています。

![ミキサーを示す図](images/ks02.png)

グラフには、フィルターのピン間の内部関係が記述されています。 より複雑なフィルターでは、フィルターを通過するデータを変換する複数のノードをカプセル化できます。

フィルターは、 [Ksk Propsetid\_トポロジ](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-topology)プロパティセットを使用して、ピンと内部ノード間の内部接続を指定します。

[**Ksk プロパティ\_TOPOLOGY\_connections**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-topology-connections)プロパティは、KS フィルターのノード間のすべての接続を照会します。 このプロパティは、 [**Kstopology\_接続**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kstopology_connection)の配列を返します。 各 KSTOPOLOGY\_接続構造は、フィルター内の1つのデータパス接続を表します。 上のミキサー図では、一連の KSTOPOLOGY\_接続構造は次のようになります。

```cpp
//    FromNode,       FromNodePin,     ToNode,        ToNodePin,
{
 {  KSFILTER_NODE,        0,            0,               0     },
 {       0,               1,       KSFILTER_NODE,        1     }
}
```

 

 




