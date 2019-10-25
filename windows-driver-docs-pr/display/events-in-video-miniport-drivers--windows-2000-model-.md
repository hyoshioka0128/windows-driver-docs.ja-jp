---
title: ビデオミニポートドライバーのイベント (Windows 2000 モデル)
description: ビデオミニポートドライバーのイベント (Windows 2000 モデル)
ms.assetid: f6b5ded8-ddb4-4242-9bd3-b12dc96d8f6b
keywords:
- ビデオミニポートドライバー WDK Windows 2000、イベント
- イベント WDK ビデオミニポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 52c97f8035e4987a249c082ca02212a4de255ffd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839699"
---
# <a name="events-in-video-miniport-drivers-windows-2000-model"></a>ビデオミニポートドライバーのイベント (Windows 2000 モデル)


## <span id="ddk_events_in_video_miniport_drivers_windows_2000_model__gg"></span><span id="DDK_EVENTS_IN_VIDEO_MINIPORT_DRIVERS_WINDOWS_2000_MODEL__GG"></span>


ビデオポートドライバーでは、イベントのサポートが提供されます。この種類の[カーネルディスパッチャーオブジェクト](https://docs.microsoft.com/windows-hardware/drivers/kernel/kernel-dispatcher-objects)を使用すると、以下のディスパッチ\_レベルで実行される2つのスレッドを同期できます。 ビデオミニポートドライバーは、イベントを使用してビデオハードウェアへのアクセスを同期することができます。

-   ビデオミニポートドライバーとディスプレイドライバーによる

-   ディスプレイまたはビデオのミニポートドライバーと、OpenGL ドライバーやプログラムの拡張機能 (コントロールパネルの表示プログラムなど) などの別のコンポーネント。

次の表に、ビデオポートドライバーが提供するイベント関連の関数を示します。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportclearevent" data-raw-source="[&lt;strong&gt;VideoPortClearEvent&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportclearevent)"><strong>VideoPortClearEvent</strong></a></p></td>
<td align="left"><p>指定されたイベントオブジェクトを非シグナル状態に設定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportcreateevent" data-raw-source="[&lt;strong&gt;VideoPortCreateEvent&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportcreateevent)"><strong>VideoPortCreateEvent</strong></a></p></td>
<td align="left"><p>イベントオブジェクトを作成します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportdeleteevent" data-raw-source="[&lt;strong&gt;VideoPortDeleteEvent&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportdeleteevent)"><strong>VideoPortDeleteEvent</strong></a></p></td>
<td align="left"><p>指定したイベントオブジェクトを削除します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportreadstateevent" data-raw-source="[&lt;strong&gt;VideoPortReadStateEvent&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportreadstateevent)"><strong>VideoPortReadStateEvent</strong></a></p></td>
<td align="left"><p>指定されたイベントオブジェクトの現在の状態 (シグナル状態または非シグナル状態) を返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportsetevent" data-raw-source="[&lt;strong&gt;VideoPortSetEvent&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportsetevent)"><strong>VideoPortSetEvent</strong></a></p></td>
<td align="left"><p>イベントオブジェクトをシグナル状態に設定し、まだその状態にない場合は、イベントオブジェクトの前の状態を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportwaitforsingleobject" data-raw-source="[&lt;strong&gt;VideoPortWaitForSingleObject&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportwaitforsingleobject)"><strong>VideoPortWaitForSingleObject</strong></a></p></td>
<td align="left"><p>指定されたディスパッチオブジェクトがシグナル状態に設定されるか、待機がタイムアウトするまで (必要に応じて)、現在のスレッドを待機状態にします。</p></td>
</tr>
</tbody>
</table>

 

GDI では、ドライバーを表示するイベントもサポートされています。 詳細については[、「ディスプレイドライバーでのイベントの使用](using-events-in-display-drivers.md)」を参照してください。

イベントの詳細については、「*カーネルモードドライバーの設計ガイド*」の「[イベントオブジェクト](https://docs.microsoft.com/windows-hardware/drivers/kernel/event-objects)」を参照してください。

 

 





