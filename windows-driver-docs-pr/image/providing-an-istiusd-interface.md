---
title: IStiUSD インターフェイスを提供します。
description: IStiUSD インターフェイスを提供します。
ms.assetid: ed15b56b-0b63-4983-a4ff-df379a2b9de9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f4a10d6c07ecb3a20bf3a24f530c1d178e3b4df
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560657"
---
# <a name="providing-an-istiusd-interface"></a>IStiUSD インターフェイスを提供します。





WIA は STI に基づいています。 STI に WIA ミニドライバーの統合を確保するために、ミニドライバーがから派生したインターフェイスを実装する必要があります、 [IStiUSD インターフェイス メソッド](https://msdn.microsoft.com/library/windows/hardware/ff543827)します。 このインターフェイスは、WIA ミニドライバーに存在する必要があります。 **IStiUSD**インターフェイス (ドライバーの読み込み) などのデバイスを管理するために使用および手段が、 [IStiDevice インターフェイス メソッド](https://msdn.microsoft.com/library/windows/hardware/ff543755)静止画像デバイスと通信します。 ミニドライバーはから派生したインターフェイスを完全に実装する必要があります、 [ **IStiUSD::Initialize** ](https://msdn.microsoft.com/library/windows/hardware/ff543824) WIA サービスによって読み込まれるメソッド。

通常、 **IStiUSD**インターフェイス メソッドは、によって定義された同じ名前のメソッドによって呼び出される、 **IStiDevice**インターフェイス。 ミニドライバーを通常実装**IStiUSD**インターフェイス メソッドを呼び出して、適切なカーネル モード ドライバー。 各ミニドライバーがメソッドでない場合は、すべてのインターフェイス メソッドを定義する必要がありますに必要なだけを返すこと STIERR\_サポートされていません。

参照してください、 *wiacam*カメラ ミニドライバー サンプルファイル*IStiUSD.cpp*、ミニドライバーを実装する方法の例については、 **IStiUSD**インターフェイス。

次の表とによって定義されたメソッドのすべてについて説明します、 **IStiUSD**インターフェイス。 メソッドを実装または WIA ミニドライバーで条件付きで実装する必要がありますが識別されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>メソッド</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543812" data-raw-source="[&lt;strong&gt;IStiUSD::DeviceReset&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543812)"><strong>IStiUSD::DeviceReset</strong></a></p></td>
<td><p>静止画像デバイスを正常に初期化された状態にリセットします。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543814" data-raw-source="[&lt;strong&gt;IStiUSD::Diagnostic&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543814)"><strong>IStiUSD::Diagnostic</strong></a></p></td>
<td><p>静止画像デバイスでは、診断テストを実行します。 WIA ミニドライバーは、このメソッドを実装する必要があります。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543815" data-raw-source="[&lt;strong&gt;IStiUSD::Escape&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543815)"><strong>IStiUSD::Escape</strong></a></p></td>
<td><p>静止画像デバイスのベンダー固有の I/O 操作を実行します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543817" data-raw-source="[&lt;strong&gt;IStiUSD::GetCapabilities&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543817)"><strong>IStiUSD::GetCapabilities</strong></a></p></td>
<td><p>静止画像デバイスを返します&#39;機能します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543820" data-raw-source="[&lt;strong&gt;IStiUSD::GetLastErrorInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543820)"><strong>IStiUSD::GetLastErrorInfo</strong></a></p></td>
<td><p>静止画像デバイスに関連付けられている最後の既知のエラーに関する情報を返します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543821" data-raw-source="[&lt;strong&gt;IStiUSD::GetNotificationData&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543821)"><strong>IStiUSD::GetNotificationData</strong></a></p></td>
<td><p>静止画像デバイスで発生した最新のイベントの説明を返します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543823" data-raw-source="[&lt;strong&gt;IStiUSD::GetStatus&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543823)"><strong>IStiUSD::GetStatus</strong></a></p></td>
<td><p>静止画像デバイスの状態を返します。 WIA ミニドライバーは、そのデバイスにイベントを生成するには、ボタンなどのオブジェクトがある場合、このメソッドを実装する必要があります。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543824" data-raw-source="[&lt;strong&gt;IStiUSD::Initialize&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543824)"><strong>IStiUSD::Initialize</strong></a></p></td>
<td><p>定義する COM オブジェクトのインスタンスを初期化します、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff543827" data-raw-source="[IStiUSD interface](https://msdn.microsoft.com/library/windows/hardware/ff543827)">IStiUSD インターフェイス</a>します。 WIA ミニドライバーは、このメソッドを実装する必要があります。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543829" data-raw-source="[&lt;strong&gt;IStiUSD::LockDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543829)"><strong>IStiUSD::LockDevice</strong></a></p></td>
<td><p>呼び出し元によって排他的に使用のデバイスをロックします。 WIA ミニドライバーは、このメソッドを実装する必要があります。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543831" data-raw-source="[&lt;strong&gt;IStiUSD::RawReadCommand&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543831)"><strong>IStiUSD::RawReadCommand</strong></a></p></td>
<td><p>読み取りは、静止画像デバイスからの情報をコマンドします。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543834" data-raw-source="[&lt;strong&gt;IStiUSD::RawReadData&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543834)"><strong>IStiUSD::RawReadData</strong></a></p></td>
<td><p>静止画像デバイスからデータを読み取ります。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543836" data-raw-source="[&lt;strong&gt;IStiUSD::RawWriteCommand&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543836)"><strong>IStiUSD::RawWriteCommand</strong></a></p></td>
<td><p>静止画像デバイスにコマンド情報を書き込みます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543839" data-raw-source="[&lt;strong&gt;IStiUSD::RawWriteData&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543839)"><strong>IStiUSD::RawWriteData</strong></a></p></td>
<td><p>静止画像デバイスにデータを書き込みます。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543840" data-raw-source="[&lt;strong&gt;IStiUSD::SetNotificationHandle&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543840)"><strong>IStiUSD::SetNotificationHandle</strong></a></p></td>
<td><p>デバイス イベントの呼び出し元に通知するために、ミニドライバーが使用する必要がありますイベント ハンドルを指定します。 WIA ミニドライバーは、そのデバイスにイベントを生成するには、ボタンなどのオブジェクトがある場合、このメソッドを実装する必要があります。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543843" data-raw-source="[&lt;strong&gt;IStiUSD::UnLockDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543843)"><strong>IStiUSD::UnLockDevice</strong></a></p></td>
<td><p>デバイスのポートを閉じます。 WIA ミニドライバーは、このメソッドを実装する必要があります。</p></td>
</tr>
</tbody>
</table>

 

 

 




