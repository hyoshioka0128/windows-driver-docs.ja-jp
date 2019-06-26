---
title: 回復操作の処理
description: 回復操作の処理
ms.assetid: 35149bb9-fd48-44d3-a9fd-0e631aa0e853
keywords:
- トランザクション WDK KTM をトランザクションの回復
- WDK KTM をトランザクションの回復
- トランザクション処理システム WDK KTM をトランザクションの回復
- TP WDK KTM をトランザクションの回復
- ログ ストリーム WDK KTM をトランザクションの回復
- 仮想のクロック値 WDK KTM をトランザクションの回復
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7cb9cacbb646034c227c9f1432c26ebc10dbd7d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385619"
---
# <a name="handling-recovery-operations"></a>回復操作の処理


*Recovery*内にある情報からの状態を回復する操作、トランザクション処理システム (TPS) で、試行[ログ ストリーム](using-log-streams-with-ktm.md)します。 回復操作が完了したら、すべてのトランザクションをコミット済みでなければなりませんまたは戻る状態にロールバックし、リソースのすべてのデータが正常な状態でなければなりません。

場合があります、TP は、すべてのトランザクションが完了する前に停止します。 たとえば、オペレーティング システムがクラッシュする可能性があります。 そのため、リソース マネージャーは、実行が開始されるたびに、回復操作を開始する必要があります。 回復操作は、すべてのトランザクションが完了しないかどうかを判断しようとします。 未完了のトランザクション ログで見つかると、回復操作はコミットまたはそれらのトランザクションのロールバックを試行します。

KTM ベース TP では、各復旧操作は、2 つの手順で構成されます。 最初の手順では、トランザクション マネージャー オブジェクトのログ ストリームから情報を回復する必要があります。 2 番目の手順では、リソース マネージャーのログ ストリームから情報を回復する必要があります。

TP は、すべてのログ ストリームの末尾に回復できる場合は、リソース マネージャーの管理[仮想クロック値](using-virtual-clock-values.md)クロックの指定した値になるまで復元できます。

### <a name="recovering-information-from-a-transaction-manager-objects-log-stream"></a>トランザクション マネージャー オブジェクトのログの Stream から情報を回復します。

リソース マネージャーの呼び出し直後後[ **ZwCreateTransactionManager** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcreatetransactionmanager)または[ **ZwOpenTransactionManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntopentransactionmanager)、呼び出す必要があります[ **ZwRecoverTransactionManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntrecovertransactionmanager)します。 **ZwRecoverTransactionManager**ルーチンは、トランザクション マネージャーのオブジェクトに属するログ ストリームを読み取ります。 このルーチンは、最後から始まるログ ストリームでは、回復情報の (すべてのトランザクション、参加リスト、およびリソース マネージャーを含む)、トランザクション マネージャー オブジェクトの状態を再構築します[再開領域](reading-restart-records-from-a-clfs-stream.md)その KTM を作成し、ストリームの末尾で終了します。

リソース マネージャーを呼び出すことができますに指定された仮想クロック値は、最後の再開領域から回復する[ **ZwRollforwardTransactionManager** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntrollforwardtransactionmanager)の代わりに**ZwRecoverTransactionManager**.

### <a name="recovering-information-from-a-resource-managers-log-stream"></a>Resource Manager のログの Stream から情報を回復します。

リソース マネージャーの呼び出し直後後[ **ZwCreateResourceManager** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcreateresourcemanager)または[ **ZwOpenResourceManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntopenresourcemanager)を呼び出す必要があります[**ZwRecoverResourceManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntrecoverresourcemanager)します。 **ZwRecoverResourceManager**ルーチンは、リソース マネージャーの参加リストのそれぞれに関連付けられているトランザクションを回復しようとしています。

リソース マネージャーを呼び出すと**ZwRecoverResourceManager**、KTM トランザクションを送信する\_通知\_回復[通知](transaction-notifications.md)リソース マネージャーの参加リストの各します。 リソース マネージャーを呼び出す必要があります[ **ZwRecoverEnlistment** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntrecoverenlistment)を受信するトランザクションのいずれかのたびに\_通知\_回復通知します。

リソース マネージャーを呼び出すと**ZwRecoverEnlistment**KTM は、次の通知の 1 つ送信します。

-   トランザクション\_通知\_コミット

    リソース マネージャーを選択し、そのログ ストリームでトランザクションをコミットする情報を使用する必要がありますし、呼び出す必要があります[ **ZwCommitComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcommitcomplete)します。

-   トランザクション\_通知\_ロールバック

    リソース マネージャーを選択し、そのログ ストリームで、トランザクションをロールバックする情報を使用する必要がありますし、呼び出す必要があります[ **ZwRollbackComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntrollbackcomplete)します。

-   トランザクション\_通知\_INDOUBT

    KTM では、トランザクションの状態が決定されていないと、コミットまたはロールバック通知を後で送信されます。

KTM でトランザクションを送信する通常、\_通知\_コミット通知すべてのリソース マネージャーと呼ばれることを判断した場合[ **ZwPrepareComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntpreparecomplete) TPS を停止する前に、再起動します。 KTM トランザクションを送信する\_通知\_1 つまたは複数のリソース マネージャーが呼び出さなかったことを判断した場合にロールバック通知**ZwPrepareComplete**します。

KTM でトランザクションが送信後\_通知\_各参加の回復の通知、トランザクション送信\_通知\_最後\_回復通知します。

リソース マネージャーが呼び出された場合**ZwRollforwardTransactionManager**の代わりに**ZwRecoverTransactionManager**、ことを指定した仮想のクロックの値に達するまで回復する必要があります**ZwRollforwardTransactionManager**します。

リソース マネージャーを呼び出すことができます[ **ZwSetInformationEnlistment** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntsetinformationenlistment)を設定するには、回復情報をカスタマイズします。 KTM は、この情報を保存し、ログ ストリームに書き込みますが、情報を解釈する KTM は試みません。 リソース マネージャーは、呼び出すことによって、いつでも、回復情報を取得できます[ **ZwQueryInformationEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntqueryinformationenlistment)します。

[優先的なトランザクション マネージャー](creating-a-superior-transaction-manager.md)トランザクションが表示される場合があります\_通知\_回復\_回復操作中にクエリ通知します。

 

 




