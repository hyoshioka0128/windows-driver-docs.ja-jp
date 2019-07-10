---
title: SRB_FUNCTION_ABORT_COMMAND の処理
description: SRB_FUNCTION_ABORT_COMMAND の処理
ms.assetid: 74d46df6-2e3e-45d8-bedb-a81a80a0aec1
keywords:
- SCSI ミニポート ドライバー WDK ストレージ、HwScsiStartIo
- HwScsiStartIo
- SRB_FUNCTION_ABORT_COMMAND
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 61d4d49db615e763ddba21653fe9612e6aebeea3
ms.sourcegitcommit: fee68bc5f92292281ecf1ee88155de45dfd841f5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/10/2019
ms.locfileid: "67716938"
---
# <a name="handling-srbfunctionabortcommand"></a>処理 SRB\_関数\_中止\_コマンド


## <span id="ddk_handling_srb_function_abort_command_kg"></span><span id="DDK_HANDLING_SRB_FUNCTION_ABORT_COMMAND_KG"></span>


*HwScsiStartIo*ルーチンはで受信される Srb を処理することも、**関数**メンバー SRB に設定\_関数\_中止\_コマンド。

中止要求に対して、ミニポート ドライバーの*HwScsiStartIo*ルーチンでは、特定の SRB されませんが中止されたこと既に呼び出すことによって確認してください**ScsiPortGetSrb**ターゲット論理ユニットと比較すること、現在 SRB へのポインターが返されます**NextSrb**値。 等しくない場合、現在 SRB 既に中止されていますが、および、ミニポート ドライバーの*HwScsiStartIo*ルーチンは、次を行う必要があります。

1.  セットの入力 SRB の**SrbStatus** SRB に\_状態\_中止\_できませんでした。

2.  呼び出す[ **ScsiPortNotification** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportnotification)で、 _NotificationType_**RequestComplete** SRB の入力を使用しています。

3.  呼び出す**ScsiPortNotification**を使用して、 _NotificationType_**NextRequest**、または**NextLuRequest** HBA がサポートしている場合タグ付けされたキューまたは論理ユニットごとの複数の要求。

それ以外の場合、 *HwScsiStartIo*ルーチンは、次を実行します。

1.  そのデバイス、論理ユニット、および SRB の拡張機能での要求のコンテキストを設定します。

2.  プログラムを中止する HBA、指定された**NextSrb**要求。

 

 




