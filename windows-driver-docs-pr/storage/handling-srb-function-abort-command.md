---
title: SRB_FUNCTION_ABORT_COMMAND の処理
description: SRB_FUNCTION_ABORT_COMMAND の処理
ms.assetid: 74d46df6-2e3e-45d8-bedb-a81a80a0aec1
keywords:
- SCSI ミニポートドライバー WDK 記憶域、HwScsiStartIo
- HwScsiStartIo
- SRB_FUNCTION_ABORT_COMMAND
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e606be54c4d7d450fc97a39058b21866f2dd0ec7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826261"
---
# <a name="handling-srb_function_abort_command"></a>SRB\_関数の処理\_ABORT\_コマンド


## <span id="ddk_handling_srb_function_abort_command_kg"></span><span id="DDK_HANDLING_SRB_FUNCTION_ABORT_COMMAND_KG"></span>


また、 *HwScsiStartIo*ルーチンは、**関数**メンバーが SRB\_FUNCTION\_ABORT\_コマンドに設定された受信 SRBs を処理します。

中止要求の場合、ミニポートドライバーの*HwScsiStartIo*ルーチンは、ターゲット論理単位の**ScsiPortGetSrb**を呼び出し、返されたポインターを現在の SRB の**と比較することによって、指定された SRB が既に中止されていないことを確認する必要があります。NextSrb**値。 これらが等しくない場合、現在の SRB は既に中止されており、ミニポートドライバーの*HwScsiStartIo*ルーチンは次の処理を実行する必要があります。

1.  入力 SRB の**Srbstatus**を SRB\_STATUS\_ABORT\_FAILED に設定します。

2.  _NotificationType_**requestcomplete**と入力 SRB を使用して[**ScsiPortNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportnotification)を呼び出します。

3.  _NotificationType_**nextrequest**を使用するか、HBA がタグ付きキューまたは複数の要求を論理ユニットごとにサポートする場合は、 **nextlurequest**で**ScsiPortNotification**を再度呼び出します。

それ以外の場合、 *HwScsiStartIo*ルーチンは次の操作を実行します。

1.  デバイス、論理ユニット、および SRB 拡張機能で要求のコンテキストを設定します。

2.  指定された**NextSrb**要求を中止するように HBA をプログラムします。

 

 




