---
title: OID_GEN_CO_NETCARD_LOAD
description: このトピックでは、OID_GEN_CO_NETCARD_LOAD オブジェクト識別子 (OID) について説明します。
ms.assetid: 0fdf9948-6b1a-48c9-87a4-7ecdfd1a8e47
keywords:
- OID_GEN_CO_NETCARD_LOAD
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: de75f2b56836a016e059d1ed6bbb77d7aa8d05d9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361160"
---
# <a name="oidgenconetcardload"></a>OID_GEN_CO_NETCARD_LOAD

> [!NOTE]
> OID_GEN_CO_NETCARD_LOAD では、OID_GEN_NETCARD_LOAD と同じです。

OID_GEN_CO_NETCARD_LOAD OID は、接続指向のミニポート ドライバーの送信システム上の相対的な負荷を返します。 ミニポート ドライバーを使用するプロトコルに返されるパケットで示されているプロトコルからの送信用に提供されるデータの量と、実際に送信されるデータの量の違いを計算することでこの数を派生する[NdisMCoSendComplete](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff553475(v=vs.85))します。 結果は、未処理の量は、いつでも、ミニポート ドライバーでデータを転送します。

この統計情報が非常に高い頻度で変更されたため、ミニポート ドライバー ポートによってフィルターする必要があります。 最も単純なフィルター処理メソッドは、実行中に維持するためには、未処理のサンプルの平均は、データを送信します。 たとえば、毎回[MiniportCoSendPackets](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff549426(v=vs.85))が呼び出され、ミニポート ドライバーはというミニポート ドライバーの定義済み変数に送信されたパケットのサイズを追加する可能性があります*OutstandingBytes*します。 ミニポート ドライバーの呼び出しごとに[NdisMCoSendComplete](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff553475(v=vs.85))、ミニポート ドライバーはから返されるパケット サイズを取得し、その*OutstandingBytes*します。 ミニポート ドライバーは、実行中に維持することはも平均で、ミニポート ドライバーが OID_GEN_CO_NETCARD_LOAD クエリへの応答で返す必要があります値です。 この変数は、呼び出すことができます*RunningAverage*、各で更新する必要があります*MiniportCoSendPackets*、次のようにします。

```c++
RunningAverage = [(RunningAverage * C) + (OutstandingBytes * (128 - C))] / 128;
```
この場合、1 \< *C* \< 128 です。 値を大きく*C*より滑らかなフィルタ リングを生成します。

## <a name="requirements"></a>必要条件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis.h (include Ndis.h) |