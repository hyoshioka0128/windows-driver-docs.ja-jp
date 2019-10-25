---
title: ディスプレイ アダプターの子デバイス
description: ディスプレイ アダプターの子デバイス
ms.assetid: 9fd20e1a-db98-4571-8fc4-6d33fd0e2f16
keywords:
- ビデオの現在のネットワーク WDK ディスプレイ、アダプターの子デバイスの表示
- VidPN WDK ディスプレイ、ディスプレイアダプターの子デバイス
- 子デバイス WDK ビデオの現在のネットワーク
- ディスプレイアダプターの子デバイス WDK ビデオの現在のネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2956e6a8976206d0b128a4125b80b9657e618f3f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839055"
---
# <a name="child-devices-of-the-display-adapter"></a>ディスプレイ アダプターの子デバイス


ディスプレイアダプターの子デバイスはディスプレイアダプターのデバイスであり、ディスプレイミニポートドライバーによって子として列挙されます。 ディスプレイアダプターのすべての子デバイスがオンボードです。ディスプレイアダプターに接続するモニターとその他の外部デバイスは、子デバイスとは見なされません。

ディスプレイミニポートドライバーの[**DxgkDdiQueryChildRelations**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_child_relations)関数は、ディスプレイアダプターの子デバイスを列挙する役割を担います。 列挙中に、ディスプレイミニポートドライバーは、各子デバイスに種類とホットプラグ検出 (HPD) 認識値を割り当てます。 この型は、[**デバイス\_型列挙子の DXGK\_子\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/ne-dispmprt-_dxgk_child_device_type)の1つです。

-   **TypeVideoOutput**

-   **TypeOther**

HPD 認識値は、 [**DXGK\_子\_デバイス\_hpd\_認識**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgk_child_device_hpd_awareness)列挙子の1つです。

-   **HpdAwarenessAlwaysConnected**

-   **HpdAwarenessInterruptible**

-   **HpdAwarenessPolled**

次の表に、さまざまな種類および HPD 認識値を持つデバイスの例をいくつか示します。

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
<th align="left">Other</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Always Connected</strong></p></td>
<td align="left"><p>デスクトップコンピューター上の統合 LCD パネルの出力</p></td>
<td align="left"><p>TV チューナー</p>
<p>横棒スイッチ</p>
<p>MPEG2 コーデック</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>割り込み</strong></p></td>
<td align="left"><p>DVI</p>
<p>HDMI</p>
<p>ポータブルコンピューター上の統合 LCD パネルの出力</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>日時</strong></p></td>
<td align="left"><p>S-ビデオ</p>
<p>HD15</p></td>
<td align="left"></td>
</tr>
</tbody>
</table>

 

オペレーティングシステムは、HPD 認識値に応じて、いくつかの方法のいずれかを使用して、外部デバイスが子デバイスに接続されているかどうかを判断します。 次の表では、さまざまな HPD 認識値を持つデバイスの接続状態をオペレーティングシステムがどのように判断するかを簡単に説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">HpdAwareness</th>
<th align="left">オペレーティングシステムが接続状態を確認する方法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Always Connected</p></td>
<td align="left"><p>オペレーティングシステムは、子デバイスが常に存在することを認識しています。 子デバイスに接続されていないか、子デバイスとの接続が切断されている外部デバイスはありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>割り込み</p></td>
<td align="left"><p>オペレーティングシステムには、外部ディスプレイデバイスが子デバイスに接続されているか、子デバイスから切断されたときに通知されます。 (ポータブルコンピューターのディスプレイパネルは、カバーが開いていて、カバーが閉じられたときに切断されたときに、接続されていると見なされます)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>日時</p></td>
<td align="left"><p>オペレーティングシステムは、外部ディスプレイデバイスが子デバイスに接続されているかどうかを確認します。</p></td>
</tr>
</tbody>
</table>

 

 

 





