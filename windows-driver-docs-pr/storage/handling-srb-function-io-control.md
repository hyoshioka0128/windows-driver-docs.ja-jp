---
title: SRB_FUNCTION_IO_CONTROL の処理
description: SRB_FUNCTION_IO_CONTROL の処理
ms.assetid: 92d09a49-d8e8-4d97-b334-c42d5b04ee8d
keywords:
- SCSI ミニポート ドライバー WDK ストレージ、HwScsiStartIo
- HwScsiStartIo
- SRB_FUNCTION_IO_CONTROL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a1eaf4fbc5bdc9013cc6b0fdc739e01d009976d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325973"
---
# <a name="handling-srbfunctioniocontrol"></a>処理 SRB\_関数\_IO\_コントロール


## <span id="ddk_handling_srb_function_io_control_kg"></span><span id="DDK_HANDLING_SRB_FUNCTION_IO_CONTROL_KG"></span>


ミニポート ドライバーが SRB を処理するかどうか\_関数\_IO\_コントロール要求、HBA がユーザー モード アプリケーションの専用サポートを提供するかどうかに依存します。 この要求をサポートするいると、一連のミニポート ドライバーに直接送信する ("private") I/O 制御の要求をドライバー定義できます。 使用される Srb の**関数**メンバー SRB に設定\_関数\_IO\_コントロール、 **DataBuffer**メンバーには、システム定義の SRBへのポインターが含まれています\_。IO\_ドライバー定義されており、アプリケーションで指定されたを含む制御構造**ControlCode**します。

NT ベースのオペレーティング システムの記憶域クラス ドライバーに送信されたすべてのシステム定義、必要なデバイス I/O 制御要求が使用される Srb にマップされて、**関数**メンバー設定される SRB\_関数\_EXECUTE\_SRB が、SCSI\_関数\_IO\_コントロール。

##  <a name="-see--also"></a>-- も参照

[SRB_FUNCTION_EXECUTE_SCSI の処理](https://docs.microsoft.com/windows-hardware/drivers/storage/handling-srb-function-execute-scsi)

[SRB_IO_CONTROL](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddscsi/ns-ntddscsi-_srb_io_control)

 




