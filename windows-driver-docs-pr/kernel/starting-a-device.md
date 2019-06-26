---
title: デバイスの開始
description: デバイスの開始
ms.assetid: c52588cf-04c8-420d-a68e-a8754a65d546
keywords:
- PnP WDK カーネルでは、デバイスの起動
- プラグ アンド プレイの WDK カーネル、デバイスの起動
- PnP デバイスの起動
- DispatchPnP ルーチン
- IoCompletion ルーチン
- 失敗した開始 PnP WDK
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9614bfec6c95559a5ae08ba2b3f021e81d7a7957
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382992"
---
# <a name="starting-a-device"></a>デバイスの開始





PnP マネージャーに送信する[ **IRP\_MN\_開始\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)新しく列挙されたデバイスを起動するかが、既存のデバイスを再起動するドライバーへの要求リソースの再調整のために停止します。

関数とフィルター ドライバーを設定する必要があります、 [ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine) 、日常的なパス、 **IRP\_MN\_開始\_デバイス**ダウン要求デバイス スタック、および下位のすべてのドライバーが IRP に完了するまで、その開始操作を延期します。 親のバス ドライバー、デバイス スタックの下部にあるドライバーは、他のドライバーが、デバイスにアクセスする前に、デバイスでは、その開始操作を実行する最初のドライバーである必要があります。

開始操作が適切な順序を確実には、Windows 2000 以降のバージョンの Windows での PnP マネージャーが延期デバイス インターフェイスを公開して、IRP が成功すると開始されるまで、デバイスの要求のブロックを作成します。

デバイスのドライバーが失敗した場合、 **IRP\_MN\_開始\_デバイス**要求、PnP マネージャーに送信、 [ **IRP\_MN\_の削除\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device) (Windows 2000 以降のバージョンの Windows で) デバイス スタックを要求します。 この IRP に応答して、ドライバーは、デバイスは、(これらには、開始 IRP が成功した) 場合は、開始操作を元に戻すの元に戻す、 [ *AddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)操作、デバイス スタックからデタッチするとします。 PnP マネージャーによって、このようなデバイス「開始できませんでした」。

このセクションでは、次のトピックについて説明します。

[Function ドライバーのデバイスの開始](starting-a-device-in-a-function-driver.md)

[フィルター ドライバーでのデバイスの起動](starting-a-device-in-a-filter-driver.md)

[バス ドライバーでのデバイスの起動](starting-a-device-in-a-bus-driver.md)

[デバイスを起動するためのデザイン ガイドライン](design-guidelines-for-starting-devices.md)

 

 




