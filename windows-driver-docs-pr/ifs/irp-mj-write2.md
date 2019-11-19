---
title: IRP_MJ_WRITE 操作の Oplock 状態を確認しています
description: IRP_MJ_WRITE 操作の Oplock 状態を確認しています
ms.assetid: 04d09810-f157-4140-8bfb-c780a65cdf77
ms.date: 11/12/2019
ms.localizationpriority: medium
ms.openlocfilehash: 636a394cdc3cfb216efba43bbcf6f30795bd26db
ms.sourcegitcommit: dac02b6af84c75e31038dae3fccc25f026a97758
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/19/2019
ms.locfileid: "74166140"
---
# <a name="checking-the-oplock-state-of-an-irp_mj_write-operation"></a>IRP_MJ_WRITE 操作の Oplock 状態を確認しています

次の条件は、*ストリーム*が書き込まれていて、書き込みがページング i/o ではない場合にのみ適用されます。

- **レベル 2**の oplock の種類では、常に [なし] になります。 確認は必要ありません。操作は直ちに続行されます。

- その他のすべての oplock の種類は、oplock を所有する FILE_OBJECT とは異なる oplock キーを持つ FILE_OBJECT で書き込み操作が行われた場合にのみ、IRP_MJ_WRITE で破損します。 Oplock が解除されている場合は、None に中断します。 確認の要件は次のとおりです。

  - **Read** oplock: 確認は必要ありません。操作は直ちに続行されます。
  
  - **読み取りハンドル**oplock: 中断の確認が必要ですが、操作はすぐに続行されます (たとえば、受信確認を待たずに)。
  
  - **レベル 1**、**バッチ**、**フィルター**、**読み取り/書き込み**、および**読み取り/書き込みハンドル**の Oplock: 操作を続行する前に受信確認を受け取る必要があります。
