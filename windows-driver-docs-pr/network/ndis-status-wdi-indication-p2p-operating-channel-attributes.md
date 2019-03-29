---
title: NDIS_STATUS_WDI_INDICATION_P2P_OPERATING_CHANNEL_ATTRIBUTES
description: ミニポート ドライバーでは、NDIS_STATUS_WDI_INDICATION_P2P_OPERATING_CHANNEL_ATTRIBUTES を使用して、移動を開始する推奨される運用チャネルを示す、優先リッスン チャネル待ちの状態を入力するように求められる場合との完全なセットには、任意の時点でチャネルがサポートされています. 表示がアダプターの初期化時に 1 回送信し、ローミングや接続またはアクセス ポイントからの切断などにより、イベントには、これらのパラメーター変更のいずれかのたびを送信します。
ms.assetid: F7D27328-99B3-4EB5-9F48-864338EF8D8A
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WDI_INDICATION_P2P_OPERATING_CHANNEL_ATTRIBUTES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: bc85dc2b7ad550306b13d1d656d5e08300b8fe03
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574367"
---
# <a name="ndisstatuswdiindicationp2poperatingchannelattributes"></a>NDIS\_状態\_WDI\_INDICATION\_P2P\_オペレーティング\_チャネル\_属性


ミニポート ドライバーを使用して、NDIS\_状態\_WDI\_INDICATION\_P2P\_オペレーティング\_チャネル\_優先動作を示す属性は、移動を開始するチャネル優先にリッスン リッスン状態、および任意の時点でサポートされているチャネルの完全なセットを入力するように求められる場合のチャネルをします。 表示がアダプターの初期化時に 1 回送信し、ローミングや接続またはアクセス ポイントからの切断などにより、イベントには、これらのパラメーター変更のいずれかのたびを送信します。

| オブジェクト |
|--------|
| ポート   |

 

運用チャネルとチャネルのリストの値はローカル設定であり、実際のチャネルのネゴシエーション GO ネゴシエーション/招待時に考慮されていません。 ドライバーは、招待/移動のネゴシエーションを実行すると、チャネルをネゴシエートするが予想されます。

リッスン状態がオンの場合、ドライバーによって報告されたリッスン チャネルが受け入れられることが期待されます。 ホストには、このを示す値を使用して以前に報告優先リッスン チャネルとは異なるリッスン チャネルが構成されている場合、この通知が発生したことが期待されます。

## <a name="payload-data"></a>ペイロード データ


| 型                                                                                       | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                              |
|--------------------------------------------------------------------------------------------|--------------------------------|----------|----------------------------------------------------------|
| [**WDI\_TLV\_P2P\_チャネル\_数**](https://msdn.microsoft.com/library/windows/hardware/dn897869)                  |                                |          | チャネル、Wi-Fi Direct の動作属性です。            |
| [**WDI\_TLV\_P2P\_チャネル\_一覧\_属性**](https://msdn.microsoft.com/library/windows/hardware/dn897868) |                                |          | ローカルのアダプターでサポートされているチャネルの完全なセット。 |
| [**WDI\_TLV\_P2P\_リッスン\_チャネル**](https://msdn.microsoft.com/library/windows/hardware/mt269138)                  |                                |          | チャネル、Wi-Fi Direct リッスン属性です。               |

 

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>サポートされている最小のクライアント</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>サポートされている最小のサーバー</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Dot11wdi.h</td>
</tr>
</tbody>
</table>

 

 




