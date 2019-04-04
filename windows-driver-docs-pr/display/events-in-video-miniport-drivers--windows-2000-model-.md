---
title: ビデオ ミニポート ドライバー内のイベント (Windows 2000 モデル)
description: ビデオ ミニポート ドライバー内のイベント (Windows 2000 モデル)
ms.assetid: f6b5ded8-ddb4-4242-9bd3-b12dc96d8f6b
keywords:
- ビデオのミニポート ドライバー WDK Windows 2000 では、イベント
- イベントの WDK ビデオのミニポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50f3c70d2f060e3c23cb8f625b8635798a63d209
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57348921"
---
# <a name="events-in-video-miniport-drivers-windows-2000-model"></a>ビデオ ミニポート ドライバー内のイベント (Windows 2000 モデル)


## <span id="ddk_events_in_video_miniport_drivers_windows_2000_model__gg"></span><span id="DDK_EVENTS_IN_VIDEO_MINIPORT_DRIVERS_WINDOWS_2000_MODEL__GG"></span>


ビデオ ポート ドライバーでは、イベントの種類のサポート[カーネルのディスパッチャー オブジェクト](https://msdn.microsoft.com/library/windows/hardware/ff553202)ディスパッチ以下を実行している 2 つのスレッドの同期に使用できる\_レベル。 ビデオのミニポート ドライバーは、イベントを使用して、ビデオ ハードウェアへのアクセスを同期できます。

-   ビデオのミニポート ドライバーと、ディスプレイ ドライバーによって

-   で表示またはビデオのミニポート ドライバーを OpenGL ドライバーまたは (コントロール パネルの 表示プログラム) など、プログラムの拡張機能など、別のコンポーネント。

次の表には、ビデオ ポート ドライバーを提供するイベントに関連する関数が一覧表示します。

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570284" data-raw-source="[&lt;strong&gt;VideoPortClearEvent&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570284)"><strong>VideoPortClearEvent</strong></a></p></td>
<td align="left"><p>特定のイベント オブジェクトを非シグナル状態に設定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570287" data-raw-source="[&lt;strong&gt;VideoPortCreateEvent&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570287)"><strong>VideoPortCreateEvent</strong></a></p></td>
<td align="left"><p>イベント オブジェクトを作成します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570292" data-raw-source="[&lt;strong&gt;VideoPortDeleteEvent&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570292)"><strong>VideoPortDeleteEvent</strong></a></p></td>
<td align="left"><p>指定されたイベント オブジェクトを削除します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570352" data-raw-source="[&lt;strong&gt;VideoPortReadStateEvent&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570352)"><strong>VideoPortReadStateEvent</strong></a></p></td>
<td align="left"><p>特定のイベント オブジェクトの現在の状態を返します。 シグナル状態か非シグナル状態。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570364" data-raw-source="[&lt;strong&gt;VideoPortSetEvent&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570364)"><strong>VideoPortSetEvent</strong></a></p></td>
<td align="left"><p>状態にある既にでしたし、イベント オブジェクトの以前の状態を返す場合は、イベント オブジェクトをシグナル状態に設定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570378" data-raw-source="[&lt;strong&gt;VideoPortWaitForSingleObject&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570378)"><strong>VideoPortWaitForSingleObject</strong></a></p></td>
<td align="left"><p>指定されたディスパッチ オブジェクトがシグナルの状態に設定されるまで待機状態に、現在のスレッドは、(必要に応じて)、または、待機がタイムアウトするまでです。</p></td>
</tr>
</tbody>
</table>

 

GDI では、ドライバーを表示するイベントのサポートも提供します。 参照してください[イベントを使用したディスプレイ ドライバーで](using-events-in-display-drivers.md)詳細についてはします。

イベントに関するより広範なパースペクティブは、[イベント オブジェクト](https://msdn.microsoft.com/library/windows/hardware/ff544323)で、*カーネル モード ドライバーの設計ガイド*を参照してください。

 

 





