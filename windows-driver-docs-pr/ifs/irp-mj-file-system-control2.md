---
title: IRP_MJ_FILE_SYSTEM_CONTROL の Oplock 状態を確認しています
description: IRP_MJ_FILE_SYSTEM_CONTROL 操作の Oplock 状態を確認しています
ms.assetid: 3651d9ed-6b6f-4b60-9dfa-1c5c0c78b1a1
ms.date: 11/25/2019
ms.localizationpriority: medium
ms.openlocfilehash: 907018a1f5a007611cb66ee977486f372b942135
ms.sourcegitcommit: 79ff84ffc2faa5fdb3294e1fb5791f6a0ea7ef50
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74543043"
---
# <a name="checking-the-oplock-state-of-irp_mj_file_system_control"></a>IRP_MJ_FILE_SYSTEM_CONTROL の Oplock 状態を確認しています

次の IRP_MJ_FILE_SYSTEM_CONTROL 操作の oplock の状態を確認します。

- **FSCTL_SET_ZERO_DATA**

この情報は、呼び出し元が指定されたストリームの現在の内容をゼロにする必要がある場合に適用されます。

### <a name="conditions-for-a-level-2-request-type"></a>レベル2の要求の種類の条件:

- 常に [なし] になります。

- 確認は必要ありません。操作は直ちに続行されます。

### <a name="conditions-for-all-other-request-types"></a>他のすべての要求の種類の条件:

- Oplock を所有する FILE_OBJECT のキーとは異なる oplock キーを持つ FILE_OBJECT で操作が行われた場合に、IRP_MJ_FILE_SYSTEM_CONTROL (FSCTL_SET_ZERO_DATA) で中断します。 Oplock が解除されている場合は、None に中断します。

- 確認の要件は次のとおりです。

  - 読み取り要求: 確認は必要ありません。操作は直ちに続行されます。
  
  - 読み取りハンドル要求: 中断の確認が必要ですが、操作はすぐに続行されます (たとえば、受信確認を待たずに)。
  
  - レベル1、バッチ、フィルター、読み取り/書き込み、および読み取り/書き込みハンドル要求: 操作を続行する前に受信確認を受信する必要があります。
