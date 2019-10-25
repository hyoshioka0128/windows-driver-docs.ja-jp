---
title: デバイスの開始
description: デバイスの開始
ms.assetid: c52588cf-04c8-420d-a68e-a8754a65d546
keywords:
- PnP WDK カーネル、開始デバイス
- WDK カーネルのプラグアンドプレイ、デバイスの起動
- PnP デバイスの開始
- DispatchPnP ルーチン
- IoCompletion ルーチン
- 失敗した WDK PnP の開始
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 332a15b203efc5e357474696ac2f37d963ead42f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836239"
---
# <a name="starting-a-device"></a>デバイスの開始





PnP マネージャーは、新しい列挙デバイスを開始するか、リソースの再調整のために停止された既存のデバイスを再起動するために、ドライバーに\_デバイスの要求を[**開始する\_、IRP\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)を送信します。

関数ドライバーとフィルタードライバーは、 [*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンを設定し、irp\_に渡して、デバイススタックを**開始\_デバイス**の要求\_渡し、すべての下位ドライバーが IRP で終了するまで開始操作を延期する必要があります。 デバイススタック内の下位ドライバーである親バスドライバーは、デバイスが他のドライバーによってアクセスされる前に、デバイスで開始操作を実行する最初のドライバーである必要があります。

開始操作が適切にシーケンス処理されるようにするために、Windows 2000 以降のバージョンの Windows 上の PnP マネージャーは、デバイスインターフェイスの公開を延期し、開始 IRP が成功するまでデバイスの要求作成要求をブロックします。

デバイスのドライバーが、\_デバイスの要求を開始\_として**irp\_** 失敗した場合、PnP マネージャーは、デバイススタックに\_デバイスの要求を削除\_(windows 2000 以降のバージョンの windows で) [**irp\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)を送信します。 この IRP に応答して、デバイスのドライバーによって開始操作が元に戻され (start IRP が成功した場合)、その[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)操作が元に戻され、デバイススタックからデタッチされます。 PnP マネージャーは、このようなデバイスの "起動に失敗しました" とマークします。

このセクションでは、次のトピックについて説明します。

[関数ドライバーでのデバイスの起動](starting-a-device-in-a-function-driver.md)

[フィルタードライバーでデバイスを起動する](starting-a-device-in-a-filter-driver.md)

[バスドライバーでのデバイスの起動](starting-a-device-in-a-bus-driver.md)

[デバイスを起動するための設計ガイドライン](design-guidelines-for-starting-devices.md)

 

 




