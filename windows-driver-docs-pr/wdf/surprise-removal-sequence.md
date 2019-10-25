---
title: 突然の取り外しのシーケンス
description: 突然の取り外しのシーケンス
ms.assetid: 5A89BEDA-BAC3-476F-99B3-4E6E6DDDE5F5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 98c6c625597bd4a86c37b233dd8b1f0d32491a85
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831667"
---
# <a name="surprise-removal-sequence"></a>突然の取り外しのシーケンス


ユーザーが警告なしでデバイスを削除した場合は、デバイスマネージャーまたはハードウェアの安全な取り外しユーティリティを使用せずにデバイスを取り外すだけで、デバイスは "突然削除されました" と見なされます。 この問題が発生すると、フレームワークは若干異なる削除シーケンスに従います。 また、デバイスが物理的に存在する場合でも、別のドライバーがデバイスで[**IoInvalidateDeviceState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinvalidatedevicestate)を呼び出すと、予期しない順序に従います。 予期しない削除シーケンスでは、フレームワークは、削除シーケンス内の他のコールバックを呼び出す前に、 [*EvtDeviceSurpriseRemoval*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_surprise_removal)コールバックを呼び出します。 シーケンスが完了すると、フレームワークはデバイスオブジェクトを破棄します。 すべてのリムーバブルデバイスのドライバーでは、シャットダウンパスとスタートアップパスの両方のコールバックが障害、特にハードウェアの削除によって発生するエラーを処理できることを確認する必要があります。 ハードウェアにアクセスしようとすると、無制限に待機することはありませんが、タイムアウトまたはウォッチドッグタイマーが適用される必要があります。

次の図は、突然の削除に関係するコールバックを示しています。

![予期しない削除の順序](images/surprise-removal.png)

デバイスが削除されても動作状態にならなかった場合、フレームワークは[*EvtDeviceSurpriseRemoval*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_surprise_removal)の直後に[*EvtDeviceReleaseHardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)イベントコールバックを呼び出します。 これは、デバイスが動作状態から終了したときに既に実行されていたステップを省略します。

 

 





