---
title: バグチェック 0x1000007F UNEXPECTED_KERNEL_MODE_TRAP_M
description: UNEXPECTED_KERNEL_MODE_TRAP_M のバグチェックの値は0x1000007F です。
ms.assetid: 913355b6-f569-4535-a6cc-bdc6071b76ff
keywords:
- バグチェック 0x1000007F UNEXPECTED_KERNEL_MODE_TRAP_M
- UNEXPECTED_KERNEL_MODE_TRAP_M
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- UNEXPECTED_KERNEL_MODE_TRAP_M
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c75bdada60651106650097264d8db72974cc3abc
ms.sourcegitcommit: 8e8aa927cf4ab56d0af652fa5e988a8ed6967904
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72916233"
---
# <a name="bug-check-0x1000007f-unexpected_kernel_mode_trap_m"></a>バグチェック 0x1000007F: 予期しない\_カーネル\_モード\_トラップ\_M


予期しない\_カーネル\_モード\_トラップ\_M バグチェックの値が0x1000007F になっています。 これは、トラップが Intel CPU によって生成され、カーネルがこのトラップをキャッチできなかったことを示します。

バグチェックには、0x1000007F と同じ意味とパラメーターがあり、[**バグチェック 0x7f**](bug-check-0x7f--unexpected-kernel-mode-trap.md) (予期しない\_カーネル\_モード\_トラップ) と同じです。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。

## <a name="resolution"></a>解像度
! [デバッグ拡張機能の[**分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)] には、バグチェックに関する情報が表示され、根本原因を特定するのに役立ちます。

 




