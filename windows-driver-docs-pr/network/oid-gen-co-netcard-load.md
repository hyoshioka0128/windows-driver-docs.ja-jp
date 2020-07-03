---
title: OID_GEN_CO_NETCARD_LOAD
description: このトピックでは、OID_GEN_CO_NETCARD_LOAD オブジェクト識別子 (OID) について説明します。
ms.assetid: 0fdf9948-6b1a-48c9-87a4-7ecdfd1a8e47
keywords:
- OID_GEN_CO_NETCARD_LOAD
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba74bfb48616a57d63ca758ea2aefe4fb2158740
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85918230"
---
# <a name="oid_gen_co_netcard_load"></a>OID_GEN_CO_NETCARD_LOAD

> [!NOTE]
> OID_GEN_CO_NETCARD_LOAD は OID_GEN_NETCARD_LOAD と同じです。

OID_GEN_CO_NETCARD_LOAD OID は、接続指向ミニポートドライバーの送信システムの相対的な負荷を返します。 ミニポートドライバーは、プロトコルから送信されるデータの量と実際に送信されるデータの量の差を計算することによって、この数を取得します。これは、 [NdisMCoSendComplete](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff553475(v=vs.85))を使用してプロトコルに返されるパケットによって示されます。 その結果、ミニポートドライバーの未処理の送信データの量がいつでも増加します。

この統計は非常に高い頻度で変更されるため、ミニポートドライバーのポートでフィルター処理する必要があります。 最も簡単なフィルター処理方法は、未処理の送信データのサンプルの実行平均を維持することです。 たとえば、 [Miniportcosendpackets](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff549426(v=vs.85))が呼び出されるたびに、ミニポートドライバーは、送信されたパケットサイズを、 *Outスタンド ingbytes*という名前のミニポートドライバー定義変数に追加できます。 ミニポートドライバーが[NdisMCoSendComplete](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff553475(v=vs.85))を呼び出すたびに、ミニポートドライバーは、返されたパケットサイズを*outingbytes*から減算します。 また、ミニポートドライバーでは、実行の平均を維持する必要があります。これは、OID_GEN_CO_NETCARD_LOAD クエリに応答してミニポートドライバーが返す値です。 この変数は、 *Runningaverage*と呼ばれる場合があります。次のように、各*Miniportcosendpackets*で更新する必要があります。

```c++
RunningAverage = [(RunningAverage * C) + (OutstandingBytes * (128 - C))] / 128;
```
この場合は、1 \< *C* \< 128 です。 *C*の値が大きいほど、より滑らかなフィルター処理が生成されます。

## <a name="requirements"></a>要件

**バージョン**: Windows Vista 以降の**ヘッダー**: Ntddndis (Ndis .h を含む)