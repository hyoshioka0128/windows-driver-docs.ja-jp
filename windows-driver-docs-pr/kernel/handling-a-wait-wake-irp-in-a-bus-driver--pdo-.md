---
title: バス ドライバー (PDO) での待機/ウェイク IRP の処理
description: バス ドライバー (PDO) での待機/ウェイク IRP の処理
ms.assetid: 9583b935-26e1-49c6-827d-932762af114d
keywords:
- 待機/ウェイク Irp の受信
- 待機/ウェイク Irp WDK 電源管理、受信
- バスドライバーの WDK 電源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6bb0e76278833de1559b728c7b51c3ae65b1a773
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836609"
---
# <a name="handling-a-waitwake-irp-in-a-bus-driver-pdo"></a>バス ドライバー (PDO) での待機/ウェイク IRP の処理





他の電源 Irp と同様に、各待機/ウェイク IRP を、デバイススタックからバスドライバー (PDO) に渡す必要があります。これは、最終的に IRP の完了を担当します。 バスドライバーは、IRP を受け取るとすぐに失敗するか、後で完了するために保留中のままにすることができます。 バスドライバーで実行する必要がある手順は次のとおりです。

1.  **Irp-&gt;Parameters. PowerState**の値を調べます。 デバイスがウェイクアップをサポートしていても、指定した[**Systemwake**](systemwake.md)状態からではなく、現在のデバイスの電源状態からのものではない場合、ドライバーは次のように IRP を失敗させる必要があります。

    -   状態\_無効\_デバイス\_状態が**Irp-&gt;IoStatus. STATUS**に設定されています。

    -   IRP ([**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)) を完了します。 IO の priority boost\_\_増分は指定しません。

    -   [*DispatchPower*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンから、 **Irp-&gt;iostatus. status**に設定されている状態を返します。

2.  待機/ウェイク IRP が PDO に対して既に保留中であるかどうかを確認します。 その場合は、[ **Irp-&gt;iostatus. status** ] を [STATUS\_DEVICE\_BUSY] に設定し、ドライバーの内部の待機/ウェイク irp の数を増やして、前の手順で説明したように irp を完了します。

    1つの PDO に対して保留できる待機/ウェイク IRP は1つだけです。

3.  デバイスが、指定されたシステム電源状態からのウェイクアップをサポートしていて、待機中の待機時間が既に保留中でない場合は、 [**Iomarkirppending**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)を呼び出して、IRP が完了するか、後でキャンセルされることを i/o マネージャーに示します。 [*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンを設定しないでください。

4.  デバイスのハードウェアをウェイクアップを有効にするように設定します。

    バスドライバーがウェイクアップ用にハードウェアを使用できるようにする特定のメカニズムは、デバイスによって異なります。 PCI デバイスの場合、このドライバーは PME 登録を所有しているため、Pci は PME-enable ビットを設定する必要があります。 その他のデバイスについては、デバイスクラス固有のドキュメントを参照してください。

5.  PDO が FDO の子である場合は、FDO の[待機/ウェイク IRP を要求](sending-a-wait-wake-irp.md)し、現在の irp (保留中の irp) に対して[*キャンセル*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel)ルーチンを設定します。 現在の IRP を成功させたり再利用したりしないでください。

6.  *DispatchPower*ルーチンから STATUS\_PENDING が返されます。

7.  ウェイクアップシグナルが到着したら、 **IoCompleteRequest**を呼び出して、保留中の待機/ウェイク IRP を完了し**ます。 IRP-iostatus を完了し、Irp-iostatus**を status\_SUCCESS に設定し、IO の priority boost\_\_インクリメントを指定します。

### <a name="for-devices-that-do-not-support-wake-up"></a>ウェイクアップをサポートしていないデバイスの場合

デバイスがウェイクアップをサポートしていない場合、バスドライバー (PDO) は次のように処理する必要があります。

1.  **IoCompleteRequest**を呼び出して wait/wake IRP を完了します。 IO\_\_増分は指定しません。

2.  *DispatchPower*ルーチンから戻り値として、 **Irp-&gt;Iostatus. Status**の値を戻り値として渡します。

 

 




