---
title: SRB_FUNCTION_IO_CONTROL の処理
description: SRB_FUNCTION_IO_CONTROL の処理
ms.assetid: 92d09a49-d8e8-4d97-b334-c42d5b04ee8d
keywords:
- SCSI ミニポートドライバー WDK 記憶域、HwScsiStartIo
- HwScsiStartIo
- SRB_FUNCTION_IO_CONTROL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bcf4211764199d6671ce27fa8f385c7210e74025
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837844"
---
# <a name="handling-srb_function_io_control"></a>IO\_制御\_の SRB\_関数の処理


## <span id="ddk_handling_srb_function_io_control_kg"></span><span id="DDK_HANDLING_SRB_FUNCTION_IO_CONTROL_KG"></span>


ミニポートドライバーが SRB\_機能を処理するかどうか\_IO\_制御要求は、HBA がユーザーモードアプリケーションの専用サポートを提供するかどうかによって異なります。 この要求をサポートすることで、ドライバーによって定義された ("プライベート") i/o 制御要求のセットをミニポートドライバーに直接送信できるようになります。 **関数**メンバーが SRB\_関数\_IO\_コントロールに設定されている場合、 **DataBuffer**メンバーには、ドライバー定義のとを含むシステム定義の SRB\_IO\_制御構造へのポインターが含まれます。アプリケーションによって指定された**コントロールコード**。

NT ベースのオペレーティングシステムストレージクラスに送信されるすべてのシステム定義の必須デバイス i/o 制御要求は、SRB\_関数ではなく\_SCSI\_実行されるように、**関数**メンバーが SRB\_関数に設定された SRBs にマップされます。IO\_制御を\_します。

##  <a name="-see--also"></a>-参照

[SRB_FUNCTION_EXECUTE_SCSI の処理](https://docs.microsoft.com/windows-hardware/drivers/storage/handling-srb-function-execute-scsi)

[SRB_IO_CONTROL](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddscsi/ns-ntddscsi-_srb_io_control)

 




