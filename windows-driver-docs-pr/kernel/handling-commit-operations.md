---
title: コミット操作の処理
description: コミット操作の処理
ms.assetid: 4885476e-ce68-4674-b8a5-8a317f33cd5b
keywords:
- WDK KTM をトランザクションのコミット トランザクション
- WDK KTM をトランザクションのコミット
- リソース マネージャー WDK KTM をトランザクションのコミット
- 単一フェーズ コミット WDK KTM、複数フェーズのコミット WDK KTM
- 事前準備フェーズ WDK KTM
- 準備フェーズ WDK KTM
- コミット フェーズ WDK KTM
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: da1a107f0ca554dfd91937148a39bdc68c20c0a6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580126"
---
# <a name="handling-commit-operations"></a>コミット操作の処理


コミット操作の 2 種類があります:*単一フェーズ コミット*と*複数フェーズのコミット*します。 単一フェーズ コミット操作は、リソース マネージャーは、複数フェーズのコミット操作には、準備手順について追加の通知が含まれていますが、対応する必要が 1 つの通知で構成されます。

単一フェーズ コミット操作が簡単に実装します。 トランザクション処理 (TPSs)、次の特性の 1 つを持つシステムに適しています。

-   1 つのリソース マネージャー。

-   その 1 つを除くすべての複数のリソース マネージャー[読み取り専用](creating-a-resource-manager.md#kernel-creating-a-read-only-enlistment)コミット操作に参加していないとします。

複数フェーズのコミット操作は、コミット操作で複数のリソース マネージャーが参加する場合は、必要があります。

### <a name="single-phase-commit-operations"></a>単一フェーズ コミット操作

トランザクションを受信する 1 つ (および 1 つだけ) のリソース マネージャーを登録する必要があります、TP 単一フェーズ コミット操作をサポートする場合は、\_通知\_単一\_フェーズ\_コミット[通知](transaction-notifications.md)その参加します。 その他のすべてのリソース マネージャーである必要があります[読み取り専用](creating-a-resource-manager.md#kernel-creating-a-read-only-enlistment)します。

含む TP を[優先的なトランザクション マネージャー](creating-a-superior-transaction-manager.md)単一フェーズ コミットを使用することはできません。

リソース マネージャーがトランザクションを受信する登録されている場合\_通知\_単一\_フェーズ\_コミットの通知、KTM 送信この種の通知トランザクション クライアントが呼び出す[ **ZwCommitTransaction**](https://msdn.microsoft.com/library/windows/hardware/ff566420)します。

リソース マネージャーがトランザクションを受信すると\_通知\_単一\_フェーズ\_コミット通知トランザクションでそのトランザクションをコミットするか単一フェーズ コミットを拒否します。

トランザクションをコミットするには、リソース マネージャーは、次の操作を行う必要があります。

1.  などの非永続的なキャッシュ (メモリ内ストレージ) に保持しているすべてのデータのフラッシュ、[領域をマーシャ リング CLFS](clfs-marshalling-areas.md)の[CLFS ログ ストリーム](using-log-streams-with-ktm.md)します。

    リソース マネージャーは、永続的なストレージ メディアに、キャッシュからデータを移動する必要があります。 たとえば、CLFS を使用しているリソース マネージャーを呼び出すことができます[ **ClfsFlushBuffers**](https://msdn.microsoft.com/library/windows/hardware/ff541544)します。

2.  永続的であり、パブリックにすべてのデータ変更を行う (つまり、リソース マネージャーのスコープ外部から参照できる)。

3.  呼び出す[ **ZwCommitComplete**](https://msdn.microsoft.com/library/windows/hardware/ff566418)します。

呼び出した後**ZwCommitComplete**、resource manager を呼び出す必要があります[ **ZwClose** ](https://msdn.microsoft.com/library/windows/hardware/ff566417)登録ハンドルを閉じます。

トランザクションの単一フェーズ コミット操作を拒否するには、resource manager を呼び出すことができます[ **ZwSinglePhaseReject**](https://msdn.microsoft.com/library/windows/hardware/ff567113)します。 リソース マネージャーを呼び出す場合**ZwSinglePhaseReject**KTM をすぐに変更のコミット操作単一フェーズからマルチ フェーズ。

場合、他のリソース マネージャーは、同じトランザクションに参加する必要がある[読み取り専用](creating-a-resource-manager.md#kernel-creating-a-read-only-enlistment)します。 ただし、トランザクションの受信登録が必要な\_通知\_RM\_切断されている通知は、単一フェーズ コミット操作を処理しているリソース マネージャーは、参加を終了した場合に受信しました。示すことがコミットされたトランザクションをロールバックせずに処理します。

### <a name="multi-phase-commit-operations"></a>複数フェーズのコミット操作

複数フェーズのコミット操作では、次のイベントのいずれかが発生したときを始めます。

-   トランザクションのクライアントが呼び出す[ **ZwCommitTransaction**](https://msdn.microsoft.com/library/windows/hardware/ff566420)、トランザクションを受信するリソース マネージャーが登録されていない\_通知\_単一\_フェーズ\_コミット通知します。

-   リソース マネージャーは、 [ **ZwSinglePhaseReject** ](https://msdn.microsoft.com/library/windows/hardware/ff567113)トランザクションを受け取った後\_通知\_単一\_フェーズ\_コミット通知します。

-   A[優先的なトランザクション マネージャー](creating-a-superior-transaction-manager.md)呼び出し[ **ZwPrePrepareEnlistment**](https://msdn.microsoft.com/library/windows/hardware/ff567044)します。

複数フェーズのコミット操作は、3 つの連続したフェーズで構成されています:*事前準備*、*準備*、および*コミット*します。

**事前準備フェーズ**

Pre-prepare フェーズ (とも呼ばれます*フェーズ 0*) KTM トランザクションを送信するときに、コミットの操作を開始\_通知\_PREPREPARE 通知は、すべてのリソース マネージャーをします。 リソース マネージャーが、トランザクションでは、単一フェーズ コミット操作をサポートしない場合、または優先的なトランザクション マネージャーを呼び出す場合、KTM はこの通知を送信[ **ZwPrePrepareEnlistment**](https://msdn.microsoft.com/library/windows/hardware/ff567044)します。

各リソース マネージャーがトランザクションを受信すると\_通知\_PREPREPARE 通知では、次を行う必要があります。

1.  などの非永続的なキャッシュ (メモリ内ストレージ) に保持しているすべてのデータのフラッシュ、[領域をマーシャ リング CLFS](clfs-marshalling-areas.md)の[CLFS ログ ストリーム](using-log-streams-with-ktm.md)します。

    リソース マネージャーは、永続的なストレージ メディアに、キャッシュからデータを移動する必要があります。 たとえば、CLFS を使用しているリソース マネージャーを呼び出すことができます[ **ClfsFlushBuffers**](https://msdn.microsoft.com/library/windows/hardware/ff541544)します。

2.  呼び出す[ **ZwPrePrepareComplete**](https://msdn.microsoft.com/library/windows/hardware/ff567040)します。

リソース後マネージャーが呼び出されて**ZwPreprepareComplete**を受け取り、クライアント要求サービスを続行します。 ただし、リソース マネージャーは、永続的なストレージ メディアにすぐに書き込まれるキャッシュ パススルー操作としてすべてのデータ変更を処理する必要があります。

リソース マネージャーでは、トランザクションを処理している間に、エラーが発生したかどうかは\_通知\_呼び出す必要があります、PREPREPARE 通知[ **ZwRollbackEnlistment** ](https://msdn.microsoft.com/library/windows/hardware/ff567083)をロールバックするにはトランザクションです。

**準備フェーズ**

準備フェーズ (とも呼ばれます*フェーズ 1*) KTM トランザクションを送信するときに、コミットの操作を開始\_通知\_すべてのリソース マネージャーに通知を準備します。 KTM トランザクション後にこの通知を送信する\_通知\_単一フェーズ コミットまたは優先的なトランザクション マネージャーを呼び出すかどうかのリソース マネージャーをサポートしない場合の PREPREPARE [ **ZwPrepareEnlistment**](https://msdn.microsoft.com/library/windows/hardware/ff567039).

各リソース マネージャーがトランザクションを受信すると\_通知\_PREPARE 通知では、次を行う必要があります。

1.  クライアント要求の処理を停止し、クライアントのエラーとしてクライアントの後続の要求を報告します。

2.  永続的なストレージにすべてのデータが移動されたことを確認します。

3.  呼び出す[ **ZwPrepareComplete**](https://msdn.microsoft.com/library/windows/hardware/ff567037)します。

リソース マネージャーでは、トランザクションを処理している間に、エラーが発生したかどうかは\_通知\_呼び出す必要があります PREPARE 通知[ **ZwRollbackEnlistment** ](https://msdn.microsoft.com/library/windows/hardware/ff567083)をロールバックする、トランザクションです。 ただし、リソース マネージャーできないトランザクションをロールバックして呼び出し後に**ZwPrepareComplete**します。

**コミット フェーズ**

コミット フェーズ (とも呼ばれます*フェーズ 2*) KTM トランザクションを送信するときに、コミットの操作を開始\_通知\_すべてのリソース マネージャーに通知をコミットします。 KTM トランザクション後にこの通知を送信する\_通知\_単一フェーズ コミットまたは優先的なトランザクション マネージャーを呼び出すかどうかのリソース マネージャーをサポートしない場合の準備[ **ZwCommitEnlistment**](https://msdn.microsoft.com/library/windows/hardware/ff566419).

各リソース マネージャーがトランザクションを受信すると\_通知\_コミット通知では、次を行う必要があります。

1.  永続的であり、パブリックにすべてのデータ変更を行う (つまり、その他のトランザクションから確認できる)。

    通常、リソース マネージャー、変更、永続的なパブリック ログ ストリームから、データベースの公開、永続的なストレージにトランザクションの保存されたデータをコピーしています。 ログ ストリームを使用する方法の詳細については、次を参照してください。 [ktm を使用するログ ストリーム](using-log-streams-with-ktm.md)します。

2.  呼び出す[ **ZwCommitComplete**](https://msdn.microsoft.com/library/windows/hardware/ff566418)します。

Resource manager の呼び出し後**ZwCommitComplete**を呼び出す必要が[ **ZwClose** ](https://msdn.microsoft.com/library/windows/hardware/ff566417)登録ハンドルを閉じます。

リソース マネージャーでは、トランザクションを処理している間に、エラーが発生したかどうかは\_通知\_コミット通知では、その必要がありますシャット ダウンします。 オペレーティング システムをリソース マネージャー、リソース マネージャーの再読み込みを次回[回復プロセス](handling-recovery-operations.md)トランザクションをエラーが発生する前に適切なことがわかっている状態に復元する必要があります。

 

 




