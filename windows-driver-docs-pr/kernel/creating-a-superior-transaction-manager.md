---
title: 上位トランザクション マネージャーの作成
description: 上位トランザクション マネージャーの作成
ms.assetid: 6f6bf61a-fe53-47b5-9559-f76334969af8
keywords:
- トランザクションマネージャーの WDK KTM
- 上位のトランザクションマネージャー WDK KTM
- WDK KTM の参加、上位の参加
- 上位の参加リスト WDK KTM
- '[WDK KTM]、[下位参加リスト]'
- 下位参加リスト WDK KTM
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 57890e9547e2ff6c5a7654b9784c97524f7409dc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837015"
---
# <a name="creating-a-superior-transaction-manager"></a>上位トランザクション マネージャーの作成


KTM では、*上位トランザクションマネージャー*は、参加しているトランザクションの上位の参加リストを作成するリソースマネージャーです。 *上位の参加*リストは、リソースマネージャーに対して、参加リストのトランザクションの[コミット操作](handling-commit-operations.md)を調整する機能を与える参加リストです。 言い換えると、トランザクションクライアントまたは上位トランザクションマネージャーは、トランザクションの準備前/準備/コミットシーケンスを開始できます。

リソースマネージャーがトランザクションの上位の参加リストを作成した後、KTM はトランザクションの[**Zwcommittransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommittransaction)へのすべての呼び出しを拒否します。 したがって、トランザクションクライアントはこのようなトランザクションをコミットできません。 代わりに、上位の参加リストを作成したリソースマネージャーは、 [**Zwpreの参加リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntpreprepareenlistment)、 [**zw/** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntprepareenlistment)参加リスト、および[**zwcommit参加**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommitenlistment)リストを呼び出す必要があります。

### <a name="when-to-create-a-superior-transaction-manager"></a>上位トランザクションマネージャーを作成する場合

トランザクション処理システム (TPS) コンポーネントを KTM に統合するが、コンポーネントには、クライアントが呼び出すことができる独自の非 KTM トランザクション管理機能が含まれているとします。 このような状況では、より優れたトランザクションマネージャーの作成が必要になる場合があります。

たとえば、クライアントがトランザクションを作成およびコミットするために使用する独自のインターフェイスがコンポーネントに用意されているとします。 コンポーネントのクライアントは、トランザクションを作成またはコミットするために KTM を呼び出しません。そのため、コンポーネントは、KTM ベースの TP に統合するときに、上位のトランザクションマネージャーになる必要があります。

### <a name="how-to-create-a-superior-transaction-manager"></a>上位トランザクションマネージャーを作成する方法

コンポーネントが上位トランザクションマネージャーになるようにするには、次の操作を行う必要があります。

1.  [**Zwcreateresourcemanager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreateresourcemanager)を呼び出して、リソースマネージャーとして登録します。

2.  コンポーネントのクライアントがコンポーネントのクライアントインターフェイスを使用してトランザクションを作成するたびに、 [**Zwcreatetransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreatetransaction)を呼び出します。

3.  [**Zwcreateenlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreateenlistment)リストを呼び出し、参加リスト\_上位フラグを設定し、サブ登録\_上位の\_権限と参加リスト\_下位\_権限のアクセスフラグを指定します。

4.  コンポーネントのクライアントがコンポーネントのクライアントインターフェイスを呼び出してトランザクションをコミットするときに、 [**Zwpreの参加リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntpreprepareenlistment)、 [**zwの**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntprepareenlistment)参加リスト、および[**zwcommit参加**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommitenlistment)リストを呼び出します。

KTM では、トランザクションごとに1つの上位参加リストのみを許可します。 他のリソースマネージャーは、追加の参加を作成できます。 これらの参加リストは、コミット操作を開始できないため、*下位参加リスト*と呼ばれます。

優れた参加リストをロールバックするために、上位トランザクションマネージャーは[**ZwRollbackEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrollbackenlistment)を呼び出します。

優れた参加リストを復旧するために、上位トランザクションマネージャーは[**Zw回復参加リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrecoverenlistment)を呼び出します。

上位トランザクションマネージャーがトランザクションをコミット、ロールバック、または復旧すると、KTM はトランザクション[通知](transaction-notifications.md)をすべての下位参加要素に送信して参加できるようにします。

上位トランザクションマネージャーを含む TPS は、[単一フェーズコミット操作](handling-commit-operations.md#single-phase-commit-operations)を使用できません。

復旧操作中に、KTM がトランザクションの結果を判断できない場合は、トランザクションを送信して、上位トランザクションマネージャーに\_クエリ通知を回復\_\_通知します。 応答として、トランザクションをコミットできる**場合は**、またはトランザクションをロールバックする必要がある場合は、 **ZwRollbackEnlistment**を呼び出す必要があります。 上位トランザクションマネージャーがトランザクションの結果を判断できない場合は、トランザクションに応答せずに、結果を特定できるまで\_クエリ通知\_復旧するように\_通知する必要があります。

 

 




