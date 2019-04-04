---
title: 個々 のデバイスの電源 Irp
description: 個々 のデバイスの電源 Irp
ms.assetid: a8d5db12-8f6b-4c65-9814-0bc3e476dd1c
keywords:
- 電源 Irp WDK カーネル、デバイス
- デバイスの電源の Irp WDK カーネル
- 電源のシーケンス値の WDK カーネル
- 動作状態は、WDK の電源管理を返します
- アクティブになるデバイス
- 電源管理のウェイク アップ機能 WDK
- デバイスのスリープ解除 ups WDK 電源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 745120e7270a05fca085e969fb0066770c806d9f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539108"
---
# <a name="power-irps-for-individual-devices"></a>個々 のデバイスの電源 Irp





A*デバイスの電源 IRP* IRP の主要なコードを指定します[ **IRP\_MJ\_POWER**](https://msdn.microsoft.com/library/windows/hardware/ff550784)、1 つ以下に示すマイナー power IRP コードと値**DevicePowerState**で、 **Power.Type**メンバー。

[**IRP\_MN\_クエリ\_電源**](https://msdn.microsoft.com/library/windows/hardware/ff551699)

[**IRP\_MN\_SET\_POWER**](https://msdn.microsoft.com/library/windows/hardware/ff551744)

[**IRP\_MN\_待機\_WAKE**](https://msdn.microsoft.com/library/windows/hardware/ff551766)

[**IRP\_MN\_POWER\_シーケンス**](https://msdn.microsoft.com/library/windows/hardware/ff551644)

デバイス スタックのすべてのドライバーです。 このような Irp を受信します。通常、デバイス電源ポリシー マネージャーだけでは、これらの Irp を送信できます。 しかし、電源マネージャー送信がデバイスの電源 IRP に代わって、デバイスをアイドル状態の検出を実行するときにで説明したよう[電源マネージャー ルーチンをアイドル状態の検出を使用して](using-power-manager-routines-for-idle-detection.md)します。

ドライバーは、次の理由のいずれかのデバイスの電源 IRP を送信します。

-   クエリまたはシステム電源 IRP への応答でデバイスの電源状態を変更するには

-   デバイスを電源を節約するためにスリープ状態にするには

-   スリープ状態になっています後に、デバイスを動作状態に戻る

-   外部からの信号への応答がスリープ解除するデバイスを有効にするには

-   デバイスの電源を入れたときに電源シーケンス値を取得するには

次の図は、一連の送信、転送、するために発生し、デバイスの電源 IRP の完了手順を示します。

![デバイスの電源 irp のパスを示す図](images/devpoirp.png)

前の図に示すよう IRP が送信されると、デバイスの電源は、転送し、次の手順で完了します。

1.  デバイスの電源ポリシー所有者呼び出し[ **PoRequestPowerIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff559734) IRP のデバイスの電源を割り当てるには、PDO IRP と IRP の完了時に呼び出されるコールバック ルーチンの対象となっているを指定します。

2.  電源マネージャーは、デバイスの電源 IRP を割り当てます、ターゲット PDO デバイス スタックの最上位のドライバーに送信します。

3.  ドライバーは、次の操作を実行します。

    -   セット、 [ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)ルーチンのいずれかが必要な場合。

    -   呼び出し[ **PoStartNextPowerIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff559776) (Windows Server 2003、Windows XP、および Windows 2000) 完了ルーチンを使用しない場合。 Windows Vista 以降、この呼び出しは必要ありませんし、このような呼び出しには電源管理操作は実行されません。

    -   呼び出し[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336) (Windows 7 および Windows Vista) または呼び出し[ **PoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff559654) (の Windows Server 2003、Windows XP、および Windows 2000) を次の下位ドライバーに IRP を渡します。

    スタック内の各ドライバーは IRP バス ドライバーに到達するまで、します。 すぐに実行する必要があります、呼び出すし、ドライバーは IRP を失敗する必要があります、 [ **IoCompleteRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548343)します。

4.  デバイス PDO を保持するには、バス ドライバーが要求されたアクションを実行しを呼び出して**IoCompleteRequest** IRP を完了します。 バス ドライバーには、デバイスが失敗する可能性がパワーアップ IRP デバイスが削除される場合、または削除処理中です。

5.  I/O マネージャー呼び出し*IoCompletion* IRP が渡されるときに、ドライバーによって設定されたルーチンがスタックをダウンします。 結局、 *IoCompletion*ルーチンが呼び出された、コールバック ルーチンを実行します。

デバイスの電源 Irp の詳細については、[個々 のデバイスを管理する Power](managing-power-for-individual-devices.md)と[サポート デバイスがあるウェイク アップ機能](supporting-devices-that-have-wake-up-capabilities.md)を参照してください。 電源シーケンス IRP の詳細については、「 [ **IRP\_MN\_POWER\_シーケンス**](https://msdn.microsoft.com/library/windows/hardware/ff551644)します。

 

 




