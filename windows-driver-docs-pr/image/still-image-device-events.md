---
title: 静止画像デバイスのイベント
description: 静止画像デバイスのイベント
ms.assetid: 5f9be89c-8442-4894-b2f6-a4d3558464bf
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 85d6b545966169e6c55d8028108049118329f366
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383719"
---
# <a name="still-image-device-events"></a>静止画像デバイスのイベント





A*イメージ デバイス イベントではまだ*上位レベルのソフトウェアについて、通知をデバイス レベルの出現は、そのソフトウェアがこのような通知を要求された場合。 ユーザー モード ミニドライバーは、ほとんどのデバイスのイベントを定義して、イベントが発生したときに通知を配信する責任を負います。 一般に、イベントは、上位のソフトウェアが何らかのアクションを実行する必要はしようとしていることを示しています。

静止画像の一般的なデバイスのイベントは、プッシュ ボタンが押されるの検出します。 たとえば、スキャナーは、テキストや写真のスキャンを開始するには、個別のボタンを持つユーザーを提供する可能性があります。 ボタンが押されたときに、上位のソフトウェアを表示またはイメージを格納するために必要になります。 静止画像イベント モニタは、イベントが発生したことを検出 (を使用して、 [IStiDevice COM インターフェイス](istidevice-com-interface.md)) 既に登録済み静止画像アプリケーションを呼び出すことができます (を使用して、 [IStillImage COM インターフェイス](istillimage-com-interface.md)).

まだデバイス イベントのイメージは、Guid で表されます。 *Sti.h*Microsoft は、次の静止画像デバイス イベントを定義します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>イベントの GUID</th>
<th>目的</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>GUID_DeviceArrivedLaunch</strong></p></td>
<td><p>静止画像デバイスは、システムに関連付けられているだけです。</p></td>
</tr>
<tr class="even">
<td><p><strong>GUID_ScanImage</strong></p></td>
<td><p>コンピューターにイメージをスキャンする必要があります。</p></td>
</tr>
<tr class="odd">
<td><p><strong>GUID_ScanFaxImage</strong></p></td>
<td><p>イメージをコンピューターにスキャンされ、fax で送信する必要があります。</p></td>
</tr>
<tr class="even">
<td><p><strong>GUID_ScanPrintImage</strong></p></td>
<td><p>イメージは、コンピューターをスキャンし、し、印刷する必要があります。</p></td>
</tr>
<tr class="odd">
<td><p><strong>GUID_STIUserDefined1</strong></p></td>
<td><p>ユーザー定義可能なボタンが押されました。</p></td>
</tr>
<tr class="even">
<td><p><strong>GUID_STIUserDefined2</strong></p></td>
<td><p>ユーザー定義可能なボタンが押されました。</p></td>
</tr>
<tr class="odd">
<td><p><strong>GUID_STIUserDefined3</strong></p></td>
<td><p>ユーザー定義可能なボタンが押されました。</p></td>
</tr>
</tbody>
</table>

 

ユーザー モードのミニドライバーの開発者は、可能な限りこれらのイベントの定義済み Guid を使用してください。 これらの Guid が適切でない場合は、デバイス固有のイベントの Guid を定義する必要があります。

静止画像デバイス イベントを定義するには、次の必要があります。

-   各イベントの GUID を指定します。

-   ユーザー モード ドライバーの INF ファイルには、各 GUID を含めます。

ドライバーの INF ファイル内では、各 GUID 仕様は、アスタリスク (つまり、「すべてのアプリケーション」) またはイベントの発生時にアプリケーションを開始するかを示す特定のアプリケーションの一覧のいずれかを含める必要があります。 静止画像イベント モニターでは、このリストを使用して、イベントをアプリケーションの既定の割り当てを行います。 ユーザーは、スキャナーとカメラのコントロール パネルでこれらの割り当てを変更できます。

### <a name="event-notification"></a>イベント通知

ドライバーは、(いずれかの非同期 I/O を使用またはポーリング) デバイスを監視する必要がありますを GUID ごとに関連付けられているイベントの発生時に決定します。 デバイスの機能に応じて、ドライバーを非同期的にまたはデバイスをポーリングする要求に応答することによってクライアント デバイス イベントの発生を通知できます。 (いずれかの方法) をデバイス イベントの通知を配信することができるすべてのドライバーが、STI に設定する必要があります\_GENCAP\_デバイスの通知フラグ[ **STI\_DEV\_キャップ** ](https://msdn.microsoft.com/library/windows/hardware/ff548380)構造体。 ドライバーが、ポーリングとしない非同期の通知をサポートする必要があります、STI を設定しても\_GENCAP\_ポーリング\_同じ構造にフラグが必要です。 (これらの機能を使用して指定することも必要があります、**機能**キーワード[の INF ファイルは、デバイスを静止画像](inf-files-for-still-image-devices.md))。

呼び出し、ドライバーは、イベントの非同期通知をサポートする場合、イベントの監視[ **IStiUSD::SetNotificationHandle** ](https://msdn.microsoft.com/library/windows/hardware/ff543840)通知を要求して、イベント ハンドルを指定します。 デバイス イベントの発生時、ドライバーは、呼び出すことによってイベント モニタを通知する必要があります**SetEvent** (Microsoft Windows SDK のドキュメントを参照)、引数としてイベント ハンドルを使用します。 クライアントが呼び出すことができますし、 [ **IStiUSD::GetNotificationData** ](https://msdn.microsoft.com/library/windows/hardware/ff543821) GUID のイベントを取得します。

イベントのポーリングが必要な場合は、呼び出しの監視[ **IStiUSD::GetStatus** ](https://msdn.microsoft.com/library/windows/hardware/ff543823) 、ドライバーは、デバイスと戻り値の結果をさらにポーリングする必要がありますをポーリングする、 [ **STI\_デバイス\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff548369)構造体。

 

 




