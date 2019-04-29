---
title: IStillImage COM インターフェイス
description: IStillImage COM インターフェイス
ms.assetid: eb60a3fd-e7e2-4d3c-973e-af8cb3c3c511
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab0bc581ed9f55041b2d45f82df87fcf6e40caf5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327032"
---
# <a name="istillimage-com-interface"></a>IStillImage COM インターフェイス





**IStillImage** COM インターフェイスへのアクセスを提供して、[イメージ イベント モニターではまだ](overview-of-sti-components.md#ddk-still-image-event-monitor-si)のため、アプリケーションが自身を「プッシュ モデル対応」として登録します。 アプリケーションでは、システムの静止画像デバイス情報を入手するのにこのインターフェイスを使用できます。

インターフェイスは、イベント通知を有効にして、カスタマイズされたアプリケーションの管理ソフトウェアによって使用される、アプリケーションの起動など、一部のアプリケーション管理機能を提供します。

さらに、 **IStillImage**インターフェイスへのアクセスを提供する、 [IStiDevice COM インターフェイス](istidevice-com-interface.md)アプリケーションの静止画像デバイスの I/O 操作を実行することができます。

次の表とすべての記述、 **IStillImage**インターフェイスのメソッド。 テーブルでは、通常、各メソッドを呼び出す必要のあるクライアントの種類を示します。

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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543778" data-raw-source="[&lt;strong&gt;IStillImage::CreateDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543778)"><strong>IStillImage::CreateDevice</strong></a></p></td>
<td><p>定義する COM オブジェクトのインスタンスを作成、 <strong>IStiDevice</strong>インターフェイス、およびインターフェイスへのポインターを返します。</p></td>
<td><p>イメージの取得 Api</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543780" data-raw-source="[&lt;strong&gt;IStillImage::EnableHwNotifications&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543780)"><strong>IStillImage::EnableHwNotifications</strong></a></p></td>
<td><p>有効またはアプリケーションの通知を無効にとき<a href="still-image-device-events.md" data-raw-source="[Still Image Device Events](still-image-device-events.md)">イメージ デバイス イベントではまだ</a>の指定されたデバイスで発生します。</p></td>
<td><p>イベント モニターを静止画像します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543782" data-raw-source="[&lt;strong&gt;IStillImage::GetDeviceInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543782)"><strong>IStillImage::GetDeviceInfo</strong></a></p></td>
<td><p>静止画像を指定したデバイスのハードウェアの特性を返します。</p></td>
<td><p>イメージの取得 Api</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543784" data-raw-source="[&lt;strong&gt;IStillImage::GetDeviceList&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543784)"><strong>IStillImage::GetDeviceList</strong></a></p></td>
<td><p>まだイメージのデバイスですべてのハードウェア特性を返しますがインストールされています。</p></td>
<td><p>スキャナーとカメラのコントロール パネル、イメージの取得 Api</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543786" data-raw-source="[&lt;strong&gt;IStillImage::GetDeviceValue&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543786)"><strong>IStillImage::GetDeviceValue</strong></a></p></td>
<td><p>静止画像を指定したデバイスに関連付けられたレジストリ情報を返します。</p></td>
<td><p>イメージの取得 Api、スキャナーとカメラのコントロール パネル</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543788" data-raw-source="[&lt;strong&gt;IStillImage::GetHwNotificationState&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543788)"><strong>IStillImage::GetHwNotificationState</strong></a></p></td>
<td><p>指定されたデバイスで発生したデバイス イベントのイメージのままに、アプリケーションを通知するかどうかを示します。</p></td>
<td><p>イベント モニターを静止画像します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543790" data-raw-source="[&lt;strong&gt;IStillImage::GetSTILaunchInformation&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543790)"><strong>IStillImage::GetSTILaunchInformation</strong></a></p></td>
<td><p>静止画像イベント モニターで開始された場合、呼び出し元は、アプリケーションを静止画像理由が開始されたを返します。</p></td>
<td><p>プッシュ モデル対応のアプリケーション</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543793" data-raw-source="[&lt;strong&gt;IStillImage::Initialize&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543793)"><strong>IStillImage::Initialize</strong></a></p></td>
<td><p>オブジェクトのインスタンスを初期化します。</p></td>
<td><p>直接呼び出されません</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543796" data-raw-source="[&lt;strong&gt;IStillImage::LaunchApplicationForDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543796)"><strong>IStillImage::LaunchApplicationForDevice</strong></a></p></td>
<td><p>静止画像を指定したデバイスの指定したアプリケーションを起動します。</p></td>
<td><p>イベント モニターを静止画像します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543798" data-raw-source="[&lt;strong&gt;IStillImage::RegisterLaunchApplication&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543798)"><strong>IStillImage::RegisterLaunchApplication</strong></a></p></td>
<td><p>プッシュ モデル対応のアプリケーションの静止のイメージ イベント モニターの一覧にアプリケーションを追加します。</p></td>
<td><p>プッシュ モデル対応するアプリケーションまたはそのインストーラー</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543799" data-raw-source="[&lt;strong&gt;IStillImage::Release&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543799)"><strong>IStillImage::Release</strong></a></p></td>
<td><p>オブジェクトのインスタンスを閉じて、アクセス権を削除、 <strong>IStillImage</strong>インターフェイス。</p></td>
<td><p>すべて<strong>IStillImage</strong>クライアント インターフェイス</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543801" data-raw-source="[&lt;strong&gt;IStillImage::SetDeviceValue&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543801)"><strong>IStillImage::SetDeviceValue</strong></a></p></td>
<td><p>静止画像を指定したデバイスのレジストリ情報を設定します。</p></td>
<td><p>スキャナーとカメラのコントロール パネル</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543803" data-raw-source="[&lt;strong&gt;IStillImage::SetupDeviceParameters&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543803)"><strong>IStillImage::SetupDeviceParameters</strong></a></p></td>
<td><p>クライアント、 <strong>IStillImage</strong>静止画像デバイスの変更をインターフェイスの特性を格納します。</p></td>
<td><p>スキャナーとカメラのコントロール パネル</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543804" data-raw-source="[&lt;strong&gt;IStillImage::StiCreateInstance&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543804)"><strong>IStillImage::StiCreateInstance</strong></a></p></td>
<td><p>定義する COM オブジェクトのインスタンスを作成、 <strong>IStillImage</strong>インターフェイス、およびインターフェイスへのポインターを返します。</p></td>
<td><p>すべて<strong>IStillImage</strong>クライアント インターフェイス</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543806" data-raw-source="[&lt;strong&gt;IStillImage::UnregisterLaunchApplication&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543806)"><strong>IStillImage::UnregisterLaunchApplication</strong></a></p></td>
<td><p>プッシュ モデル対応のアプリケーションの静止のイメージ イベント モニターの一覧からアプリケーションを削除します。</p></td>
<td><p>プッシュ モデル対応するアプリケーションまたはそのインストーラー</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543807" data-raw-source="[&lt;strong&gt;IStillImage::WriteToErrorLog&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543807)"><strong>IStillImage::WriteToErrorLog</strong></a></p></td>
<td><p>静止画像エラー ログにメッセージを書き込みます。</p></td>
<td><p>すべて<strong>IStillImage</strong>クライアント インターフェイス</p></td>
</tr>
</tbody>
</table>

 

 

 




