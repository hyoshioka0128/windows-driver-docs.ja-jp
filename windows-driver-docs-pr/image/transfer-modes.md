---
title: 転送モード
description: 転送モード
ms.assetid: 79af0d8f-dd04-4ff4-a047-f415562a16a5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b1238a65de397dbf32e684cf10afb226e65ba3f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389611"
---
# <a name="transfer-modes"></a>転送モード





静止画像インターフェイス定義の 2 つの転送モード −*ステータス モード*と*データ モード*します。 クライアントのときに、 **IStillImage** COM インターフェイス呼び出し[ **IStillImage::CreateDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff543778)静止画像デバイスへのアクセスを取得する、転送の 1 つ (または両方) を指定モードです。 複数のクライアント ステータスのモードでデバイスを開くことができますが、一度に 1 つのみのクライアントは、データ モードでデバイスを開くことができます。

静止画像イベント モニターでは、状態のモードでデバイスを開きます。 常にではありませんが、通常、[イメージの取得 Api](creating-device-specific-components-for-image-acquisition-apis.md)データ モードでデバイスを開きます。

イベント モニターをクライアントには、データ モードで、デバイスが開かれて、格納後続[デバイス イベントを静止画像](still-image-device-events.md)を内部キューにします。 場合は、クライアントが呼び出す[ **IStiDevice::Subscribe**](https://msdn.microsoft.com/library/windows/hardware/ff543768)、呼び出すことによって、キューからイベントを読み取り、 [ **IStiDevice::GetLastNotificationData** ](https://msdn.microsoft.com/library/windows/hardware/ff543751). クライアントがデバイスを閉じた後、その後に受信したイベントは、もう一度登録済みのアプリケーションを起動しようとするイベント モニタをによりします。

2 つの転送モードは、デバイスのユーザー モードのミニドライバーに完全に依存します。 **IStillImage**と**IStiDevice**インターフェイスは、どちらのモードで呼び出されるすべてのメソッドを使用します。

呼び出すことによって開かれたモードの決定できます、ミニドライバー [ **IStiDevice::GetLastNotificationData**](https://msdn.microsoft.com/library/windows/hardware/ff543751)します。 ミニドライバーは、クライアントを禁止するからデバイスへのアクセスを取得するときに、クライアントが状態モードのみを要求した場合は、データ転送を実行する必要があります。

デバイスが通常の比較的長いステータス モードで開いていることに注意してください (たとえば、イメージを読み取るように) 時間が比較的短いデータ モードで開いたときに (たとえば、デバイスのイベントのイベント モニターのウォッチ ポイント) 時刻します。 静止イメージ アーキテクチャでは、データ モードでデバイスを開くには、一度に 1 つのみのクライアントを使用できますが、デバイスへのアクセスにさらに制限を設定するためのドライバーに必要な場合があります。

たとえば、シリアル ポートに接続されているデバイスのドライバーを記述する場合を呼び出す[ **CreateFile** ](https://msdn.microsoft.com/library/windows/desktop/aa363858)からドライバーの内[ **IStiUSD::LockDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff543829)メソッド、デバイス状態モードで開いた場合。 これは他のアプリケーションを禁止する状態中に、ポートを他のデバイスをサポート可能性があります) を使用してから、デバイスから情報を取得します。

SCSI または USB バス デバイスなどの専用ポートに接続されているデバイスを呼び出す通常許容[ **CreateFile** ](https://msdn.microsoft.com/library/windows/desktop/aa363858)内から[ **IStiUSD::Initialize**](https://msdn.microsoft.com/library/windows/hardware/ff543824)かどうかステータス モードが指定されているため、デバイスとポートは常に専用にする 1 つのクライアント。

デバイスがデータ モードで開かれたときに[ **CreateFile** ](https://msdn.microsoft.com/library/windows/desktop/aa363858)は通常内から呼び出されます**IStiUSD:Initialize**バスの種類に依存しません。

 

 




