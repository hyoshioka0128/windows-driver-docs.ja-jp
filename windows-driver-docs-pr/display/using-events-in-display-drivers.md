---
title: ディスプレイ ドライバーでのイベントの使用
description: ディスプレイ ドライバーでのイベントの使用
ms.assetid: 0c02d64f-0aad-43b4-b105-09ab8901e0de
keywords:
- WDK の Windows 2000 のイベントを表示します。
- ドライバー WDK Windows 2000 では、イベントを表示します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c594be9785148f55719ee6e58e2acadff55cd487
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389061"
---
# <a name="using-events-in-display-drivers"></a>ディスプレイ ドライバーでのイベントの使用


## <span id="ddk_using_events_in_display_drivers_gg"></span><span id="DDK_USING_EVENTS_IN_DISPLAY_DRIVERS_GG"></span>


GDI は、イベントの種類のサポートを提供します[カーネルのディスパッチャー オブジェクト](https://msdn.microsoft.com/library/windows/hardware/ff553202)ディスパッチ以下を実行している 2 つのスレッドの同期に使用できる\_レベル。 ディスプレイ ドライバーは、イベントを使用して、ビデオ ハードウェアへのアクセスを同期できます。

-   ディスプレイ ドライバー、ビデオのミニポート ドライバー

-   で表示またはビデオのミニポート ドライバーを OpenGL ドライバーまたは (コントロール パネルの 表示プログラム) など、プログラムの拡張機能など、別のコンポーネント。

次の表には、GDI イベントに関連する関数が一覧表示します。

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
<td align="left"><p>特定のイベント オブジェクトを非シグナル状態に設定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564211" data-raw-source="[&lt;strong&gt;EngCreateEvent&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564211)"><strong>EngCreateEvent</strong></a></p></td>
<td align="left"><p>同期イベント オブジェクトを作成します。</p></td>
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
<td align="left"><p>特定のイベント オブジェクトの現在の状態を返します。 シグナル状態か非シグナル状態。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565013" data-raw-source="[&lt;strong&gt;EngSetEvent&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565013)"><strong>EngSetEvent</strong></a></p></td>
<td align="left"><p>状態にある既にでしたし、イベント オブジェクトの以前の状態を返す場合は、イベント オブジェクトをシグナル状態に設定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565434" data-raw-source="[&lt;strong&gt;EngUnmapEvent&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565434)"><strong>EngUnmapEvent</strong></a></p></td>
<td align="left"><p>マップされたユーザー モード イベントに割り当てられたカーネル モードのリソースをクリーンアップします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565461" data-raw-source="[&lt;strong&gt;EngWaitForSingleObject&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565461)"><strong>EngWaitForSingleObject</strong></a></p></td>
<td align="left"><p>指定されたディスパッチ オブジェクトがシグナルの状態に設定されるまで待機状態に、現在のスレッドは、(必要に応じて)、または、待機がタイムアウトするまでです。</p></td>
</tr>
</tbody>
</table>

 

ビデオ ポート ドライバーには、ビデオのミニポート ドライバーへのイベントのサポートも提供します。 参照してください[ビデオのミニポート ドライバー (Windows 2000 モデル) 内のイベント](events-in-video-miniport-drivers--windows-2000-model-.md)詳細についてはします。

イベントに関するより広範なパースペクティブは、次を参照してください。[イベント オブジェクト](https://msdn.microsoft.com/library/windows/hardware/ff544323)します。

 

 





