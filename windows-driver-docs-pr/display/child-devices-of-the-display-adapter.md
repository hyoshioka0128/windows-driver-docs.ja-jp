---
title: ディスプレイ アダプターの子デバイス
description: ディスプレイ アダプターの子デバイス
ms.assetid: 9fd20e1a-db98-4571-8fc4-6d33fd0e2f16
keywords:
- ビデオの WDK 表示のネットワークを表示、アダプター子デバイスを表示します。
- VidPN WDK の表示、ディスプレイ アダプター子デバイス
- 子デバイス WDK ビデオ存在するネットワーク
- アダプター子デバイス WDK ビデオ存在するネットワークを表示します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9a629b06681594fd022295e66c59dd33a6f6684
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370718"
---
# <a name="child-devices-of-the-display-adapter"></a>ディスプレイ アダプターの子デバイス


ディスプレイ アダプターの子デバイスは、ディスプレイのミニポート ドライバーによって子として列挙されているディスプレイ アダプター上のデバイスです。 ディスプレイ アダプターのすべての子デバイスがオンボードします。モニターとその他の外部に接続するデバイス ディスプレイ アダプターは、子デバイスは考慮されません。

ディスプレイのミニポート ドライバーの[ **DxgkDdiQueryChildRelations** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_query_child_relations)関数は子デバイスのディスプレイ アダプターを列挙する責任を負います。 列挙中にディスプレイのミニポート ドライバーでは、型とホット プラグ検出 (HPD) 認識の値にそれぞれの子デバイスが割り当てられます。 種類は、のいずれか、 [ **DXGK\_子\_デバイス\_型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/ne-dispmprt-_dxgk_child_device_type)列挙子。

-   **TypeVideoOutput**

-   **TypeOther**

HPD 認識値が 1 の[ **DXGK\_子\_デバイス\_HPD\_認識**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ne-d3dkmdt-_dxgk_child_device_hpd_awareness)列挙子。

-   **HpdAwarenessAlwaysConnected**

-   **HpdAwarenessInterruptible**

-   **HpdAwarenessPolled**

次の表では、さまざまな種類と HPD 認識の値を持つデバイスの例をいくつかを示します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">HpdAwareness</th>
<th align="left">VideoOutput</th>
<th align="left">その他</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>AlwaysConnected</strong></p></td>
<td align="left"><p>デスクトップ コンピューターでの統合の LCD パネルの出力</p></td>
<td align="left"><p>TV チューナー</p>
<p>バーのスイッチ間します。</p>
<p>MPEG2 コーデック</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>割り込み可能</strong></p></td>
<td align="left"><p>DVI</p>
<p>HDMI</p>
<p>ポータブル コンピューターの統合の LCD パネルの出力</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ポーリング</strong></p></td>
<td align="left"><p>S-ビデオ</p>
<p>HD15</p></td>
<td align="left"></td>
</tr>
</tbody>
</table>

 

オペレーティング システムでは、外部デバイスが子デバイスに接続されているかどうかを判断するのに、HPD 認識値に応じて、いくつかの方法のいずれかを使用します。 次の表では、オペレーティング システムが HPD 認識のさまざまな値を持つデバイスの接続の状態を判断する方法を簡単に説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">HpdAwareness</th>
<th align="left">オペレーティング システムが接続の状態を判断する方法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>AlwaysConnected</p></td>
<td align="left"><p>オペレーティング システムでは、子デバイスは常に存在を認識します。 外部のデバイスではありませんが、これまでに接続されているか子デバイスから切断されています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>割り込み可能</p></td>
<td align="left"><p>オペレーティング システムは、外付けディスプレイ デバイスに接続されている、または子デバイスから切断されているときに通知されます。 (ポータブル コンピューターで、表示パネルと見なされます、カバーが開いているときに接続されており、カバーを閉じた時点で切断されます)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ポーリング</p></td>
<td align="left"><p>オペレーティング システムでは、外付けディスプレイ、デバイスが子デバイスに接続されているかどうかを確認します。</p></td>
</tr>
</tbody>
</table>

 

 

 





