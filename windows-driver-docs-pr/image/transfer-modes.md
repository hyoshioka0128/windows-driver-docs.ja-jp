---
title: 転送モード
description: 転送モード
ms.assetid: 79af0d8f-dd04-4ff4-a047-f415562a16a5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 59e858b0d2d4d45612f393f3c1887031194142c4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840734"
---
# <a name="transfer-modes"></a>転送モード





静止イメージインターフェイスは、*ステータスモード*と*データモード*という2つの転送モードを定義します。 **IStillImage** COM インターフェイスのクライアントが[**IStillImage:: CreateDevice**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff543778(v=vs.85))を呼び出して、静止イメージデバイスへのアクセスを取得する場合は、転送モードの一方 (または両方) を指定します。 複数のクライアントがステータスモードでデバイスを開くことはできますが、一度に1つのクライアントだけがデータモードでデバイスを開けるようにすることができます。

静止画像イベントモニターは、状態モードでデバイスを開きます。 通常、[イメージ取得 api](creating-device-specific-components-for-image-acquisition-apis.md)はデータモードでデバイスを開きますが、常にではありません。

クライアントがデータモードでデバイスを開いた後、イベントモニターは、後続の[静止イメージデバイスイベント](still-image-device-events.md)を内部キューに格納します。 クライアントが[**istidevice:: Subscribe**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-subscribe)を呼び出すと、 [**Istidevice:: GetLastNotificationData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-getlastnotificationdata)を呼び出すことによって、キューからイベントを読み取ることができます。 クライアントがデバイスを閉じた後でイベントを受信すると、イベントモニターは登録されたアプリケーションを再び開始しようとします。

2つの転送モードの意味は、デバイスのユーザーモードミニドライバーに完全に依存しています。 IStillImage インターフェイスと**i デバイス**インターフェイスを使用すると、いずれのモードでもすべてのメソッドを呼び出すことができます。

ミニドライバーは、 [**Istidevice:: GetLastNotificationData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-getlastnotificationdata)を呼び出すことによって、それが開かれたモードを特定できます。 ミニドライバーは、デバイスへのアクセスを取得するときにクライアントがステータスモードのみを要求した場合に、クライアントがデータ転送を実行できないようにする必要があります。

デバイスは通常、ステータスモードで比較的長い時間 (たとえば、イベントモニターがデバイスイベントを監視します) で開かれますが、比較的短い時間 (画像を読み取るなど) のためにデータモードで開かれていることに注意してください。 静止画像アーキテクチャでは、一度に1つのクライアントのみがデータモードでデバイスを開くことができますが、デバイスへのアクセスについて、ドライバーが追加の制限を設定する必要がある場合があります。

たとえば、シリアルポートに接続されているデバイスのドライバーを作成する場合、デバイスがステータスモードで開かれている場合は、ドライバーの[**ib usd:: LockDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-lockdevice)メソッド内から[**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)を呼び出すことができます。 これにより、デバイスからステータス情報が取得されている間に、他のアプリケーションがポート (他のデバイスをサポートしている可能性があります) を使用できなくなります。

SCSI や USB バスデバイスなどの専用ポートに接続されているデバイスの場合、デバイスとポートは常に専用であるため、状態モードが指定されている場合は、 [**Istype usd:: Initialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-initialize)内から[**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)を呼び出すことができます。client.

デバイスがデータモードで開かれている場合、通常、 [**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)は、バスの種類に関係なく、 **istype usd: Initialize**内から呼び出されます。

 

 




