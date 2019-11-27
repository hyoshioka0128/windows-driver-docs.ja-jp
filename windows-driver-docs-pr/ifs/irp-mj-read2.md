---
title: IRP_MJ_READ 操作の Oplock 状態を確認しています
description: IRP_MJ_READ 操作の Oplock 状態を確認しています
ms.assetid: 9b4d1ba9-0838-44f1-8328-f60bfb3910ee
ms.date: 11/25/2019
ms.localizationpriority: medium
ms.openlocfilehash: de28ee85404764aa586b12a2e80b8b14d65990e7
ms.sourcegitcommit: 79ff84ffc2faa5fdb3294e1fb5791f6a0ea7ef50
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74543045"
---
# <a name="checking-the-oplock-state-of-an-irp_mj_read-operation"></a>IRP_MJ_READ 操作の Oplock 状態を確認しています

*ストリーム*を読み取るときには、次の[oplock ブレーク](https://docs.microsoft.com/windows-hardware/drivers/ifs/breaking-oplocks)条件が適用されます。 TxF のトランザクションリーダーが読み取りを実行する場合、トランザクションリーダーがライターを除外するため、このチェックは行われません (つまり、oplock を保持するライターはまったく存在できません)。

### <a name="conditions-for-level-2-filter-read-and-read-handle-request-types"></a>レベル2、フィルター、読み取り、および読み取りハンドルの要求の種類の条件

- Oplock が破損していません。

- 確認は必要ありません。操作は直ちに続行されます。

### <a name="conditions-for-level-1-batch-read-write-and-read-write-handle-request-types"></a>レベル1、バッチ、読み取り/書き込み、および読み取り/書き込みハンドルの要求の種類の条件

- Oplock を所有する FILE_OBJECT のキーとは異なる oplock キーを持つ FILE_OBJECT で読み取り操作が発生した場合に IRP_MJ_READ を中断します。 Oplock が解除された場合は、次のようになります。

  - レベル1とバッチ要求がレベル2に分割されます。

  - 読み取り/書き込み要求が読み取りに対して中断します。

  - 読み取り/書き込みハンドル要求が読み取りハンドルに分割されます。

- 操作を続行するには、受信確認を受信する必要があります。
