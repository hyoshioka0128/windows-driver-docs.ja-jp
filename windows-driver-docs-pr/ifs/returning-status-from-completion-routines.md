---
title: 完了ルーチンから返される状態
description: 完了ルーチンから返される状態
ms.assetid: fb12720b-10fe-43ab-ade7-c1b09d00d922
keywords:
- IRP の完了ルーチン WDK ファイル システム、状態を返す
- 状態値 WDK ファイル システム
- 成功状態の値の WDK ファイル システム
- WDK のファイル システムの状態を返す
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9716f55e9f35c1a51adc3549aa210095583c8f30
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344545"
---
# <a name="returning-status-from-completion-routines"></a>完了ルーチンから返される状態


## <span id="ddk_returning_status_from_completion_routines_if"></span><span id="DDK_RETURNING_STATUS_FROM_COMPLETION_ROUTINES_IF"></span>


ファイル システム フィルター ドライバー完了ルーチンでは、呼び出し元に次の 2 つの NTSTATUS 値のいずれかの通常返します。

-   ステータス\_成功

-   ステータス\_詳細\_処理\_必要な作業

ステータス\_成功は、ドライバーは IRP が終了し、完了 IRP の処理を続行する I/O マネージャーを使用することを示します。

ステータス\_詳細\_処理\_REQUIRED が I/O マネージャーの完了の IRP の処理を停止します。

その他の NTSTATUS 値が返された場合 I/O マネージャーにリセット状態\_成功します。

状態の取得の詳細については\_詳細\_処理\_必要に応じてを参照してください[完了ルーチンの制約](constraints-on-completion-routines.md)します。

 

 




