---
title: トランザクション操作の処理
description: トランザクション操作の処理
ms.assetid: 9b82e9d6-3db2-4806-a087-1c9622dc04e2
keywords:
- 操作の処理の WDK KTM トランザクション
- 操作の WDK KTM をトランザクション処理
- WDK KTM をトランザクションのコミット トランザクション
- WDK KTM をトランザクションのコミット
- トランザクション WDK KTM をトランザクションのロールバック
- WDK KTM トランザクションをロールバックしています
- トランザクション WDK KTM をトランザクションの回復
- WDK KTM をトランザクションの回復
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd579db79ef67370c75770e86d3277b68bb69477
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559848"
---
# <a name="handling-transaction-operations"></a>トランザクション操作の処理


リソース マネージャーは、3 つのトランザクション操作を処理する必要があります:*コミット*、*ロールバック*、および*recovery*します。

*トランザクションをコミット*、永続的であり、その他のトランザクションから確認できる、リソース マネージャーがトランザクションのデータにすべての変更を加えます。

*トランザクションをロールバックする*、リソース マネージャーがトランザクションのデータに対するすべての変更を削除します。 リソース マネージャーは、トランザクションが作成された前に、の状態にデータを復元する必要があります。

*、トランザクションの復旧*、リソース マネージャー システムがクラッシュまたは別の予期しないイベントの後にトランザクションのデータを正常な状態に復元します。

このセクションには、次のトピックが含まれています。

[コミット操作の処理](handling-commit-operations.md)

[ロールバック操作の処理](handling-rollback-operations.md)

[回復操作の処理](handling-recovery-operations.md)

 

 




