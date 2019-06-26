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
ms.openlocfilehash: 89f24b23755ee8bdc3e2f94543ae10f35de6d008
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361808"
---
# <a name="bug-check-0x6-invalidprocessdetachattempt"></a>バグ チェック 0x6:無効な\_プロセス\_デタッチ\_試行


無効な\_プロセス\_デタッチ\_試行のバグ チェックが 0x00000006 の値を持ちます。

このバグ チェックが非常に少ない回数が表示されます。 このバグ チェックを呼び出すことによって発生すること、 [**KeStackAttachProcess** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-kestackattachprocess)ルーチンとその後[ **KeUnstackDetachProcess** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-keunstackdetachprocess)のドライバーの実装では、 [ **PLOAD_IMAGE_NOTIFY_ROUTINE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nc-ntddk-pload_image_notify_routine)コールバック関数。 イメージが読み込まれるプロセスのスレッドでコールバックが実行されます。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)します。


 

 




