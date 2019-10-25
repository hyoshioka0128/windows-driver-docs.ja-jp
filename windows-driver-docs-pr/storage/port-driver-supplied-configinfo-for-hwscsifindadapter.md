---
title: HwScsiFindAdapter に関するポート ドライバー提供の ConfigInfo
description: HwScsiFindAdapter に関するポート ドライバー提供の ConfigInfo
ms.assetid: 9691f47d-1ea8-4ef6-8e0d-57570ff70a16
keywords:
- HwScsiFindAdapter
- SCSI ミニポートドライバー WDK 記憶域、HwScsiFindAdapter
- ConfigInfo
- ポートドライバーが提供する ConfigInfo WDK SCSI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 31c2d0d689f74c5fe3b91bea1d43904fdd1272f7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842726"
---
# <a name="port-driver-supplied-configinfo-for-hwscsifindadapter"></a>HwScsiFindAdapter に関するポート ドライバー提供の ConfigInfo


## <span id="ddk_port_driver_supplied_configinfo_for_hwscsifindadapter_kg"></span><span id="DDK_PORT_DRIVER_SUPPLIED_CONFIGINFO_FOR_HWSCSIFINDADAPTER_KG"></span>


システムポートドライバーは、ポート\_構成\_情報を指すポインターを使用してミニポートドライバーの*HwScsiFindAdapter*ルーチンを呼び出す前に、次の[**ポート\_構成\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_port_configuration_information)を常に設定します (*Configinfo*バッファー):

-   **Sizeof**(ポート\_構成\_情報) の**長さ**

-   **AdapterInterfaceType**をミニポートドライバーの[**ハードウェア\_初期化\_データ (SCSI)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_hw_initialization_data)仕様にする

-   PCI バス**の場合**は**InterruptMode** 、その他のすべての種類のバスには**ラッチ**

    ミニポートドライバーに*HwScsiInterrupt*ルーチンが含まれておらず、そのために、HW\_初期化\_データの**HwInterrupt**エントリポイントが**NULL**に設定されている場合、このメンバーは無関係です。

-   以前に読み込まれたドライバーで i/o ポート範囲0x1F0 と0x1FF が使用されている場合、 **AtdiskPrimaryClaimed**は**TRUE**になります。

-   以前に読み込まれたドライバーで i/o ポート範囲0x170 から0X170 を使用している場合は、 **AtdiskSecondaryClaimed**を**TRUE**にします。

-   **Numberofaccessranges**をミニポートドライバーのハードウェア\_初期化\_データ仕様に設定します。

-   システムに 4 GB を超える物理アドレスを持つメモリがある場合は、ミニポートドライバーの HW\_初期化\_データ**仕様に準拠します**。

また、ポートドライバーは、次のメンバーにシステム内の他のソースの値 (レガシミニポートドライバーの場合はレジストリ、プラグアンドプレイミニポートドライバーの場合はプラグアンドプレイマネージャー) の値を設定しようとします。

-   I/o バスのシステム割り当て値に設定された**SystemIoBusNumber**

    ミニポートドライバーの[*HwScsiFindAdapter*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557300(v=vs.85))ルーチンは、指定された**AdapterInterfaceType**の各バスに対して**SystemIoBusNumber**の値を更新して呼び出すことができます。また、システムによって検出された HBA が指定された**AdapterInterfaceType**の特定のバス。

-   **Accessranges**型の要素は、アクセス\_範囲の要素、バス相対**Rangestart**アドレスと**RangeLength**を使用して設定します。また、各範囲が**rangestart**であるかどうかを示します。

    **Rangeinmemory**が**FALSE**に設定されている場合は、メモリ領域の範囲ではなく、i/o 領域のポートの範囲を示します。

    ポートドライバーは、ACCESS\_範囲要素内のすべての情報を提供するか、要素のすべてのメンバーを (既定値) 0 に設定します。 通常、ポートドライバーは、アクセス範囲に0以外の値を提供する場合、追加の構成情報を提供します。

    ミニポートドライバーは、ポートドライバーによって指定されたバス相対アクセス範囲の値を[**ScsiPortGetDeviceBase**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportgetdevicebase)にマップし、対応する HBA がドライバーでサポートされているものであるかどうかを判断するために、マップされた論理アドレスの値を使用する必要があります。 ポート\_構成\_のポートに入力されたアクセス範囲要素がポートドライバーによって提供されている場合*は、ポート*ドライバーによってバス上の HBA にアクセスするために、ミニポートドライバーが提供する範囲をマップして使用し*ない*でください。 ポートドライバーによって指定されたアドレスを使用してポートドライバーが指定した範囲構成情報の場合、既に構成されている HBA をリセットしたり、不充足を行ったり、システムがブートプロセスを失敗させることもできます。

    マップされた論理アクセス範囲の使用の詳細については、「 [HwScsiFindAdapter での ConfigInfo の設定](setting-up-configinfo-in-hwscsifindadapter.md)」を参照してください。

-   **BusInterruptLevel**または**BusInterruptVector**

    ミニポートドライバーに[**HwScsiInterrupt**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557312(v=vs.85))ルーチンがない場合、このメンバーは無関係です。

-   **DmaChannel**または**DmaPort** (HBA がシステム DMA コントローラーを使用する場合)

    HBA がバスマスターまたは PIO を使用している場合、これらのメンバーは関係ありません。

-   **InitiatorBusId**

    入力**InitiatorBusId\[0\]** の値が0の場合は、HBA が hba を照会することによって決定された特定の値を使用する必要がない場合、ミニポートドライバーは既定値を割り当てることができます。 それ以外の場合、可能であれば、ポートドライバーによって割り当てられる0以外の値をミニポートドライバーで使用する必要があります。 すべてのミニポートドライバーは、hba が使用するものと一致するように**InitiatorBusId**の仕様を更新する必要があります。必要に応じて、hba を照会して適切な値を決定します。

    ミニポートドライバーでは、 **numberofbuses**の値によって示されるように、HBA でサポートされている各 SCSI バスのエントリを設定する必要があります。

 

 




