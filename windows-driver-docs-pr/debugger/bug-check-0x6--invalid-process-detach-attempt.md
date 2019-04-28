---
title: バグ チェック 0x6 INVALID_PROCESS_DETACH_ATTEMPT
description: INVALID_PROCESS_DETACH_ATTEMPT のバグ チェックでは、0x00000006 の値を持ちます。 このバグ チェックが非常に少ない回数が表示されます。
ms.assetid: f468b348-6576-4430-aa8f-b6100a689fee
keywords:
- バグ チェック 0x6 INVALID_PROCESS_DETACH_ATTEMPT
- INVALID_PROCESS_DETACH_ATTEMPT
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- INVALID_PROCESS_DETACH_ATTEMPT
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0d17c01b7ed232768e85e4a67aaa23668761141f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366467"
---
# <a name="bug-check-0x6-invalidprocessdetachattempt"></a>バグ チェック 0x6:無効な\_プロセス\_デタッチ\_試行


無効な\_プロセス\_デタッチ\_試行のバグ チェックが 0x00000006 の値を持ちます。

このバグ チェックが非常に少ない回数が表示されます。 このバグ チェックを呼び出すことによって発生すること、 [**KeStackAttachProcess** ](https://msdn.microsoft.com/library/windows/hardware/ff549659)ルーチンとその後[ **KeUnstackDetachProcess** ](https://msdn.microsoft.com/library/windows/hardware/ff549677)のドライバーの実装では、 [ **PLOAD_IMAGE_NOTIFY_ROUTINE** ](https://msdn.microsoft.com/library/windows/hardware/mt764088(v=vs.85).aspx)コールバック関数。 イメージが読み込まれるプロセスのスレッドでコールバックが実行されます。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


 

 




