---
title: IStiDevice COM インターフェイス
description: IStiDevice COM インターフェイス
ms.assetid: b026fb74-9ce6-4d4e-8a5b-402731904064
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 702ed90d5cc5efa4935ee084454cce47461469d0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529968"
---
# <a name="istidevice-com-interface"></a>IStiDevice COM インターフェイス





**IStiDevice** COM インターフェイスと通信する機能をアプリケーションがデバイスを静止画像を提供します。 インターフェイス メソッドを使用すると、アプリケーション データとの通知を受け取る診断テストを実行するコマンド、送受信[イメージ デバイス イベントではまだ](still-image-device-events.md)とデバイスの機能と状態情報を取得します。

アクセス、 **IStiDevice**インターフェイスを呼び出すことによって取得、 **CreateDevice**のメソッド、 [IStillImage COM インターフェイス](istillimage-com-interface.md)します。 多くは、 **IStiDevice**によって定義された同じ名前のメソッドを呼び出すことによってインターフェイスのメソッドが実装されている、 [IStiUSD COM インターフェイス](istiusd-com-interface.md)します。

次の表とすべてのによって提供されるメソッドについて説明します、 **IStiDevice**インターフェイス。 テーブルでは、通常、各メソッドを呼び出す必要のあるクライアントの種類を示します。

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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543733" data-raw-source="[&lt;strong&gt;IStiDevice::DeviceReset&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543733)"><strong>IStiDevice::DeviceReset</strong></a></p></td>
<td><p>静止画像デバイスを既知の状態にリセットします。</p></td>
<td><p>イメージの取得 Api</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543736" data-raw-source="[&lt;strong&gt;IStiDevice::Diagnostic&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543736)"><strong>IStiDevice::Diagnostic</strong></a></p></td>
<td><p>静止画像デバイスで診断テストを実行します。</p></td>
<td><p>スキャナーとカメラのコントロール パネル</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543740" data-raw-source="[&lt;strong&gt;IStiDevice::Escape&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543740)"><strong>IStiDevice::Escape</strong></a></p></td>
<td><p>静止画像デバイスには、ベンダー固有の I/O 操作の要求を送信します。</p></td>
<td><p>イメージの取得 Api</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543745" data-raw-source="[&lt;strong&gt;IStiDevice::GetCapabilities&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543745)"><strong>IStiDevice::GetCapabilities</strong></a></p></td>
<td><p>静止画像デバイスを返します&#39;機能します。</p></td>
<td><p>イベント モニターを静止画像します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543747" data-raw-source="[&lt;strong&gt;IStiDevice::GetLastError&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543747)"><strong>IStiDevice::GetLastError</strong></a></p></td>
<td><p>静止画像デバイスに関連付けられている最後の既知のエラーを返します。</p></td>
<td><p>イメージの取得 Api</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543749" data-raw-source="[&lt;strong&gt;IStiDevice::GetLastErrorInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543749)"><strong>IStiDevice::GetLastErrorInfo</strong></a></p></td>
<td><p>静止画像デバイスに関連付けられている最後の既知のエラーに関する情報を返します。</p></td>
<td><p>イメージの取得 Api</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543751" data-raw-source="[&lt;strong&gt;IStiDevice::GetLastNotificationData&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543751)"><strong>IStiDevice::GetLastNotificationData</strong></a></p></td>
<td><p>静止画像デバイスで発生した最新のイベントの説明を返します。</p></td>
<td><p>イメージの取得 Api</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543752" data-raw-source="[&lt;strong&gt;IStiDevice::GetStatus&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543752)"><strong>IStiDevice::GetStatus</strong></a></p></td>
<td><p>静止画像デバイスを返します&#39;s 状態情報。</p></td>
<td><p>イメージの取得 Api と、まだイベント モニターの画像</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543754" data-raw-source="[&lt;strong&gt;IStiDevice::Initialize&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543754)"><strong>IStiDevice::Initialize</strong></a></p></td>
<td><p>オブジェクトのインスタンスを初期化します。</p></td>
<td><p>直接呼び出されません</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543756" data-raw-source="[&lt;strong&gt;IStiDevice::LockDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543756)"><strong>IStiDevice::LockDevice</strong></a></p></td>
<td><p>呼び出し元によって排他的に使用のデバイスをロックします。</p></td>
<td><p>すべて<strong>IStiDevice</strong>クライアント インターフェイス</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543758" data-raw-source="[&lt;strong&gt;IStiDevice::RawReadCommand&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543758)"><strong>IStiDevice::RawReadCommand</strong></a></p></td>
<td><p>読み取りは、静止画像デバイスからの情報をコマンドします。</p></td>
<td><p>イメージの取得 Api</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543760" data-raw-source="[&lt;strong&gt;IStiDevice::RawReadData&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543760)"><strong>IStiDevice::RawReadData</strong></a></p></td>
<td><p>静止画像デバイスからデータを読み取ります。</p></td>
<td><p>イメージの取得 Api</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543762" data-raw-source="[&lt;strong&gt;IStiDevice::RawWriteCommand&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543762)"><strong>IStiDevice::RawWriteCommand</strong></a></p></td>
<td><p>送信は、静止画像デバイス情報をコマンドします。</p></td>
<td><p>イメージの取得 Api</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543764" data-raw-source="[&lt;strong&gt;IStiDevice::RawWriteData&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543764)"><strong>IStiDevice::RawWriteData</strong></a></p></td>
<td><p>静止画像デバイスにデータを書き込みます。</p></td>
<td><p>イメージの取得 Api</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543765" data-raw-source="[&lt;strong&gt;IStiDevice::Release&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543765)"><strong>IStiDevice::Release</strong></a></p></td>
<td><p>オブジェクトのインスタンスを閉じて、アクセス権を削除、 <strong>IStiDevice</strong>インターフェイス。</p></td>
<td><p>すべて<strong>IStiDevice</strong>クライアント インターフェイス</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543768" data-raw-source="[&lt;strong&gt;IStiDevice::Subscribe&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543768)"><strong>IStiDevice::Subscribe</strong></a></p></td>
<td><p>デバイス イベントの通知を受け取る、呼び出し元を登録します。</p></td>
<td><p>イメージの取得 Api</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543770" data-raw-source="[&lt;strong&gt;IStiDevice::UnLockDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543770)"><strong>IStiDevice::UnLockDevice</strong></a></p></td>
<td><p>デバイスのロックを解除します。</p></td>
<td><p>すべて<strong>IStiDevice</strong>クライアント インターフェイス</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543773" data-raw-source="[&lt;strong&gt;IStiDevice::UnSubscribe&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543773)"><strong>IStiDevice::UnSubscribe</strong></a></p></td>
<td><p>デバイス イベントの通知に登録されているアプリケーションの一覧から、呼び出し元を削除します。</p></td>
<td><p>イメージの取得 Api</p></td>
</tr>
</tbody>
</table>

 

 

 




