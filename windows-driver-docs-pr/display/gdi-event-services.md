---
title: GDI イベント サービス
description: GDI イベント サービス
ms.assetid: 966fa3ce-c72c-4b91-9cf7-b789d39e69b5
keywords:
- GDI WDK Windows 2000 の表示、イベント
- グラフィックス ドライバー WDK Windows 2000 の表示、イベント
- WDK の GDI やイベントの描画
- WDK GDI のイベント
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4ba788af90887e402d6692c612c6ec3d1f89427c
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349612"
---
# <a name="gdi-event-services"></a>GDI イベント サービス


## <span id="ddk_gdi_event_services_gg"></span><span id="DDK_GDI_EVENT_SERVICES_GG"></span>


GDI は、イベントに関連するいくつかのサービスを提供します。 これらのサービスを使用してドライバーは、作成、イベントを削除し、マップ、およびイベント、およびイベントを読み取り、設定およびクリアをマップ解除できます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">関数</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564190" data-raw-source="[&lt;strong&gt;EngClearEvent&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564190)"><strong>EngClearEvent</strong></a></p></td>
<td align="left"><p>指定したイベント オブジェクトを非シグナル状態に設定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564211" data-raw-source="[&lt;strong&gt;EngCreateEvent&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564211)"><strong>EngCreateEvent</strong></a></p></td>
<td align="left"><p>ディスプレイ ドライバーとビデオのミニポート ドライバーのハードウェア アクセスを同期するために使用される同期イベント オブジェクトを作成します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564801" data-raw-source="[&lt;strong&gt;EngDeleteEvent&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564801)"><strong>EngDeleteEvent</strong></a></p></td>
<td align="left"><p>指定されたイベント オブジェクトを削除します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564970" data-raw-source="[&lt;strong&gt;EngMapEvent&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564970)"><strong>EngMapEvent</strong></a></p></td>
<td align="left"><p>カーネル モード、ユーザー モード イベント オブジェクトにマップします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565001" data-raw-source="[&lt;strong&gt;EngReadStateEvent&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565001)"><strong>EngReadStateEvent</strong></a></p></td>
<td align="left"><p>指定されたイベント オブジェクトの現在の状態を返します。 シグナル状態か非シグナル状態。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565013" data-raw-source="[&lt;strong&gt;EngSetEvent&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565013)"><strong>EngSetEvent</strong></a></p></td>
<td align="left"><p>シグナルの状態を指定したイベント オブジェクトを設定し、イベント オブジェクトの以前の状態を返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565434" data-raw-source="[&lt;strong&gt;EngUnmapEvent&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565434)"><strong>EngUnmapEvent</strong></a></p></td>
<td align="left"><p>マップされたユーザー モード イベントに割り当てられたカーネル モードのリソースをクリーンアップします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565461" data-raw-source="[&lt;strong&gt;EngWaitForSingleObject&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565461)"><strong>EngWaitForSingleObject</strong></a></p></td>
<td align="left"><p>指定されたイベント オブジェクトがシグナルの状態に設定されるまで、または、待機がタイムアウトするまでは、ディスプレイ ドライバーの現在のスレッドを待機状態に保存されます。</p></td>
</tr>
</tbody>
</table>

 

 

 





