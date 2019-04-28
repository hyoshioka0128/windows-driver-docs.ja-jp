---
title: イベント\_型\_修飾子
description: イベント\_型\_修飾子
ms.assetid: 528e5eaa-aaeb-4e5b-a4b2-0f518fcd79ee
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: cc015ae40f9b2db851ebc16b0749d8b5d39c5a9e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360909"
---
# <a name="eventtypesqualifiers"></a>イベント\_型\_修飾子


## <span id="ddk_event_type_qualifiers_kr"></span><span id="DDK_EVENT_TYPE_QUALIFIERS_KR"></span>


イベント\_型\_修飾子の WMI クラスの修飾子が T11 委員会をサポートする HBA のミニポート ドライバーによって報告されるイベントの種類の一覧を含む*ファイバー チャネル HBA API*仕様。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">値</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>HBA_EVENT_ADAPTER_UNKNOWN</p></td>
<td align="left"><p>アダプターのイベントが既知であることを示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_EVENT_ADAPTER_ADD</p></td>
<td align="left"><p>HBA がローカル システムに追加されたことを示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_EVENT_ADAPTER_REMOVE</p></td>
<td align="left"><p>HBA がローカル システムから削除されたことを示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_EVENT_ADAPTER_CHANGE</p></td>
<td align="left"><p>されていると、ローカル システム上の HBA に構成の変更を示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_EVENT_PORT_UNKNOWN</p></td>
<td align="left"><p>ポートのイベントが既知であることを示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_EVENT_PORT_OFFLINE</p></td>
<td align="left"><p>ローカル ポートをオフラインになっていることを示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_EVENT_PORT_ONLINE</p></td>
<td align="left"><p>ローカル ポートがオンラインにすることを示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_EVENT_PORT_NEW_TARGETS</p></td>
<td align="left"><p>ローカル ポートが検出された、リモート ポートにターゲット デバイスを追加していることを示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_EVENT_PORT_FABRIC</p></td>
<td align="left"><p>ローカル ポートが登録済みの状態変更通知 (RSCN) コマンドを受信したことを示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_EVENT_PORT_STAT_THRESHOLD</p></td>
<td align="left"><p>統計カウンターが登録されているレベルに達したことを示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_EVENT_PORT_STAT_GROWTH</p></td>
<td align="left"><p>等しいか、登録済みレートを超える場合の料金で、統計カウンターが増加したことを示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_EVENT_TARGET_UNKNOWN</p></td>
<td align="left"><p>対象のイベントが既知であることを示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_EVENT_TARGET_OFFLINE</p></td>
<td align="left"><p>ターゲット ポートの使用が operational が不可能になったことを示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_EVENT_TARGET_ONLINE</p></td>
<td align="left"><p>ターゲット ポートの使用が operational が復元されたことを示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_EVENT_TARGET_REMOVED</p></td>
<td align="left"><p>ターゲット ポートがファブリックから削除されたことを示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_EVENT_LINK_UNKNOWN</p></td>
<td align="left"><p>リンクのイベントが既知であることを示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_EVENT_LINK_INCIDENT</p></td>
<td align="left"><p>ローカルの HBA が登録リンク インシデント コマンドを受信したことを示します。</p></td>
</tr>
</tbody>
</table>

 

含めることによって*Hbaapi.h*ソフトウェアは、一連の前の表に、型名に対応するシンボリック定数へのアクセスになります。 これらの記号定数の定義が記載されていない*Hbapiwmi.h* (WMI ツールのスイートを生成、コンパイル時にファイル)。

 

 





