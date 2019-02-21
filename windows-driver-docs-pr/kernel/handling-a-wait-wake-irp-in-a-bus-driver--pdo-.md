---
title: 待機/ウェイク バス ドライバー (PDO) で IRP の処理
description: 待機/ウェイク バス ドライバー (PDO) で IRP の処理
ms.assetid: 9583b935-26e1-49c6-827d-932762af114d
keywords:
- 受信側の待機またはスリープ解除 Irp
- 待機/ウェイク Irp WDK の電源管理の受信
- バス ドライバー WDK 電源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9185f81649a2c637aa94ce65df560c96e5673662
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527977"
---
# <a name="handling-a-waitwake-irp-in-a-bus-driver-pdo"></a>待機/ウェイク バス ドライバー (PDO) で IRP の処理





その他の power Irp のように IRP の完了を最終的には、バス ドライバー (PDO) に IRP 待機/ウェイク デバイス スタックの一番下渡す必要があります。 IRP を受信すると、バス ドライバーがすぐに失敗するか保持する保留中の後で完了します。 以下は、バス ドライバーが実行する必要があります手順です。

1.  値を検査**Irp -&gt;Parameters.WaitWake.PowerState**します。 指定したから、デバイスが、ウェイク アップをサポートしている場合は[ **SystemWake** ](systemwake.md)状態または現在のデバイスの電源状態からではなく、ドライバーは IRP を失敗次のようにします。

    -   状態を設定\_無効な\_デバイス\_で状態**Irp -&gt;IoStatus.Status**します。

    -   IRP の完了 ([**IoCompleteRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548343))、IO の優先順位を指定する\_いいえ\_インクリメントします。

    -   設定の状態を返す**Irp -&gt;IoStatus.Status**から、 [ *DispatchPower* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチン。

2.  待機/ウェイク IRP が既に保留中かどうかを確認、pdo します。 場合、その設定**Irp -&gt;IoStatus.Status**ステータス\_デバイス\_ビジー、待機/ウェイク Irp のドライバーの内部のカウントをインクリメントし、前の手順に従って、IRP を完了します。

    1 つだけ待機/ウェイク IRP が保留されている PDO の。

3.  指定したシステムの電源状態と待機/ウェイク IRP が既に保留中デバイスは、ウェイク アップをサポートしている場合は、呼び出す[ **IoMarkIrpPending** ](https://msdn.microsoft.com/library/windows/hardware/ff549422) IRP が完了する I/O マネージャーに示すために、または後で取り消されました。 設定しないでください、 [ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)ルーチン。

4.  ウェイク アップを有効にする、デバイスのハードウェアを設定します。

    バス ドライバーにより、そのハードウェアのウェイク アップされる特定のメカニズムは、デバイスによって異なります。 PCI デバイス、Pci.sys はこのドライバーは、PME レジスタを所有しているため、PME の有効にするビットの設定を行います。 その他のデバイスでは、デバイス固有クラスのドキュメントを参照してください。

5.  PDO FDO の子である場合[要求待機/ウェイク IRP](sending-a-wait-wake-irp.md) 、FDO のために設定してください、 [*キャンセル*](https://msdn.microsoft.com/library/windows/hardware/ff540742)現在 IRP (保留中、保持している IRP) のルーチン。 渡すか、現在の IRP を再利用しないでください。

6.  状態を返す\_から PENDING、 *DispatchPower*ルーチン。

7.  ウェイク アップのシグナルを受け取ったときに呼び出す**IoCompleteRequest**保留中待機/ウェイク IRP、設定を完了する**Irp IoStatus.Status**ステータス\_成功した場合、および IO の優先順位を指定します。\_いいえ\_インクリメントします。

### <a name="for-devices-that-do-not-support-wake-up"></a>ウェイク アップをサポートしていないデバイス

デバイスがウェイク アップをサポートしていない場合、バス ドライバー (PDO) する必要がありますに従います。

1.  待機/ウェイク IRP を呼び出すことによって完了**IoCompleteRequest**、IO を指定する\_いいえ\_インクリメントします。

2.  戻り値、 *DispatchPower*で値を渡すルーチン**Irp -&gt;IoStatus.Status**戻り値として返します。

 

 




