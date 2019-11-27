---
title: IRP_MJ_LOCK_CONTROL 操作の Oplock 状態を確認しています
description: IRP_MJ_LOCK_CONTROL 操作の Oplock 状態を確認しています
ms.assetid: 6e0a5287-9a22-465f-b345-c9af556e6cdb
ms.date: 11/25/2019
ms.localizationpriority: medium
ms.openlocfilehash: 425dd95dd2e1635a88431a98723216c7d8411a84
ms.sourcegitcommit: 79ff84ffc2faa5fdb3294e1fb5791f6a0ea7ef50
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74543040"
---
# <a name="checking-the-oplock-state-of-an-irp_mj_lock_control-operation"></a>IRP_MJ_LOCK_CONTROL 操作の Oplock 状態を確認しています

次の[oplock ブレーク](https://docs.microsoft.com/windows-hardware/drivers/ifs/breaking-oplocks)条件は、指定されたストリームのすべてのバイト範囲ロック操作に適用されます。

### <a name="conditions-for-a-level-2-request-type"></a>レベル2の要求の種類の条件

- 常に [なし] になります。

- 確認は必要ありません。操作は直ちに続行されます。

### <a name="conditions-for-a-filter-request-type"></a>フィルター要求の種類の条件

- Oplock が破損していません。

- 確認は必要ありません。操作は直ちに続行されます。

### <a name="conditions-for-level-1-batch-read-read-handle-read-write-and-read-write-handle-request-types"></a>レベル1、バッチ、読み取り、読み取りハンドル、読み取り/書き込み、および読み取り/書き込みの各要求の種類の条件

- Oplock を所有する FILE_OBJECT のキーとは異なる oplock キーを持つ FILE_OBJECT でロック操作が発生したときに、IRP_MJ_LOCK_CONTROL を中断します。 Oplock が解除されている場合は、None に中断します。

- 確認の要件は次のとおりです。

  - 読み取り要求: 確認は必要ありません。操作は直ちに続行されます。

  - 読み取りハンドルと読み取り/書き込みハンドルの要求: 中断の確認が必要ですが、操作はすぐに続行されます (たとえば、受信確認を待たずに)。

  - レベル1、バッチ、および読み取り/書き込み要求: 操作を続行する前に、受信確認を受信する必要があります。
