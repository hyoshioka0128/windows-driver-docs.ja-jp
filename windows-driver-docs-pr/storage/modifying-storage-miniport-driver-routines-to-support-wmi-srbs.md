---
title: WMI される Srb をサポートする記憶域ミニポート ドライバー、ルーチンの変更
description: WMI される Srb をサポートする記憶域ミニポート ドライバー、ルーチンの変更
ms.assetid: c3a222e8-dd02-4e45-b3e2-cec35d3abfdc
keywords:
- WMI される Srb WDK の記憶域をサポートするルーチンの変更
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2b8184f8419852b73991423297b660faef2a2f83
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560569"
---
# <a name="modifying-storage-miniport-driver-routines-to-support-wmi-srbs"></a>WMI される Srb をサポートする記憶域ミニポート ドライバー、ルーチンの変更


## <span id="ddk_modifying_storage_miniport_driver_routines_to_support_wmi_srbs_kg"></span><span id="DDK_MODIFYING_STORAGE_MINIPORT_DRIVER_ROUTINES_TO_SUPPORT_WMI_SRBS_KG"></span>


ミニポート ドライバーでは、WMI される Srb をサポートできますが、前に、ミニポート ドライバーが必要なに含まれていることを確認する必要があります[ **HwScsiWmiQueryReginfo** ](https://msdn.microsoft.com/library/windows/hardware/ff557344)ルーチンとに指定されたアクションが実行される、次のルーチン:

[ **SCSI ミニポート ドライバーの DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff552654)ルーチン。

-   ミニポート ドライバーでは、SCSI ポート WMI ライブラリを使用する場合は、初期化、 [ **SCSI\_WMILIB\_コンテキスト**](https://msdn.microsoft.com/library/windows/hardware/ff565395)に記載されている構造体[SCSI ポート WMI を使用ライブラリ](using-the-scsi-port-wmi-library.md)します。

-   ポート ドライバーに SRB の拡張機能のメモリを割り当てる必要があるかどうかを示します。 ミニポート ドライバーでは、SRB の拡張機能を設定して割り当てる必要があることを示します、 **SrbExtensionSize**のメンバー、 [ **HW\_初期化\_データ (SCSI)** ](https://msdn.microsoft.com/library/windows/hardware/ff557456) 0 以外の値構造体。

[ *HwScsiFindAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff557300)ルーチン。

-   設定、 **WmiDataProvider**のメンバー、 [**ポート\_構成\_情報 (SCSI)** ](https://msdn.microsoft.com/library/windows/hardware/ff563900)構造体と等しい**は TRUE。**.

[ **HwScsiStartIo** ](https://msdn.microsoft.com/library/windows/hardware/ff557323)ルーチン。

-   テスト**関数**SRB と等しいかどうかを SRB のメンバー\_関数\_WMI します。 この条件は、場合**TRUE**、ミニポート ドライバーは、SRB の型を処理する必要があります[ **SCSI\_WMI\_要求\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff565397)ではなく型の SRB より[ **SCSI\_要求\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff565393)します。

-   メモリを割り当てる、 [ **SCSIWMI\_要求\_コンテキスト**](https://msdn.microsoft.com/library/windows/hardware/ff564946) SRB のコンテキストを保持する構造体。 場合は、ミニポート ドライバーには、WMI 要求の保留が可能性があります、ミニポート ドライバーが、SRB の処理全体での要求コンテキストを維持できるように、SRB の拡張機能からメモリを割り当てます。 それ以外の場合、要求は、これまで保留にする可能性がない場合、スタックからコンテキストのメモリを割り当てます。

-   確認**Srb**-&gt;**WMIFlags**要求が、アダプターまたは論理ユニットのかどうかを判断します。

-   SCSI ポート WMI ライブラリのディスパッチ ルーチンを呼び出す[ **ScsiPortWmiDispatchFunction**](https://msdn.microsoft.com/library/windows/hardware/ff564766)します。 このディスパッチ ルーチンを呼び出す方法の詳細については、[SCSI ポート WMI ライブラリを使用して](using-the-scsi-port-wmi-library.md)を参照してください。

-   呼び出す[ **ScsiPortWmiPostProcess** ](https://msdn.microsoft.com/library/windows/hardware/ff564796)ドライバーによって保留された場合、要求を処理した後。 かどうか、ドライバーが保留されません、要求し**ScsiPortWmiPostProcess**ミニポート ドライバーの I/O ルーチンを開始するのではなく、ミニポート ドライバー コールバック ルーチンを呼び出す必要があります。

-   設定**Srb**-&gt;**DataTransferLength**と**Srb**-&gt;**SrbStatus**によって返される値に[ **ScsiPortWmiGetReturnSize** ](https://msdn.microsoft.com/library/windows/hardware/ff564789)と[ **ScsiPortWmiGetReturnStatus** ](https://msdn.microsoft.com/library/windows/hardware/ff564791)それぞれします。

-   呼び出す[ **ScsiPortNotification** ](https://msdn.microsoft.com/library/windows/hardware/ff564657)で**RequestComplete**ときのこ**NextRequest**または (**NextLuRequest**).

 

 




