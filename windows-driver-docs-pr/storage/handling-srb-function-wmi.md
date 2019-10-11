---
title: SRB_FUNCTION_WMI の処理
description: SRB_FUNCTION_WMI の処理
ms.assetid: df20b9dc-1b67-4044-8abe-3cf5714076b3
keywords:
- SCSI ミニポートドライバー WDK 記憶域、HwScsiStartIo
- HwScsiStartIo
- SRB_FUNCTION_WMI
- WMI WDK SCSI
ms.date: 10/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: 96d490a71d205ef19bb0f89a73c777228cd082aa
ms.sourcegitcommit: 5f4252ee4d5a72fa15cf8c68a51982c2bc6c8193
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/10/2019
ms.locfileid: "72252405"
---
# <a name="handling-srb_function_wmi"></a>SRB_FUNCTION_WMI の処理

ホストバスアダプター (HBA) で[Windows Management Instrumentation](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-wmi) (wmi) がサポートされている場合、ポートドライバーはミニポートドライバーに wmi 要求を送信します。 HBA は、 [**Driverentry**](driverentry-of-scsi-miniport-driver.md)ルーチンで[*PORT_CONFIGURATION_INFORMATION*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_port_configuration_information)構造体の [の設定] を**TRUE**に設定することによって、WMI をサポートしていることを示しています。

ミニポートドライバーのライターは、次のように、WMI 要求を処理するようにミニポートを準備します。

- ミニポートがカスタムデータブロックまたはイベントブロックを公開する場合は、そのようなブロックを MOF ファイルで定義し、ミニポートのバイナリイメージでバイナリリソースとしてコンパイルする必要があります。 詳細については、「 [Windows Management Instrumentation](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-wmi)」を参照してください。

- 「 [SCSI ミニポートドライバールーチン](scsi-miniport-driver-routines.md)」で説明されているように、必須および省略可能な*HwScsiWmiXxx*コールバックルーチンを実装します。

- SRB_FUNCTION_WMI を処理します。

ミニポートドライバーが WMI 要求を保留している場合、その**Driverentry**ルーチンは、SRB 拡張機能にメモリを割り当てるように要求する必要があります。これにより、ミニポートドライバーは SRB の処理中に要求コンテキストを維持できるようになります。

ミニポートドライバーは、最初の WMI 要求を処理する前に、デバイス拡張機能に SCSI_WMILIB_CONTEXT 構造体を割り当て、次のように構造体を初期化する必要があります。

- ミニポートドライバーによってサポートされるデータおよびイベントブロックの数。 *wmicore*のシステムで定義されている標準ブロックと、ミニポートドライバーのカスタムブロック (存在する場合) が含まれます。

- サポートされているブロックごとに1つずつ、SCSIWMIGUIDREGINFO 構造体の配列へのポインター。

- エントリポイントは、ミニポートドライバーの*HwScsiWmiXxx*コールバックルーチンを指します。 少なくとも、ミニポートドライバーは、 [*HwScsiWmiQueryReginfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_query_reginfo)ルーチンと[*HwScsiWmiQueryDataBlock*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_query_datablock)ルーチンへのエントリポイントを提供する必要があります。

ミニポートドライバーでは、PORT_CONFIGURATION_INFO 構造体の設定を**TRUE**に設定し、必要な*HwScsiWmiQueryReginfo*ルーチンを実装する以外に、データおよびイベントブロックを登録するために何らかのアクションを実行する必要はありません. ポートドライバーは、ミニポートドライバーのブロックを WMI カーネルコンポーネントに登録します。

**関数**メンバーが SRB_FUNCTION_WMI に設定されている SRB を受信すると、ミニポートドライバーの[*HwScsiStartIo*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557323(v=vs.85))ルーチンは次のように実行します。

- 要求が保留される可能性がある場合は SRB 拡張機能から SCSIWMI_REQUEST_CONTEXT 構造体を割り当て、要求が保留されない場合はスタックから割り当てます。

- **> Srb の Wmi フラグ**をチェックして、要求がアダプターまたは論理ユニットのどちらに対するものかを判断します。

- ミニポートドライバーの SCSI_WMILIB_CONTEXT、そのデバイス拡張機能、および要求コンテキストへのポインターと、SRB からの次のパラメーターを使用して、 [**ScsiPortWmiDispatchFunction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nf-scsiwmi-scsiportwmidispatchfunction)を呼び出します。

    **Srb-> WMISubFunction**

    **Srb-> データパス**

    **Srb-> Datatransの長さ**

    **Srb-> DataBuffer**

- ドライバーが要求の処理を終了したときに[**ScsiPortWmiPostProcess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nf-scsiwmi-scsiportwmipostprocess)を呼び出します。 ドライバーが要求を保留していない場合、コールバックで**ScsiPortWmiPostProcess**が呼び出される可能性が最も高くなります。 ドライバーが要求を pends した場合は、要求が完了したときに**ScsiPortWmiPostProcess**を呼び出す必要があります。

- **> Srb Datatrans length**と**Srb > srbstatus**をそれぞれ[**ScsiPortWmiGetReturnSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nf-scsiwmi-scsiportwmigetreturnsize)と[**ScsiPortWmiGetReturnStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nf-scsiwmi-scsiportwmigetreturnstatus)によって返される値にそれぞれ設定します。

- **Requestcomplete**と**nextrequest**または (**nextlurequest**) を使用して[**ScsiPortNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportnotification)を呼び出します。

WMI の詳細については、「 [Windows Management Instrumentation](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-wmi)」を参照してください。
