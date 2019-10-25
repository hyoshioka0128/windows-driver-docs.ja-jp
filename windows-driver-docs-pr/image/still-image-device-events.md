---
title: 静止画像デバイスのイベント
description: 静止画像デバイスのイベント
ms.assetid: 5f9be89c-8442-4894-b2f6-a4d3558464bf
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 099ab5af5aa14525e3db36aa435140500764d0cf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840747"
---
# <a name="still-image-device-events"></a>静止画像デバイスのイベント





*静止イメージデバイスイベント*は、ソフトウェアが通知を要求した場合に、上位レベルのソフトウェアに通知する必要があるデバイスレベルのイベントです。 ユーザーモードミニドライバーは、ほとんどのデバイスイベントを定義し、イベントが発生したときに通知を配信します。 一般に、イベントは、何らかのアクションを実行するために、上位レベルのソフトウェアが必要であることを示します。

一般的な静止イメージデバイスイベントは、押されたプッシュボタンの検出です。 たとえば、スキャナーは、テキストや写真のスキャンを開始するためのボタンをユーザーに提供する場合があります。 ボタンを押すと、イメージを表示または保存するために、上位レベルのソフトウェアが必要になります。 静止イメージイベントモニタは、( [IIStillImage](istidevice-com-interface.md)com インターフェイスを使用して) イベントが発生したことを検出し、以前に登録された静止イメージアプリケーションを呼び出すことができます ( [COM インターフェイス](istillimage-com-interface.md)を使用)。

静止イメージデバイスイベントは Guid によって表されます。 *Sti*では、Microsoft は次の静止イメージデバイスイベントを定義します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>イベント GUID</th>
<th>目的</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>GUID_DeviceArrivedLaunch</strong></p></td>
<td><p>静止イメージデバイスがシステムにアタッチされたばかりです。</p></td>
</tr>
<tr class="even">
<td><p><strong>GUID_ScanImage</strong></p></td>
<td><p>イメージをコンピューターでスキャンする必要があります。</p></td>
</tr>
<tr class="odd">
<td><p><strong>GUID_ScanFaxImage</strong></p></td>
<td><p>イメージをコンピューターにスキャンして、fax を送信する必要があります。</p></td>
</tr>
<tr class="even">
<td><p><strong>GUID_ScanPrintImage</strong></p></td>
<td><p>イメージをコンピューターにスキャンしてから印刷する必要があります。</p></td>
</tr>
<tr class="odd">
<td><p><strong>GUID_STIUserDefined1</strong></p></td>
<td><p>ユーザー定義のボタンが押されました。</p></td>
</tr>
<tr class="even">
<td><p><strong>GUID_STIUserDefined2</strong></p></td>
<td><p>ユーザー定義のボタンが押されました。</p></td>
</tr>
<tr class="odd">
<td><p><strong>GUID_STIUserDefined3</strong></p></td>
<td><p>ユーザー定義のボタンが押されました。</p></td>
</tr>
</tbody>
</table>

 

ユーザーモードミニドライバーの開発者は、可能な限りこれらの定義済みイベント Guid を使用する必要があります。 これらの Guid が適切でない場合は、デバイス固有のイベントの Guid を定義する必要があります。

静止イメージデバイスイベントを定義するには、次のことを行う必要があります。

-   各イベントの GUID を指定します。

-   ユーザーモードドライバーの INF ファイルに各 GUID を含めます。

ドライバーの INF ファイル内では、各 GUID 指定にアスタリスク ("すべてのアプリケーション") または特定のアプリケーションの一覧が含まれている必要があります。これは、イベントの発生時にどのアプリケーションを起動する必要があるかを示します。 静止画像イベントモニタは、この一覧を使用して、アプリケーションのイベントへの既定の割り当てを提供します。 ユーザーは、[スキャナーとカメラ] コントロールパネルを使用して、これらの割り当てを変更できます。

### <a name="event-notification"></a>イベント通知

ドライバーは、(非同期 i/o またはポーリングを使用して) デバイスを監視し、各 GUID に関連付けられているイベントがいつ発生するかを判断する必要があります。 デバイスの機能に応じて、ドライバーは、デバイスイベントの発生をクライアントに非同期で通知することも、デバイスのポーリング要求に応答してクライアントに通知することもできます。 デバイスイベントの通知を配信できるすべてのドライバー (いずれの方法でも) は、デバイスの[**sti\_DEV\_CAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sti/ns-sti-_sti_dev_caps)構造体で、STI\_GENCAP\_通知フラグを設定する必要があります。 非同期通知ではなく、ポーリングをサポートするドライバーも、同じ構造内の\_GENCAP\_ポーリング\_必要なフラグを設定する必要があります。 (これらの機能は、[イメージデバイス用の INF ファイル](inf-files-for-still-image-devices.md)の**capabilities**キーワードを使用しても指定する必要があります)。

ドライバーがイベントの非同期通知をサポートしている場合、イベントモニターは[**Istiusd:: SetNotificationHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-setnotificationhandle)を呼び出して通知を要求し、イベントハンドルを提供します。 デバイスイベントが発生した場合、ドライバーは、イベントハンドルを引数として使用して、 **SetEvent**を呼び出すことによってイベントモニターに通知する必要があります (Microsoft Windows SDK のドキュメントを参照してください)。 その後、クライアントは、 [**I、usd:: GetNotificationData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getnotificationdata)を呼び出して、イベントの GUID を取得できます。

ポーリングが必要な場合、イベントモニターは[**IGetStatus usd::** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getstatus)を呼び出してドライバーをポーリングします。これにより、デバイスをポーリングして、[**デバイス\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sti/ns-sti-_sti_device_status)構造体の STI\_に結果を返す必要があります。

 

 




