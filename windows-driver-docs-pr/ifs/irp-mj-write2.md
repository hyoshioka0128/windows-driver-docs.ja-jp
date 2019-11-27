---
title: IRP_MJ_WRITE 操作の Oplock 状態を確認しています
description: IRP_MJ_WRITE 操作の Oplock 状態を確認しています
ms.assetid: 04d09810-f157-4140-8bfb-c780a65cdf77
ms.date: 11/25/2019
ms.localizationpriority: medium
ms.openlocfilehash: 82fad40d1b288cc9be243a52fec8928955624f92
ms.sourcegitcommit: 79ff84ffc2faa5fdb3294e1fb5791f6a0ea7ef50
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74543041"
---
# <a name="checking-the-oplock-state-of-an-irp_mj_write-operation"></a>IRP_MJ_WRITE 操作の Oplock 状態を確認しています

*ストリーム*が書き込まれていて、書き込みがページング i/o ではない場合、次の[oplock ブレーク](https://docs.microsoft.com/windows-hardware/drivers/ifs/breaking-oplocks)条件が適用されます。

### <a name="conditions-for-a-level-2-request-type"></a>レベル2の要求の種類の条件:

- 常に [なし] になります。

- 確認は必要ありません。操作は直ちに続行されます。

### <a name="conditions-for-all-other-request-types"></a>他のすべての要求の種類の条件:

- Oplock を所有する FILE_OBJECT のキーとは異なる oplock キーを持つ FILE_OBJECT で書き込み操作が行われたときに、IRP_MJ_WRITE を中断します。 Oplock が解除されている場合は、None に中断します。

- 確認の要件は次のとおりです。

  - 読み取り要求: 確認は必要ありません。操作は直ちに続行されます。
  
  - 読み取りハンドル要求: 中断の確認が必要ですが、操作はすぐに続行されます (たとえば、受信確認を待たずに)。
  
  - レベル1、バッチ、フィルター、読み取り/書き込み、および読み取り/書き込みハンドル要求: 操作を続行する前に受信確認を受信する必要があります。
