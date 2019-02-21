---
title: 上位トランザクション マネージャーの作成
description: 上位トランザクション マネージャーの作成
ms.assetid: 6f6bf61a-fe53-47b5-9559-f76334969af8
keywords:
- トランザクション マネージャー WDK KTM
- 優先的なトランザクション マネージャー WDK KTM
- WDK KTM、優れた参加リストの登録
- 参加リストが優れた WDK KTM
- WDK KTM、下位の参加リストの登録
- 下位の参加リスト WDK KTM
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 25f9ba7163ef8816fc8cdbb1e83be7b741ed0cdf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557600"
---
# <a name="creating-a-superior-transaction-manager"></a>上位トランザクション マネージャーの作成


KTM で、*優先的なトランザクション マネージャー*リソース マネージャーに含まれているトランザクションの優れた参加リストを作成します。 A*上位登録*リソース マネージャーに調整する権限が付与された参加リストは、[コミット操作](handling-commit-operations.md)登録リストのトランザクションの。 つまり、トランザクションのクライアントまたは上位のトランザクション マネージャーは、トランザクションの前-prepare/準備/コミットのシーケンスを開始できます。

KTM はすべての呼び出しを拒否するリソース マネージャーがトランザクションの上位の登録を作成、 [ **ZwCommitTransaction** ](https://msdn.microsoft.com/library/windows/hardware/ff566420)トランザクションにします。 そのため、トランザクションのクライアントは、このようなトランザクションをコミットすることはできません。 代わりに、上位の登録を作成したリソース マネージャーを呼び出す必要があります[ **ZwPrePrepareEnlistment**](https://msdn.microsoft.com/library/windows/hardware/ff567044)、 [ **ZwPrepareEnlistment** ](https://msdn.microsoft.com/library/windows/hardware/ff567039)、および[ **ZwCommitEnlistment**](https://msdn.microsoft.com/library/windows/hardware/ff566419)します。

### <a name="when-to-create-a-superior-transaction-manager"></a>上位のトランザクション マネージャーを作成する場合

処理 (TP) のシステム コンポーネント、ktm トランザクションを統合するとしますが、コンポーネントには、クライアントが呼び出すことができます独自の非 KTM トランザクション管理機能が含まれています。 このような状況では、優先的なトランザクション マネージャーを作成する必要があります。

たとえば、コンポーネントがクライアントを作成し、トランザクションのコミットに使用する独自のインターフェイスを提供します。 コンポーネントのクライアントは、トランザクションのコミットを作成または KTM を呼び出さないでください、ために、コンポーネントでは、KTM ベース TP に統合する際に優れたトランザクション マネージャーになります。

### <a name="how-to-create-a-superior-transaction-manager"></a>上位のトランザクション マネージャーを作成する方法

コンポーネントに優れたトランザクション マネージャーになる場合は、以下を行うこと必要があります。

1.  呼び出す[ **ZwCreateResourceManager** ](https://msdn.microsoft.com/library/windows/hardware/ff566427)リソース マネージャーとして登録します。

2.  呼び出す[ **ZwCreateTransaction** ](https://msdn.microsoft.com/library/windows/hardware/ff566429)たびに、クライアントのコンポーネントがコンポーネントのクライアント インターフェイスを使用してトランザクションを作成します。

3.  呼び出す[ **ZwCreateEnlistment**](https://msdn.microsoft.com/library/windows/hardware/ff566422)、参加リストを設定\_優れたフラグ、および参加リストの両方を指定して\_優れた\_権限との参加\_下位\_権限フラグにアクセスします。

4.  呼び出す[ **ZwPrePrepareEnlistment**](https://msdn.microsoft.com/library/windows/hardware/ff567044)、 [ **ZwPrepareEnlistment**](https://msdn.microsoft.com/library/windows/hardware/ff567039)、および[ **ZwCommitEnlistment** ](https://msdn.microsoft.com/library/windows/hardware/ff566419)コンポーネントのクライアントがトランザクションをコミットするコンポーネントのクライアント インターフェイスを呼び出すとします。

KTM では、トランザクションあたり 1 つだけ上位の登録を許可します。 他のリソース マネージャーは、追加の参加リストを作成できます。 これらの参加リストが呼び出される*下位の参加リスト*コミット操作を開始することはできませんので。

上位の登録を優先的なトランザクション マネージャーの呼び出しをロールバックする[ **ZwRollbackEnlistment**](https://msdn.microsoft.com/library/windows/hardware/ff567083)します。

上位の登録を優先的なトランザクション マネージャーの呼び出しを回復する[ **ZwRecoverEnlistment**](https://msdn.microsoft.com/library/windows/hardware/ff567075)します。

優先的なトランザクション マネージャーがコミットまたはロールバック、トランザクションの復旧、KTM を送信[トランザクション通知](transaction-notifications.md)すべてに参加リストが下位に参加できるようにします。

優先的なトランザクション マネージャーを含む TP は使用できません[単一フェーズ コミット操作](handling-commit-operations.md#single-phase-commit-operations)します。

回復操作中に KTM をトランザクションの結果を判断できない場合、送信トランザクション\_通知\_回復\_優れたトランザクション マネージャーに通知をクエリします。 応答として、上位のトランザクション マネージャーを呼び出す必要があります**ZwCommitEnlistment**トランザクションをコミットすることができる場合または**ZwRollbackEnlistment**場合は、トランザクションをロールバックする必要があります。 トランザクションに応答する必要がありますしない場合は、トランザクションの結果を判断できないのは、上位のトランザクション マネージャー、\_通知\_回復\_まで結果を実現することを確認し、クエリ通知します。

 

 




