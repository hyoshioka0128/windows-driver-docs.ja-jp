---
title: AV/C ストリーミングのプロトコル ドライバー関数コード
description: AV/C ストリーミングのプロトコル ドライバー関数コード
ms.assetid: c76662fc-8bb9-411a-8672-d00a4533e952
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 56185b3b2b2cb69df674caf50bf844e4c008e852
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323520"
---
# <a name="avc-streaming-protocol-driver-function-codes"></a>AV/C ストリーミングのプロトコル ドライバー関数コード


## <span id="ddk_av_c_streaming_protocol_driver_function_codes_ks"></span><span id="DDK_AV_C_STREAMING_PROTOCOL_DRIVER_FUNCTION_CODES_KS"></span>


AV/C ストリーミング フィルター ドライバーは Irp をインターセプト デバイス スタックでします。

通信する*avcstrm.sys*、サブユニット ドライバーが IRP を設定する必要があります**IoControlCode** IOCTL メンバー\_AVCSTRM\_クラス。

I/O 要求を行うには、ヘッダー ファイルをインクルード*avcstrm.h*、これは Microsoft Windows Driver Kit (WDK) に含まれています。

 

 





