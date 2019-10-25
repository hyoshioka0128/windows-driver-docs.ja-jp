---
title: トランザクション通知
description: トランザクション通知
ms.assetid: 62169b56-e70f-4d32-a051-a7fd947dbc64
keywords:
- 通知 WDK KTM
- トランザクション WDK KTM、通知
- リソースマネージャーの WDK KTM、通知
- カーネルトランザクションマネージャー WDK、通知
- KTM WDK、通知
- 上位のトランザクションマネージャー WDK KTM
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a425b3fddd5986e934b2d385eda2a8b9ba71257
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838383"
---
# <a name="transaction-notifications"></a>トランザクション通知


KTM は、各リソースマネージャーの通知キューを提供します。 KTM は、リソースマネージャーのキューに配置することによって、リソースマネージャーに通知を配信します。

リソースマネージャーは、同期または非同期のいずれかで、キューから通知を取得できます。

-   通知を同期的に取得するには、リソースマネージャーが[**Zwgetnotificationresourcemanager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntgetnotificationresourcemanager)を繰り返し呼び出すことができます。

-   通知を非同期に受信するために、リソースマネージャーは[**Tmenablecallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-tmenablecallbacks)を呼び出して、コールバックルーチンを設定できます。 KTM は、リソースマネージャーのキューに通知を配置するたびにコールバックルーチンを呼び出します。

リソースマネージャーが[**Zwcreateenlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreateenlistment)を呼び出してトランザクションの参加リストを作成する場合、リソースマネージャーは受信する通知の種類を指定します。 リソースマネージャーは、受信するために登録された通知のみを受信します。

通知定数は、Ktmtypes. h で定義されています。 通知定数名には、 *Xxx*\_通知\_トランザクションの形式があります。

このトピックの残りの部分では、Ktmtypes によって定義され、3つのグループに分割されるすべての通知定数を示します。

-   リソースマネージャーが受信できる通知

-   上位トランザクションマネージャーが受信できる通知

-   定義されているが現在使用されていない通知定数

### <a href="" id="notifications-for-resource-managers"></a>リソースマネージャーの通知

すべてのリソースマネージャーは、トランザクションを受け取るために登録する必要があります。\_事前準備、トランザクション\_通知\_準備、およびトランザクション\_は、後でを呼び出し[**た場合でもコミット通知を通知\_通知\_ます。ZwReadOnlyEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntreadonlyenlistment)は、参加リストを読み取り専用としてマークします。

リソースマネージャーは、トランザクション\_をサポートして、単一\_フェーズ\_コミット\_通知を行うことができますが、マルチフェーズ事前準備、準備、およびコミット通知もサポートする必要があります。

次の一覧には、リソースマネージャーが受信できるすべての通知が含まれています。

<a href="" id="transaction-notify-preprepare"></a>トランザクション\_\_PREPREPARE に通知する  
**送信された場合**: クライアントは[**Zwcommittransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommittransaction)を呼び出しますが、リソースマネージャーが単一フェーズコミットをサポートしていないか、[上位トランザクションマネージャー](creating-a-superior-transaction-manager.md)が[**zwcommittransaction 参加リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntpreprepareenlistment)を呼び出しています。

**受信者**: リソースマネージャー。

**受信者の必須のアクション**: 事前準備操作を実行し、 [**Zwpreプロビジョニング完了**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntprepreparecomplete)を呼び出します。 (事前準備操作の詳細については、「[コミット操作の処理](handling-commit-operations.md)」を参照してください)。

**制限:** リソースマネージャーは、トランザクション\_をサポートする必要もあります。\_準備とトランザクション\_通知\_コミットに通知します。

<a href="" id="transaction-notify-prepare"></a>トランザクション\_通知\_準備  
**送信時**: クライアントが[**Zwcommittransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommittransaction)を呼び出し、リソースマネージャーが単一フェーズコミットをサポートしていない場合、または上位トランザクションマネージャーが[**zw/参加リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntprepareenlistment)を呼び出す場合、トランザクション\_後に、事前準備\_通知します。

**受信者**: リソースマネージャー。

**受信者の必須の操作:** 準備操作を実行し、 [**Zw/complete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntpreparecomplete)を呼び出します。 (準備操作の詳細については、「[コミット操作の処理](handling-commit-operations.md)」を参照してください)。

**制限:** リソースマネージャーは、トランザクション\_をサポートしている必要があります\_事前準備とトランザクション\_\_COMMIT を通知します。

<a href="" id="transaction-notify-commit"></a>コミット\_通知するトランザクション\_  
**送信時**: クライアントが[**Zwcommittransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommittransaction)を呼び出し、リソースマネージャーが単一フェーズコミットをサポートしていない場合、または上位トランザクションマネージャーが[**zwcommittransaction リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommitenlistment)を呼び出す場合、トランザクション\_後に通知\_準備をします。

**受信者**: リソースマネージャー。

**受信者の必須のアクション**: コミット操作を実行し、 [**Zwcommitcomplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommitcomplete)を呼び出します。 (コミット操作の詳細については、「[コミット操作の処理](handling-commit-operations.md)」を参照してください)。

**制限:** リソースマネージャーは、トランザクション\_\_事前準備とトランザクション\_通知\_準備を行う必要があります。

<a href="" id="transaction-notify-single-phase-commit"></a>トランザクション\_\_単一\_フェーズ\_コミットに通知します  
**送信された場合**: クライアントは[**Zwcommittransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommittransaction)を呼び出し、resource manager は単一フェーズコミット操作をサポートします。

**受信者**: リソースマネージャー。

**受信者の必須のアクション**: トランザクションをコミットするか、 [**ZwSinglePhaseReject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntsinglephasereject)を呼び出します。 (単一フェーズコミット操作の詳細については、「[コミット操作の処理](handling-commit-operations.md)」を参照してください)。

**制限:** リソースマネージャーは、トランザクション\_もサポートしている必要があります。\_事前準備、トランザクション\_通知\_準備、およびトランザクション\_コミット\_通知します。

<a href="" id="transaction-notify-rollback"></a>トランザクション\_通知\_ロールバック  
**送信されると**、クライアントが[**ZwRollbackTransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrollbacktransaction)を呼び出すか、上位のトランザクションマネージャーが[**ZwRollbackEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrollbackenlistment)を呼び出します。または、KTM によってエラー (ログストリームへの書き込みに失敗したなど) が検出されます。

**受信者**: リソースマネージャーと上位トランザクションマネージャーの両方。

**受信者の必須のアクション**: トランザクションのデータをロールバックするために必要な操作を実行し、 [**ZwRollbackComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrollbackcomplete)を呼び出します。 (ロールバック操作の詳細については、「[ロールバック操作の処理](handling-rollback-operations.md)」を参照してください)。

**制限:** すべてのリソースマネージャーと上位のトランザクションマネージャーは、トランザクションをサポートして\_ロールバックを通知\_必要があります。

<a href="" id="transaction-notify-recover"></a>トランザクション\_\_の回復を通知する  
**送信された場合**: リソースマネージャーは、 [**Zw回復マネージャー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrecoverresourcemanager)を呼び出します。

**受信者**: リソースマネージャー。

**受信者の必須アクション**: リソースマネージャーは、 [**Zw回復参加リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrecoverenlistment)を呼び出す必要があります。 (回復操作の詳細については、「[復旧操作の処理](handling-recovery-operations.md)」を参照してください)。

**制限:** 存在.

<a href="" id="transaction-notify-last-recover"></a>最後\_回復\_通知するトランザクション\_  
**送信日時**: KTM が最後のトランザクションを送信した後に、リソースマネージャーの参加リストを\_復旧\_通知します。

**受信者**: リソースマネージャー。

**受信者の必須の操作**: 回復操作を終了します。 (回復操作の詳細については、「[復旧操作の処理](handling-recovery-operations.md)」を参照してください)。

**制限:** 存在.

<a href="" id="transaction-notify-indoubt"></a>トランザクション\_通知\_INDOUBT  
**送信時**: リソースマネージャーが[**Zw回復参加リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrecoverenlistment)を呼び出した後、KTM がトランザクションをコミットするかロールバックするかを決定できない場合 (通常は、tp に使用できない上位のトランザクションマネージャーがあるため)。

受信者: リソースマネージャー。

**受信者の必須のアクション**: KTM がトランザクションを送信するまで何もしないで、\_コミットまたはトランザクション\_通知\_ロールバックを通知\_ます。

**制限:** 存在.

<a href="" id="transaction-notify-rm-disconnected"></a>\_RM\_DISCONNECTED に通知するトランザクション\_  
**送信された場合**: 単一フェーズのコミット操作を処理しているリソースマネージャーは、トランザクションをコミットまたはロールバックしたことを示すことなく、参加リストを閉じます。

**受信者**: トランザクションに参加しているリソースマネージャーと上位のトランザクションマネージャー。

**受信者の必須の操作**: トランザクション固有のクリーンアップ操作。 通常、この通知は読み取り専用のリソースマネージャーに役立ちます。

**制限:** 存在.

### <a href="" id="notifications-for-superior-transaction-managers"></a>上位トランザクションマネージャーの通知

[上位トランザクションマネージャー](creating-a-superior-transaction-manager.md)は、次の通知を受け取ることができます。

<a href="" id="transaction-notify-rollback"></a>トランザクション\_通知\_ロールバック  
前の説明を参照してください。

<a href="" id="transaction-notify-rm-disconnected"></a>\_RM\_DISCONNECTED に通知するトランザクション\_  
前の説明を参照してください。

<a href="" id="transaction-notify-preprepare-complete"></a>トランザクション\_\_PREPREPARE\_完了を通知します  
**送信日時**: すべてのリソースマネージャーがトランザクションを受信した後に、 [**Zwpreプロビジョニング完了**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntprepreparecomplete)を呼び出して\_事前準備と応答を\_に通知します。

**受信者**: 上位トランザクションマネージャー。

**受信者の必須のアクション**: 上位トランザクションマネージャーは[**Zw/参加リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntprepareenlistment)を呼び出す必要があります。

<a href="" id="transaction-notify-prepare-complete"></a>トランザクション\_通知\_準備\_完了  
**送信された場合**: すべてのリソースマネージャーがトランザクションを受信した後に、 [**Zwの完了**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntpreparecomplete)を呼び出して準備と応答を\_に通知\_通知します。

**受信者**: 上位トランザクションマネージャー。

**受信者の必須のアクション**: 上位トランザクションマネージャーは[**Zwcommitenlistment リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommitenlistment)を呼び出す必要があります。

<a href="" id="transaction-notify-commit-complete"></a>トランザクション\_\_コミット\_完了を通知します  
**送信された場合**: すべてのリソースマネージャーがトランザクションを受信した後\_\_コミットに通知し、 [**Zwcommitcomplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommitcomplete)を呼び出して応答します。

**受信者**: 上位トランザクションマネージャー。

**受信者の必須のアクション**: トランザクションのクリーンアップ操作。

<a href="" id="transaction-notify-rollback-complete"></a>トランザクション\_\_ロールバック\_完了を通知します  
**送信日時**: すべてのリソースマネージャーがトランザクションを受信した後、 [**ZwRollbackComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrollbackcomplete)を呼び出すことによって\_ロールバックを通知し、応答\_ます。

**受信者**: 上位トランザクションマネージャー。

**受信者の必須のアクション**: トランザクションのクリーンアップ操作。

<a href="" id="transaction-notify-recover-query"></a>トランザクション\_通知\_復旧\_クエリ  
**送信時**: 上位トランザクションマネージャーが[**zw回復**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrecoverresourcemanager)マネージャーを呼び出します。

**受信者**: 上位トランザクションマネージャー。

**受信者の必須アクション**: 上位トランザクションマネージャーは、参加リストに対して[**Zwcommitenlistment リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommitenlistment)または[**ZwRollbackEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrollbackenlistment)のいずれかを呼び出す必要があります。

<a href="" id="transaction-notify-commit-request"></a>トランザクション\_\_コミット\_要求に通知します  
**送信日時**: クライアントは[**Zwcommittransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommittransaction)を呼び出します。 上位トランザクションマネージャーが参加リストに対してこの通知を登録している場合、KTM はトランザクション\_通知を送信するのでは**なく**、\_コミット\_要求\_通知します。リソースマネージャーにコミット\_ます。

**受信者**: 上位トランザクションマネージャー。

**受信者の必須のアクション**: 上位トランザクションマネージャーが[**Zwcommitenlistment リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommitenlistment)を呼び出します。

<a href="" id="transaction-notify-request-outcome"></a>トランザクション\_\_要求\_結果に通知します  
**送信時**: リソースマネージャーは、トランザクションが準備された状態のときに[**TmRequestOutcomeEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-tmrequestoutcomeenlistment)を呼び出します。

**受信者**: 上位トランザクションマネージャー。

**受信者の必須のアクション**: 上位トランザクションマネージャーは[**Zwcommitenlistment リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommitenlistment)または[**ZwRollbackEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrollbackenlistment)を呼び出す必要があります。

### <a href="" id="unused-notifications"></a>未使用の通知

次の通知は Ktmtypes .h で定義されていますが、現在、KTM ではサポートされていません。

トランザクション\_\_デリゲート\_COMMIT に通知します

\_マスクの参加\_トランザクション\_通知

トランザクション\_通知\_登録\_事前準備

トランザクション\_通知\_マーシャリング

トランザクション\_通知\_昇格

トランザクション\_通知\_昇格\_新規

トランザクション\_通知\_伝達\_プル

トランザクション\_通知\_伝達\_プッシュ

トランザクション\_\_TM\_オンラインに通知します

トランザクション\_\_コミット\_最終処理に通知します

 

 




