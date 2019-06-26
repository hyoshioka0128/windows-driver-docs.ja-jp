---
title: 転送モード
description: 転送モード
ms.assetid: 79af0d8f-dd04-4ff4-a047-f415562a16a5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 81704a52aff4ad3f27fc15c440e49ca136cd54c9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358230"
---
# <a name="transfer-modes"></a>転送モード





静止画像インターフェイス定義の 2 つの転送モード −*ステータス モード*と*データ モード*します。 クライアントのときに、 **IStillImage** COM インターフェイス呼び出し[ **IStillImage::CreateDevice** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff543778(v=vs.85))静止画像デバイスへのアクセスを取得する、転送の 1 つ (または両方) を指定モードです。 複数のクライアント ステータスのモードでデバイスを開くことができますが、一度に 1 つのみのクライアントは、データ モードでデバイスを開くことができます。

静止画像イベント モニターでは、状態のモードでデバイスを開きます。 常にではありませんが、通常、[イメージの取得 Api](creating-device-specific-components-for-image-acquisition-apis.md)データ モードでデバイスを開きます。

イベント モニターをクライアントには、データ モードで、デバイスが開かれて、格納後続[デバイス イベントを静止画像](still-image-device-events.md)を内部キューにします。 場合は、クライアントが呼び出す[ **IStiDevice::Subscribe**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-subscribe)、呼び出すことによって、キューからイベントを読み取り、 [ **IStiDevice::GetLastNotificationData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-getlastnotificationdata). クライアントがデバイスを閉じた後、その後に受信したイベントは、もう一度登録済みのアプリケーションを起動しようとするイベント モニタをによりします。

2 つの転送モードは、デバイスのユーザー モードのミニドライバーに完全に依存します。 **IStillImage**と**IStiDevice**インターフェイスは、どちらのモードで呼び出されるすべてのメソッドを使用します。

呼び出すことによって開かれたモードの決定できます、ミニドライバー [ **IStiDevice::GetLastNotificationData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-getlastnotificationdata)します。 ミニドライバーは、クライアントを禁止するからデバイスへのアクセスを取得するときに、クライアントが状態モードのみを要求した場合は、データ転送を実行する必要があります。

デバイスが通常の比較的長いステータス モードで開いていることに注意してください (たとえば、イメージを読み取るように) 時間が比較的短いデータ モードで開いたときに (たとえば、デバイスのイベントのイベント モニターのウォッチ ポイント) 時刻します。 静止イメージ アーキテクチャでは、データ モードでデバイスを開くには、一度に 1 つのみのクライアントを使用できますが、デバイスへのアクセスにさらに制限を設定するためのドライバーに必要な場合があります。

たとえば、シリアル ポートに接続されているデバイスのドライバーを記述する場合を呼び出す[ **CreateFile** ](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)からドライバーの内[ **IStiUSD::LockDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-lockdevice)メソッド、デバイス状態モードで開いた場合。 これは他のアプリケーションを禁止する状態中に、ポートを他のデバイスをサポート可能性があります) を使用してから、デバイスから情報を取得します。

SCSI または USB バス デバイスなどの専用ポートに接続されているデバイスを呼び出す通常許容[ **CreateFile** ](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)内から[ **IStiUSD::Initialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-initialize)かどうかステータス モードが指定されているため、デバイスとポートは常に専用にする 1 つのクライアント。

デバイスがデータ モードで開かれたときに[ **CreateFile** ](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)は通常内から呼び出されます**IStiUSD:Initialize**バスの種類に依存しません。

 

 




