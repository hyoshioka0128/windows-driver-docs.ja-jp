---
title: IRP_MJ_CLEANUP 操作の Oplock 状態を確認しています
description: IRP_MJ_CLEANUP 操作の Oplock 状態を確認しています
ms.assetid: 5e078575-cbb8-4460-9986-4c546b8c20be
ms.date: 11/25/2019
ms.localizationpriority: medium
ms.openlocfilehash: 8c6a7b81a4908a90b1c2860e5f02edcb4c63dcd5
ms.sourcegitcommit: 79ff84ffc2faa5fdb3294e1fb5791f6a0ea7ef50
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74543037"
---
# <a name="checking-the-oplock-state-of-an-irp_mj_cleanup-operation"></a>IRP_MJ_CLEANUP 操作の Oplock 状態を確認しています

次の[oplock ブレーク](https://docs.microsoft.com/windows-hardware/drivers/ifs/breaking-oplocks)条件は、*ストリーム*が閉じられている場合にのみ適用されます。

### <a name="conditions-for-level-2-and-read-request-types"></a>レベル2および読み取り要求の種類の条件

- 常に [なし] になります。 同じストリームに対する他のレベル2または読み取り oplock は影響を受けないことに注意してください。この FILE_OBJECT に関連付けられているレベル2または読み取り oplock のみが壊れています。

- 確認は必要ありません。操作は直ちに続行されます。

### <a name="conditions-for-level-1-batch-filter-read-handle-read-write-and-read-write-handle-request-types"></a>レベル1、バッチ、フィルター、読み取りハンドル、読み取り/書き込み、および読み取り/書き込み要求の種類の条件

- 常に [なし] になります。

- 確認は必要ありません。操作は直ちに続行されます。 保留中の中断要求からの受信確認を待機している i/o 操作 (Irp) は、直ちに完了することに注意してください。
