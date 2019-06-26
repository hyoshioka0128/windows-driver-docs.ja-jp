---
title: HwScsiFindAdapter に関するポート ドライバー提供の ConfigInfo
description: HwScsiFindAdapter に関するポート ドライバー提供の ConfigInfo
ms.assetid: 9691f47d-1ea8-4ef6-8e0d-57570ff70a16
keywords:
- HwScsiFindAdapter
- SCSI ミニポート ドライバー WDK ストレージ、HwScsiFindAdapter
- ConfigInfo
- ConfigInfo WDK SCSI のドライバーによって提供されるポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 58697e462a94a881caced31c40cfc4d373ee800f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358459"
---
# <a name="port-driver-supplied-configinfo-for-hwscsifindadapter"></a>HwScsiFindAdapter に関するポート ドライバー提供の ConfigInfo


## <span id="ddk_port_driver_supplied_configinfo_for_hwscsifindadapter_kg"></span><span id="DDK_PORT_DRIVER_SUPPLIED_CONFIGINFO_FOR_HWSCSIFINDADAPTER_KG"></span>


システムのポート ドライバーは、常に、次のよう設定[**ポート\_構成\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_port_configuration_information)ミニポート ドライバーを呼び出す前に*HwScsiFindAdapter*ポートへのポインターとルーチン\_構成\_情報 (、 *ConfigInfo*バッファー)。

-   **長さ**に**sizeof**(ポート\_構成\_情報)

-   **AdapterInterfaceType**ミニポート ドライバーの[ **HW\_初期化\_データ (SCSI)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_hw_initialization_data)仕様

-   **InterruptMode**に**LevelSensitive** PCI バスまたは**Latched**他のすべてのバスの種類

    ミニポート ドライバーがにない場合*HwScsiInterrupt*ルーチンとセット、 **HwInterrupt**へのエントリ ポイント**NULL**ハードウェア ベース\_の初期化\_データは、このメンバーには関係ありません。

-   **AtdiskPrimaryClaimed**に**TRUE** 0x1F0 に 0x1FF I/O ポートの範囲を使用してドライバーを以前に読み込まれた場合

-   **AtdiskSecondaryClaimed**に**TRUE** 0x170 に 0x17F I/O ポートの範囲を使用してドライバーを以前に読み込まれた場合

-   **NumberOfAccessRanges**ミニポート ドライバーのハードウェアに\_初期化\_データの指定

-   **Dma64BitAddresses**ミニポート ドライバーのハードウェアに\_初期化\_システムに 4 GB を超える物理アドレスを持つメモリがある場合、データの指定

ポート ドライバーは、また、従来のミニポート ドライバーまたはプラグ アンド プレイのミニポート ドライバーのプラグ アンド プレイ マネージャーから、レジストリなど、システムに他のソースから値を持つ次のメンバーを入力しようとします。

-   **SystemIoBusNumber** I/O バスのシステムによって割り当てられた値に設定

    ミニポート ドライバーの[ *HwScsiFindAdapter* ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557300(v=vs.85))の各バスのルーチンを呼び出すことが、指定された**AdapterInterfaceType**の更新された値を持つ**SystemIoBusNumber**、システムの特定のバス上の HBA を検出した場合、システムで決定された値に設定できますか、指定された**AdapterInterfaceType**します。

-   **AccessRanges**型へのアクセスの要素\_bus 相対で設定されている範囲 **%rangestart**アドレスと**RangeLength**、および各範囲のかどうかは、 **RangeInMemory**

    **RangeInMemory**設定**FALSE** I/O の領域でポートの範囲ではなくメモリ領域の範囲を示します。

    ポート ドライバーがいずれかのアクセスのすべての情報を提供\_または範囲の要素が 0 (既定値) に要素のすべてのメンバーを設定します。 通常、ポート、ドライバーは、アクセスの範囲の非ゼロ値を提供する場合、追加の構成情報を提供します。

    ミニポート ドライバーでポート ドライバーによって提供される相対バスへのアクセス範囲値をマップする必要があります[ **ScsiPortGetDeviceBase** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportgetdevicebase)論理アドレスが割り当てられた値を使用してを決定するかどうか、対応する HBA は、ドライバーをサポートしています。 *決して*マップし、バス上の HBA へのアクセス ポート ドライバー、ポート範囲要素に塗りつぶされたアクセスを提供する場合に、ミニポート ドライバーが指定した範囲を使用して\_構成\_に渡す情報、 *HwScsiFindAdapter*ルーチン。 ポート ドライバーには、範囲の構成情報が提供されているときに、ミニポート ドライバーが指定したアドレスを使用して、機能しなくなるので、既に構成されている HBA をリセットしたり、システムのブート プロセスが失敗するおそれもできます。

    詳細については、マップされた論理アクセスの範囲を使用して、次を参照してください。 [HwScsiFindAdapter で ConfigInfo セットアップ](setting-up-configinfo-in-hwscsifindadapter.md)します。

-   **BusInterruptLevel**または**BusInterruptVector**

    このメンバーは、ミニポート ドライバーがにない場合は、関連は[ **HwScsiInterrupt** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557312(v=vs.85))ルーチン。

-   **できます**または**DmaPort** HBA システム DMA コント ローラーを使用している場合

    HBA は、バス マスターまたは PIO を使用して、これらのメンバーは関係ありません。

-   **InitiatorBusId**

    場合、入力**InitiatorBusId\[0\]** 値が 0 がその HBA には、HBA をクエリすることによって決定されます。 特定の値の使用が必要としない場合、ミニポート ドライバーは、既定値を割り当てることができます。 それ以外の場合、ミニポート ドライバーでは、可能であればポート ドライバーによって割り当てられている 0 以外の値を使用する必要があります。 すべてのミニポート ドライバーを更新する必要があります**InitiatorBusId**適切な値 (秒) を決定する HBA のクエリを実行するために必要な場合、その HBA の使用と一致する仕様。

    値によって示される、ミニポート ドライバーは、HBA でサポートされている各 SCSI バスのエントリを設定する必要があります**NumberOfBuses**します。

 

 




