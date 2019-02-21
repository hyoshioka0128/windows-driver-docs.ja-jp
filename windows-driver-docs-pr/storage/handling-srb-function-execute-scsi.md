---
title: SRB_FUNCTION_EXECUTE_SCSI の処理
description: SRB_FUNCTION_EXECUTE_SCSI の処理
ms.assetid: 221e1070-12d8-4870-a23c-426ed4a25b84
keywords:
- SCSI ミニポート ドライバー WDK ストレージ、HwScsiStartIo
- HwScsiStartIo
- SRB_FUNCTION_EXECUTE_SCSI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 87da85d7f9a496f29d86c7ef2b34ba25f06f276e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529054"
---
# <a name="handling-srbfunctionexecutescsi"></a>処理 SRB\_関数\_EXECUTE\_SCSI


## <span id="ddk_handling_srb_function_execute_scsi_kg"></span><span id="DDK_HANDLING_SRB_FUNCTION_EXECUTE_SCSI_KG"></span>


高度な記憶域クラス ドライバーが読み込まれた後、される Srb のほとんどに送信、 [ **HwScsiStartIo** ](https://msdn.microsoft.com/library/windows/hardware/ff557323)ルーチンが、**関数**メンバー設定される SRB\_関数\_EXECUTE\_SCSI です。

SRB の受信時に\_関数\_EXECUTE\_SCSI 要求、ミニポート ドライバーの*HwScsiStartIo*ルーチンは次の処理します。

-   取得や、そのデバイス、論理ユニット、および SRB の拡張機能でミニポート ドライバーは、どのようなコンテキストを設定

    SRB 自体と、SRB へのポインターを論理ユニットの拡張機能がありますミニポート ドライバーを設定など**DataBuffer**ポインターの場合、SRB **DataTransferLength**値とドライバーの定義済みの値 (または CDBSCSIOP\_*XXX*値)、HBA に実行する操作を示します。

-   部分的に指示として、HBA をプログラムする内部のルーチンを呼び出す、 **SrbFlags**、要求された操作に対して

    デバイス I/O 操作は、内部ルーチンは一般にターゲット デバイスを選択し、ターゲット論理ユニットに、バス経由で CDB を送信します。

呼び出す必要がありますが、ミニポート ドライバーでは、システム DMA を使用する場合[ **ScsiPortIoMapTransfer**](https://msdn.microsoft.com/library/windows/hardware/ff564649)*する前に*データを転送する HBA をプログラミングします。 **ScsiPortIoMapTransfer**システム DMA コント ローラーを設定し、ミニポート ドライバーの*HwScsiDmaStarted*ルーチンを後で説明されている[SCSI ミニポート ドライバーの HwScsiDmaStarted ルーチン](scsi-miniport-driver-s-hwscsidmastarted-routine.md).

NT ベースのオペレーティング システムの記憶域クラス ドライバーに送信されたすべてのシステム定義、必要なデバイス I/O 制御要求が使用される Srb にマップされて、**関数**メンバー設定される SRB\_関数\_EXECUTE\_SCSI です。

 

 




