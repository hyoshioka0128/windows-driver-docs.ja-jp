---
title: MB ミニポート ドライバーのパフォーマンス要件
description: MB ミニポート ドライバーのパフォーマンス要件
ms.assetid: 16986208-7572-412d-8839-71f1a66b074f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7cc897488d143b7fe69bbfbe17dba3115dcd970
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581378"
---
# <a name="mb-miniport-driver-performance-requirements"></a>MB ミニポート ドライバーのパフォーマンス要件


次の表では、MB のさまざまな操作に応答する MB ミニポート ドライバーの要件について説明します。 最良の結果、ミニポート ドライバーは「最適な時間 (秒)」の列で識別された時間内で操作を完了する必要があります。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">MB の操作</th>
<th align="left">最適なケース時間 (秒)</th>
<th align="left">最悪のケースの時間 (秒)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>初期化するためにデバイスの時刻 (に到達する<a href="https://msdn.microsoft.com/library/windows/hardware/ff571227" data-raw-source="[&lt;strong&gt;WwanReadyStateInitialized&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff571227)"> <strong>WwanReadyStateInitialized</strong></a>) 後、コンピューターに挿入される ( <a href="https://msdn.microsoft.com/library/windows/hardware/ff569833" data-raw-source="[OID_WWAN_READY_INFO](https://msdn.microsoft.com/library/windows/hardware/ff569833)">OID_WWAN_READY_INFO</a>)</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>5</p></td>
</tr>
<tr class="even">
<td align="left"><p>手動のネットワークの登録 ( <a href="https://msdn.microsoft.com/library/windows/hardware/ff569834" data-raw-source="[OID_WWAN_REGISTER_STATE](https://msdn.microsoft.com/library/windows/hardware/ff569834)">OID_WWAN_REGISTER_STATE</a>)</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>50</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ネットワーク スキャン操作 ( <a href="https://msdn.microsoft.com/library/windows/hardware/ff569843" data-raw-source="[OID_WWAN_VISIBLE_PROVIDERS](https://msdn.microsoft.com/library/windows/hardware/ff569843)">OID_WWAN_VISIBLE_PROVIDERS</a>)</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>200</p></td>
</tr>
<tr class="even">
<td align="left"><p>パケット アタッチ操作 ( <a href="https://msdn.microsoft.com/library/windows/hardware/ff569827" data-raw-source="[OID_WWAN_PACKET_SERVICE](https://msdn.microsoft.com/library/windows/hardware/ff569827)">OID_WWAN_PACKET_SERVICE</a>)</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>5</p></td>
</tr>
<tr class="odd">
<td align="left"><p>パケットのデタッチ操作 (OID_WWAN_PACKET_SERVICE)</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>5</p></td>
</tr>
<tr class="even">
<td align="left"><p>PDP アクティブ化 ( <a href="https://msdn.microsoft.com/library/windows/hardware/ff569823" data-raw-source="[OID_WWAN_CONNECT](https://msdn.microsoft.com/library/windows/hardware/ff569823)">OID_WWAN_CONNECT</a>)</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>10</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PDP 非アクティブ化 (OID_WWAN_CONNECT)</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>10</p></td>
</tr>
<tr class="even">
<td align="left"><p>システムの IP アドレス、デフォルト ゲートウェイ、および DNS アドレスを更新します。</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>5</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567391" data-raw-source="[&lt;strong&gt;NDIS_STATUS_LINK_STATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567391)"><strong>NDIS_STATUS_LINK_STATE</strong> </a> PDP アクティブ化の後の通知</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>10</p></td>
</tr>
<tr class="even">
<td align="left"><p>次のピン留め操作の完了 ( <a href="https://msdn.microsoft.com/library/windows/hardware/ff569828" data-raw-source="[OID_WWAN_PIN](https://msdn.microsoft.com/library/windows/hardware/ff569828)">OID_WWAN_PIN</a>)。</p>
<p>以下に</p>
<p>Enable</p>
<p>無効</p>
<p>[Change]</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>4</p></td>
</tr>
<tr class="odd">
<td align="left"><p>クエリ OID_WWAN_PIN MB デバイスの現在の暗証番号 (pin) の状態を取得するには</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>4</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569829" data-raw-source="[OID_WWAN_PIN_LIST](https://msdn.microsoft.com/library/windows/hardware/ff569829)">OID_WWAN_PIN_LIST</a>応答の一覧を取得するには、暗証番号 (pin) の種類がサポートされています</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>4</p></td>
</tr>
<tr class="odd">
<td align="left"><p>準備ができる SMS サブシステムの時間 (、NDIS_STATUS_WWAN_SMS_CONFIGURATION を送信する必要があります要請されていないを示す値)</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>60</p></td>
</tr>
<tr class="even">
<td align="left"><p>ミニポート ドライバーがすべて他 WWAN Oid OID_WWAN_VENDOR_SPECIFIC を除くこの表で説明されていないを完了するための時間</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>15</p></td>
</tr>
</tbody>
</table>

 

 

 





