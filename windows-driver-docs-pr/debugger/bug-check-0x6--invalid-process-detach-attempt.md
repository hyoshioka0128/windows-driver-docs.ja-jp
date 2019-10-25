---
title: バグチェック 0x6 INVALID_PROCESS_DETACH_ATTEMPT
description: INVALID_PROCESS_DETACH_ATTEMPT のバグチェックの値は0x00000006 です。 このバグチェックは非常に頻繁に行われません。
ms.assetid: f468b348-6576-4430-aa8f-b6100a689fee
keywords:
- バグチェック 0x6 INVALID_PROCESS_DETACH_ATTEMPT
- INVALID_PROCESS_DETACH_ATTEMPT
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- INVALID_PROCESS_DETACH_ATTEMPT
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a2da0ddc9b2d0032f789793602b9e282d608fe5b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827000"
---
# <a name="bug-check-0x6-invalid_process_detach_attempt"></a>バグチェック 0x6: 無効な\_プロセス\_デタッチ\_試行


無効な\_プロセス\_デタッチ\_試行のバグチェックの値は0x00000006 です。

このバグチェックは非常に頻繁に行われません。 このバグチェックは、 [**Kestackattachprocess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-kestackattachprocess)ルーチンを呼び出し、その後、ドライバーの[**PLOAD_IMAGE_NOTIFY_ROUTINE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nc-ntddk-pload_image_notify_routine) callback 関数の実装で[**KeUnstackDetachProcess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-keunstackdetachprocess)を呼び出すことによって発生することがあります。 コールバックは、イメージが読み込まれたプロセスのスレッドで実行されます。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


 

 




