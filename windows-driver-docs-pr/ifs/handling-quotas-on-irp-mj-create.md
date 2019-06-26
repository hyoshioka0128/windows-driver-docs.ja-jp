---
title: IRP_MJ_CREATE でのクォータの処理
description: IRP_MJ_CREATE でのクォータの処理
ms.assetid: 71cf5e78-c87a-48fe-ba0b-f5efe8166525
keywords:
- IRP_MJ_CREATE
- WDK のクォータはファイル システム
- セキュリティは、WDK のファイル システム、irp_mj_create 用を確認します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b41944cf14b9becec9f13b9308d1ff2357f66cc4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365874"
---
# <a name="handling-quotas-on-irpmjcreate"></a>IRP のクォータを処理\_MJ\_を作成します。


## <span id="ddk_handling_quotas_on_irp_mj_create_if"></span><span id="DDK_HANDLING_QUOTAS_ON_IRP_MJ_CREATE_IF"></span>


いくつかのロジックは、ファイル システム クォータをサポートしている場合は、クォータの情報を取得する可能性がありますも含まれます。 ファイル システムを採用している 1 つの戦略に関するクォータ情報のブロックを取得すること[ **IRP\_MJ\_作成**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-create)を後でチェックありのディスパッチ ルーチンによって更新ファイルのサイズを変更できる他の IRP 要求 (削除および書き込み操作など)。

 

 




