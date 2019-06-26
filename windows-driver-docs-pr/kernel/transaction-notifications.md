---
title: トランザクション通知
description: トランザクション通知
ms.assetid: 62169b56-e70f-4d32-a051-a7fd947dbc64
keywords:
- WDK KTM の通知
- WDK KTM、通知のトランザクション
- WDK KTM、通知のリソース マネージャー
- カーネル トランザクション マネージャ WDK、通知
- KTM WDK、通知
- 優先的なトランザクション マネージャー WDK KTM
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d231f88e1dfca5914c354251e739799adc184be
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382953"
---
# <a name="transaction-notifications"></a>トランザクション通知


KTM では、各リソース マネージャーの通知キューを提供します。 KTM では、リソース マネージャーのキューに置くことによって、リソース マネージャーに通知を配信します。

リソース マネージャーは、同期または非同期で、そのキューから通知を取得できます。

-   リソース マネージャーを繰り返し呼び出しする通知を同期的に取得する[ **ZwGetNotificationResourceManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntgetnotificationresourcemanager)します。

-   通知を非同期的に受信する、resource manager を呼び出すことができます[ **TmEnableCallbacks** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-tmenablecallbacks)コールバック ルーチンを設定します。 その it はこのリソース マネージャーのキューに通知するたびに、KTM は、コールバック ルーチンを呼び出します。

リソース マネージャーを呼び出すと[ **ZwCreateEnlistment** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcreateenlistment)リソース マネージャーをトランザクションの参加リストを作成するを受信する通知の種類を指定します。 リソース マネージャーでは、ご登録いただく通知だけを受信します。

通知の定数は、Ktmtypes.h で定義されます。 トランザクションの形式である通知の定数名\_通知\_*Xxx*します。

このトピックの残りの部分では、すべての通知定数 Ktmtypes.h を定義し、3 つのグループに分割して、示します。

-   リソース マネージャーが受信可能な通知

-   優先的なトランザクション マネージャーが受信可能な通知

-   定義されているが、現在使用されていない通知定数

### <a href="" id="notifications-for-resource-managers"></a> リソース マネージャーの通知

トランザクションを受信するすべてのリソース マネージャーを登録する必要があります\_通知\_PREPREPARE、トランザクション\_通知\_準備、およびトランザクション\_通知\_でもコミット通知その後を呼び出す場合に[ **ZwReadOnlyEnlistment** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntreadonlyenlistment)読み取り専用と参加リストをマークします。

リソース マネージャーがトランザクションをサポートできる\_通知\_単一\_フェーズ\_がコミットする必要がありますも複数フェーズ pre-prepare をサポートして、準備、および通知をコミットします。

次の一覧には、リソース マネージャーが受信可能なすべての通知が含まれています。

<a href="" id="transaction-notify-preprepare"></a>トランザクション\_通知\_PREPREPARE  
**送信されたときに**:クライアントが呼び出す[ **ZwCommitTransaction** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcommittransaction)とリソース マネージャーが単一フェーズ コミットをサポートしない場合は、[優先的なトランザクション マネージャー](creating-a-superior-transaction-manager.md)呼び出し[ **ZwPrePrepareEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntpreprepareenlistment)します。

**受信した**:リソース マネージャー。

**受信者のアクションを必須**:実行操作を事前に準備し、呼び出す[ **ZwPrePrepareComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntprepreparecomplete)します。 (詳細については操作を事前準備を参照してください[コミット操作の処理](handling-commit-operations.md))。

**制限:** リソース マネージャーがトランザクションをサポートする必要がありますも\_通知\_準備とトランザクション\_通知\_をコミットします。

<a href="" id="transaction-notify-prepare"></a>トランザクション\_通知\_準備  
**送信されたときに**:トランザクション後\_通知\_PREPREPARE クライアントが呼び出す場合[ **ZwCommitTransaction** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcommittransaction)リソース マネージャーが単一フェーズ コミットをサポートしないと、優先的なトランザクションの場合、またはmanager 呼び出し[ **ZwPrepareEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntprepareenlistment)します。

**受信した**:リソース マネージャー。

**受信者には、アクションを必須します。** 実行操作を準備し、呼び出す[ **ZwPrepareComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntpreparecomplete)します。 (詳細については操作の準備を参照してください[コミット操作の処理](handling-commit-operations.md))。

**制限:** リソース マネージャーがトランザクションをサポートする必要がありますも\_通知\_PREPREPARE とトランザクション\_通知\_をコミットします。

<a href="" id="transaction-notify-commit"></a>トランザクション\_通知\_コミット  
**送信されたときに**:トランザクション後\_通知\_クライアントが呼び出す場合の準備[ **ZwCommitTransaction** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcommittransaction)リソース マネージャーが単一フェーズ コミットをサポートしないと、優先的なトランザクションの場合、またはmanager 呼び出し[ **ZwCommitEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcommitenlistment)します。

**受信した**:リソース マネージャー。

**受信者のアクションを必須**:コミット操作を行い、呼び出して[ **ZwCommitComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcommitcomplete)します。 (コミット操作の詳細については、次を参照してください[コミット操作の処理](handling-commit-operations.md)。)。

**制限:** リソース マネージャーがトランザクションをサポートする必要がありますも\_通知\_PREPREPARE とトランザクション\_通知\_準備します。

<a href="" id="transaction-notify-single-phase-commit"></a>トランザクション\_通知\_単一\_フェーズ\_コミット  
**送信されたときに**:クライアントが呼び出す[ **ZwCommitTransaction** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcommittransaction)リソース マネージャーが単一フェーズ コミット操作をサポートしています。

**受信した**:リソース マネージャー。

**受信者のアクションを必須**:呼び出し、トランザクションをコミットするか[ **ZwSinglePhaseReject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntsinglephasereject)します。 (単一フェーズ コミット操作の詳細については、次を参照してください[コミット操作の処理](handling-commit-operations.md)。)。

**制限:** リソース マネージャーがトランザクションをサポートする必要がありますも\_通知\_PREPREPARE、トランザクション\_通知\_準備、およびトランザクション\_通知\_をコミットします。

<a href="" id="transaction-notify-rollback"></a>トランザクション\_通知\_ロールバック  
**送信されたときに**:クライアントが呼び出す[ **ZwRollbackTransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntrollbacktransaction)、優先的なトランザクション マネージャーは、 [ **ZwRollbackEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntrollbackenlistment)KTM を検出したか、ログ ストリームに失敗した書き込み) などのエラーです。

**受信した**:リソース マネージャーと優れたトランザクション マネージャーの両方。

**受信者のアクションを必須**:トランザクションのデータをロールバックし、呼び出すために必要な操作を実行[ **ZwRollbackComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntrollbackcomplete)します。 (ロールバック操作の詳細については、次を参照してください[ロールバック操作の処理](handling-rollback-operations.md)。)。

**制限:** すべてのリソース マネージャーおよび優先的なトランザクション マネージャーがトランザクションをサポートする必要があります\_通知\_ロールバックします。

<a href="" id="transaction-notify-recover"></a>トランザクション\_通知\_回復  
**送信されたときに**:リソース マネージャーは、 [ **ZwRecoverResourceManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntrecoverresourcemanager)します。

**受信した**:リソース マネージャー。

**受信者のアクションを必須**:リソース マネージャーを呼び出す必要があります[ **ZwRecoverEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntrecoverenlistment)します。 (回復操作の詳細については、次を参照してください[回復操作の処理](handling-recovery-operations.md)。)。

**制限:** なし。

<a href="" id="transaction-notify-last-recover"></a>トランザクション\_通知\_最後\_回復  
**送信されたときに**:KTM で最後のトランザクションが送信後\_通知\_リソース マネージャーの参加リストを回復します。

**受信した**:リソース マネージャー。

**受信者のアクションを必須**:回復操作を終了します。 (回復操作の詳細については、次を参照してください[回復操作の処理](handling-recovery-operations.md)。)。

**制限:** なし。

<a href="" id="transaction-notify-indoubt"></a>トランザクション\_通知\_INDOUBT  
**送信されたときに**:リソース マネージャーを呼び出してから[ **ZwRecoverEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntrecoverenlistment)KTM は、トランザクションをコミットまたはロールバックするかどうかを判断できない場合、(通常、優先的なトランザクション マネージャーが、TPご利用いただけません)。

受信しました。リソース マネージャー。

**受信者のアクションを必須**:KTM トランザクションを送信するまで何もしない\_通知\_COMMIT transaction または TRANSACTION\_通知\_ロールバックします。

**制限:** なし。

<a href="" id="transaction-notify-rm-disconnected"></a>トランザクション\_通知\_RM\_切断  
**送信されたときに**:単一フェーズ コミット操作を処理しているリソース マネージャーは、ことを示すことがコミットされたトランザクションをロールバックせず登録ハンドルを閉じます。

**受信した**:リソース マネージャーと優れたトランザクション マネージャーをトランザクションの参加リストを持ちます。

**受信者のアクションを必須**:トランザクションに固有のクリーンアップ操作。 通常、この通知は、読み取り専用のリソース マネージャーに便利です。

**制限:** なし。

### <a href="" id="notifications-for-superior-transaction-managers"></a> 優先的なトランザクション マネージャーの通知

[優先的なトランザクション マネージャー](creating-a-superior-transaction-manager.md)次の通知を受け取ることができます。

<a href="" id="transaction-notify-rollback"></a>トランザクション\_通知\_ロールバック  
以前の説明を参照してください。

<a href="" id="transaction-notify-rm-disconnected"></a>トランザクション\_通知\_RM\_切断  
以前の説明を参照してください。

<a href="" id="transaction-notify-preprepare-complete"></a>トランザクション\_通知\_PREPREPARE\_完了  
**送信されたときに**:すべてのリソースの後に、マネージャーのトランザクションが受信した\_通知\_PREPREPARE 呼び出すことで応答し[ **ZwPrePrepareComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntprepreparecomplete)します。

**受信した**:優先的なトランザクション マネージャー。

**受信者のアクションを必須**:上位のトランザクション マネージャーを呼び出す必要があります[ **ZwPrepareEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntprepareenlistment)します。

<a href="" id="transaction-notify-prepare-complete"></a>トランザクション\_通知\_準備\_完了  
**送信されたときに**:すべてのリソースの後に、マネージャーのトランザクションが受信した\_通知\_準備と呼び出すことによって応答[ **ZwPrepareComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntpreparecomplete)します。

**受信した**:優先的なトランザクション マネージャー。

**受信者のアクションを必須**:上位のトランザクション マネージャーを呼び出す必要があります[ **ZwCommitEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcommitenlistment)します。

<a href="" id="transaction-notify-commit-complete"></a>トランザクション\_通知\_コミット\_完了  
**送信されたときに**:すべてのリソースの後に、マネージャーのトランザクションが受信した\_通知\_をコミットし、呼び出すことによって応答[ **ZwCommitComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcommitcomplete)します。

**受信した**:優先的なトランザクション マネージャー。

**受信者のアクションを必須**:トランザクションのクリーンアップ操作。

<a href="" id="transaction-notify-rollback-complete"></a>トランザクション\_通知\_ロールバック\_完了  
**送信されたときに**:すべてのリソースの後に、マネージャーのトランザクションが受信した\_通知\_ロールバックと呼び出すことによって応答[ **ZwRollbackComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntrollbackcomplete)します。

**受信した**:優先的なトランザクション マネージャー。

**受信者のアクションを必須**:トランザクションのクリーンアップ操作。

<a href="" id="transaction-notify-recover-query"></a>トランザクション\_通知\_回復\_クエリ  
**送信されたときに**:優先的なトランザクション マネージャーは、 [ **ZwRecoverResourceManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntrecoverresourcemanager)します。

**受信した**:優先的なトランザクション マネージャー。

**受信者のアクションを必須**:上位のトランザクション マネージャーは、いずれかを呼び出す必要があります[ **ZwCommitEnlistment** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcommitenlistment)または[ **ZwRollbackEnlistment** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntrollbackenlistment)の参加します。

<a href="" id="transaction-notify-commit-request"></a>トランザクション\_通知\_コミット\_要求  
**送信されたときに**:クライアントが呼び出す[ **ZwCommitTransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcommittransaction)します。 優先的なトランザクション マネージャーが参加リスト用には、この通知の登録、KTM 送信トランザクション\_通知\_コミット\_優れたトランザクション マネージャーに要求**の代わりに**トランザクションを送信する\_通知\_リソース マネージャーにコミットします。

**受信した**:優先的なトランザクション マネージャー。

**受信者のアクションを必須**:優先的なトランザクション マネージャーの呼び出し[ **ZwCommitEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcommitenlistment)します。

<a href="" id="transaction-notify-request-outcome"></a>トランザクション\_通知\_要求\_結果  
**送信されたときに**:リソース マネージャーは、 [ **TmRequestOutcomeEnlistment** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-tmrequestoutcomeenlistment)トランザクションの準備済み状態の中。

**受信した**:優先的なトランザクション マネージャー。

**受信者のアクションを必須**:上位のトランザクション マネージャーを呼び出す必要があります[ **ZwCommitEnlistment** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcommitenlistment)または[ **ZwRollbackEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntrollbackenlistment)します。

### <a href="" id="unused-notifications"></a> 未使用の通知

次の通知が Ktmtypes.h で定義されますが、KTM 現在はサポートしていません。

トランザクション\_通知\_デリゲート\_コミット

トランザクション\_通知\_参加\_マスク

トランザクション\_通知\_参加\_PREPREPARE

トランザクション\_通知\_マーシャ リングする.

トランザクション\_通知\_昇格

トランザクション\_通知\_昇格\_新規

トランザクション\_通知\_伝達\_プル

トランザクション\_通知\_伝達\_プッシュ

トランザクション\_通知\_TM\_オンライン

トランザクション\_通知\_コミット\_FINALIZE

 

 




