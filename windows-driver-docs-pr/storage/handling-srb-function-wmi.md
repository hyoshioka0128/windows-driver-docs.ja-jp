---
title: SRB_FUNCTION_WMI の処理
description: SRB_FUNCTION_WMI の処理
ms.assetid: df20b9dc-1b67-4044-8abe-3cf5714076b3
keywords:
- SCSI ミニポート ドライバー WDK ストレージ、HwScsiStartIo
- HwScsiStartIo
- SRB_FUNCTION_WMI
- WMI の WDK SCSI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 463045b6073e923293fee74d3edc22093114789d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372332"
---
# <a name="handling-srbfunctionwmi"></a>処理 SRB\_関数\_WMI


## <span id="ddk_handling_srb_function_wmi_kg"></span><span id="DDK_HANDLING_SRB_FUNCTION_WMI_KG"></span>


HBA がサポートしている場合[Windows Management Instrumentation](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-wmi) (WMI)、ポート、ドライバーは WMI に要求を送信、ミニポート ドライバー。 HBA の WmiDataProvider フィールドを設定して、WMI をサポートしていることを示します、 [**ポート\_構成\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_port_configuration_information)構造体を**TRUE**でその[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)ルーチン。

ミニポート ドライバーのライターは、次のように WMI 要求を処理するミニポートを準備します。

-   ミニポートは、カスタム データのブロックまたはブロックのイベントを公開する場合は、MOF ファイルにこのようなブロックを定義する必要があり、ミニポートのバイナリの画像のバイナリ リソースとしてコンパイルします。 詳細については、次を参照してください。 [Windows Management Instrumentation](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-wmi)します。

-   必須および省略可能な実装*HwScsiWmiXxx* 」の説明に従って、コールバック ルーチン[SCSI ミニポート ドライバー ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。

-   処理 SRB\_関数\_WMI します。

ミニポート ドライバーが保留の WMI 要求場合その**DriverEntry**ルーチンは、そのメモリを要求する必要があります SRB の拡張機能、ミニポート ドライバーを維持できるため、SRB の処理全体でのコンテキストの要求に割り当てられます。

SCSI を割り当てる必要があります、ミニポート ドライバーでは、最初の WMI 要求を処理する前に\_WMILIB\_コンテキストがそのデバイスの拡張機能の構造体し、次の構造体を初期化します。

-   システムによって定義されている標準のブロックを含む、ミニポート ドライバーでサポートされているデータとイベントのブロック数*wmicore.mof*存在する場合、ミニポート ドライバーのカスタム要素とします。

-   サポートされているブロックごとに 1 つ SCSIWMIGUIDREGINFO 構造体の配列へのポインター。

-   ミニポート ドライバーへのエントリ ポイント*HwScsiWmiXxx*コールバック ルーチン。 ミニポート ドライバーには、少なくともへのエントリ ポイントを提供する必要があります、 [ **HwScsiWmiQueryReginfo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_query_reginfo)ルーチンと[ **HwScsiWmiQueryDataBlock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_query_datablock)ルーチン。

ミニポート ドライバーがそのデータを登録するアクションを実行する必要はありませんし、イベント ブロック ポートの WmiDataProvider フィールドを設定するよりもその他の\_構成\_情報構造体を**TRUE**を実装し、必要な*HwScsiWmiQueryReginfo*ルーチン。 ポート ドライバーは、WMI のカーネル コンポーネントと、ミニポート ドライバーのブロックを登録します。

これで、SRB の受信時に、**関数**SRB にメンバーが設定されている\_関数\_WMI、ミニポート ドライバーの[ **HwScsiStartIo** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557323(v=vs.85))ルーチン次:

-   割り当て、SCSIWMI\_要求\_SRB 拡張場合は、要求が保留される場合、または保留しないことが要求する場合、スタックからコンテキストの構造体。

-   チェック**Srb**- **&gt;WMIFlags**要求が、アダプターまたは論理ユニットの要求かどうかを判断します。

-   呼び出し[ **ScsiPortWmiDispatchFunction** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nf-scsiwmi-scsiportwmidispatchfunction)ミニポート ドライバーの SCSI へのポインターで\_WMILIB\_コンテキスト、そのデバイスの拡張機能および要求コンテキスト、および次SRB パラメーター:

    **Srb**- **&gt;WMISubFunction**

    **Srb**- **&gt;データパス**

    **Srb**- **&gt;DataTransferLength**

    **Srb**- **&gt;DataBuffer**

-   呼び出し[ **ScsiPortWmiPostProcess** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nf-scsiwmi-scsiportwmipostprocess)ドライバーが完了すると、要求を処理します。 かどうか、ドライバーは保留されません、要求、 **ScsiPortWmiPostProcess**はほとんどの場合、コールバック内で呼び出されます。 場合、ドライバー、要求が保留**ScsiPortWmiPostProcess**要求が完了したときに呼び出す必要があります。

-   セット**Srb**- **&gt;DataTransferLength**と**Srb**- **&gt;SrbStatus**によって返される値に[ **ScsiPortWmiGetReturnSize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nf-scsiwmi-scsiportwmigetreturnsize)と[ **ScsiPortWmiGetReturnStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nf-scsiwmi-scsiportwmigetreturnstatus)、それぞれ、

-   呼び出し[ **ScsiPortNotification** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportnotification)で**RequestComplete**ときのこ**NextRequest**または (**NextLuRequest**).

WMI の詳細については、次を参照してください。 [Windows Management Instrumentation](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-wmi)します。

 

 




