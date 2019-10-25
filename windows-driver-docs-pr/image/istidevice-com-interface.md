---
title: IStiDevice COM インターフェイス
description: IStiDevice COM インターフェイス
ms.assetid: b026fb74-9ce6-4d4e-8a5b-402731904064
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 774fd0a82e1b51c076dbcf60fb3f8f1037ca80c1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840810"
---
# <a name="istidevice-com-interface"></a>IStiDevice COM インターフェイス





**Iのデバイス**COM インターフェイスを使用すると、アプリケーションは静止イメージデバイスと通信できます。 インターフェイスメソッドを使用すると、アプリケーションは、データとコマンドを送受信したり、診断テストを実行したり、[静止イメージデバイスイベント](still-image-device-events.md)の通知を受信したり、デバイスの機能と状態情報を取得したりできます。

**Istidevice**インターフェイスへのアクセスは、 [IStillImage COM インターフェイス](istillimage-com-interface.md)の**CreateDevice**メソッドを呼び出すことによって取得されます。 [Istidevice COM インターフェイス](istiusd-com-interface.md)によって定義されているような名前付きメソッドを呼び出すことによって、 **istidevice**インターフェイスのメソッドの多くが実装されます。

次の表は、 **Iのデバイス**インターフェイスによって提供されるすべてのメソッドの一覧とその説明を示しています。 この表は、通常、各メソッドを呼び出す必要があるクライアントの種類を示しています。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>メソッド</th>
<th>説明</th>
<th>一般的な呼び出し元</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-devicereset" data-raw-source="[&lt;strong&gt;IStiDevice::DeviceReset&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-devicereset)"><strong>Ii デバイス::D eviceReset</strong></a></p></td>
<td><p>静止イメージデバイスを既知の状態にリセットします。</p></td>
<td><p>イメージ取得 Api</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-diagnostic" data-raw-source="[&lt;strong&gt;IStiDevice::Diagnostic&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-diagnostic)"><strong>Ii デバイス::D iに依存しない</strong></a></p></td>
<td><p>静止イメージデバイスで診断テストを実行します。</p></td>
<td><p>スキャナーとカメラのコントロールパネル</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-escape" data-raw-source="[&lt;strong&gt;IStiDevice::Escape&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-escape)"><strong>Ii デバイス:: Escape</strong></a></p></td>
<td><p>ベンダー固有の i/o 操作の要求を静止イメージデバイスに送信します。</p></td>
<td><p>イメージ取得 Api</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-getcapabilities" data-raw-source="[&lt;strong&gt;IStiDevice::GetCapabilities&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-getcapabilities)"><strong>Ia デバイス:: GetCapabilities</strong></a></p></td>
<td><p>静止イメージデバイスの機能を返します。</p></td>
<td><p>静止画像イベントモニタ</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-getlasterror" data-raw-source="[&lt;strong&gt;IStiDevice::GetLastError&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-getlasterror)"><strong>Ii デバイス:: GetLastError</strong></a></p></td>
<td><p>静止イメージデバイスに関連付けられている最後の既知のエラーを返します。</p></td>
<td><p>イメージ取得 Api</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-getlasterrorinfo" data-raw-source="[&lt;strong&gt;IStiDevice::GetLastErrorInfo&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-getlasterrorinfo)"><strong>Ia デバイス:: GetLastErrorInfo</strong></a></p></td>
<td><p>静止イメージデバイスに関連付けられている最後の既知のエラーに関する情報を返します。</p></td>
<td><p>イメージ取得 Api</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-getlastnotificationdata" data-raw-source="[&lt;strong&gt;IStiDevice::GetLastNotificationData&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-getlastnotificationdata)"><strong>Iのデバイス:: GetLastNotificationData</strong></a></p></td>
<td><p>静止イメージデバイスで発生した最新のイベントの説明を返します。</p></td>
<td><p>イメージ取得 Api</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-getstatus" data-raw-source="[&lt;strong&gt;IStiDevice::GetStatus&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-getstatus)"><strong>Ii デバイス:: GetStatus</strong></a></p></td>
<td><p>静止イメージデバイスの状態情報を返します。</p></td>
<td><p>イメージ取得 Api と静止画像イベントモニター</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-initialize" data-raw-source="[&lt;strong&gt;IStiDevice::Initialize&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-initialize)"><strong>Ii デバイス:: Initialize</strong></a></p></td>
<td><p>オブジェクトインスタンスを初期化します。</p></td>
<td><p>直接呼び出されない</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-lockdevice" data-raw-source="[&lt;strong&gt;IStiDevice::LockDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-lockdevice)"><strong>Ii デバイス:: LockDevice</strong></a></p></td>
<td><p>呼び出し元によって排他的に使用されるようにデバイスをロックします。</p></td>
<td><p>すべての<strong>Ii デバイス</strong>インターフェイスクライアント</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-rawreadcommand" data-raw-source="[&lt;strong&gt;IStiDevice::RawReadCommand&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-rawreadcommand)"><strong>IStiDevice:: RawReadCommand</strong></a></p></td>
<td><p>静止イメージデバイスからコマンド情報を読み取ります。</p></td>
<td><p>イメージ取得 Api</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-rawreaddata" data-raw-source="[&lt;strong&gt;IStiDevice::RawReadData&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-rawreaddata)"><strong>Ii デバイス:: RawReadData</strong></a></p></td>
<td><p>静止イメージデバイスからデータを読み取ります。</p></td>
<td><p>イメージ取得 Api</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-rawwritecommand" data-raw-source="[&lt;strong&gt;IStiDevice::RawWriteCommand&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-rawwritecommand)"><strong>IStiDevice:: RawWriteCommand</strong></a></p></td>
<td><p>コマンド情報を静止イメージデバイスに送信します。</p></td>
<td><p>イメージ取得 Api</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-rawwritedata" data-raw-source="[&lt;strong&gt;IStiDevice::RawWriteData&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-rawwritedata)"><strong>IStiDevice:: RawWriteData</strong></a></p></td>
<td><p>静止イメージデバイスにデータを書き込みます。</p></td>
<td><p>イメージ取得 Api</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-release" data-raw-source="[&lt;strong&gt;IStiDevice::Release&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-release)"><strong>Ii デバイス:: リリース</strong></a></p></td>
<td><p>オブジェクトインスタンスを閉じ、 <strong>Iのデバイス</strong>インターフェイスへのアクセスを削除します。</p></td>
<td><p>すべての<strong>Ii デバイス</strong>インターフェイスクライアント</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-subscribe" data-raw-source="[&lt;strong&gt;IStiDevice::Subscribe&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-subscribe)"><strong>Ia デバイス:: Subscribe</strong></a></p></td>
<td><p>デバイスイベントの通知を受信するように呼び出し元を登録します。</p></td>
<td><p>イメージ取得 Api</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-unlockdevice" data-raw-source="[&lt;strong&gt;IStiDevice::UnLockDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-unlockdevice)"><strong>Ii デバイス:: UnLockDevice</strong></a></p></td>
<td><p>デバイスのロックを解除します。</p></td>
<td><p>すべての<strong>Ii デバイス</strong>インターフェイスクライアント</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-unsubscribe" data-raw-source="[&lt;strong&gt;IStiDevice::UnSubscribe&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-unsubscribe)"><strong>Ii デバイス:: 登録解除</strong></a></p></td>
<td><p>デバイスイベントの通知を受信するために登録されているアプリケーションの一覧から呼び出し元を削除します。</p></td>
<td><p>イメージ取得 Api</p></td>
</tr>
</tbody>
</table>

 

 

 




