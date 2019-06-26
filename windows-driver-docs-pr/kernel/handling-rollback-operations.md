---
title: ロールバック操作の処理
description: ロールバック操作の処理
ms.assetid: d36bfac8-47dc-4fcd-a6e2-feb27d244630
keywords:
- トランザクション WDK KTM をトランザクションのロールバック
- WDK KTM トランザクションをロールバックしています
- リソース マネージャー WDK KTM、バッキング トランザクション ロール
- WDK KTM をトランザクションのロールバック トランザクションのクライアント
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a700c30af4d7f1e686df6e1b796c9342a8b9ff7c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385618"
---
# <a name="handling-rollback-operations"></a>ロールバック操作の処理


リソース マネージャー、トランザクションのクライアントまたは KTM できるトランザクションをロールバックすること、トランザクションはコミットできません必要がありますと判断した場合 (通常、エラーが検出されたため)。

リソース マネージャーを呼び出すことができます、トランザクションをロールバックする[ **ZwRollbackEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntrollbackenlistment)します。 マネージャーが呼び出されて、リソースの後に[ **ZwCreateEnlistment** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcreateenlistment) 、トランザクションに参加させるにはトランザクションをロールバックして呼び出す前に、いつでも、 [ **ZwPrepareComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntpreparecomplete)します。

トランザクションのクライアントはトランザクションをロールバック呼び出して[ **ZwRollbackTransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntrollbacktransaction)します。 トランザクションのクライアントが呼び出された後[ **ZwCreateTransaction** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcreatetransaction)トランザクションを作成することできますトランザクションをロールバックして呼び出す前に、いつでも、 [ **ZwCommitTransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcommittransaction)します。

トランザクションのクライアントが呼び出すことによって、トランザクションのタイムアウト値を設定するさらに、 [ **ZwSetInformationTransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntsetinformationtransaction)します。 KTM トランザクションをロールバック、一定の時間でコミットされていない場合。

呼び出し時に**ZwRollbackEnlistment**または**ZwRollbackTransaction**を行うと、タイムアウト値を超えると、KTM をトランザクション送信または\_通知\_ロールバック[通知](transaction-notifications.md)すべてのリソース マネージャーにします。

各リソース マネージャーがトランザクションを受信すると\_通知\_ロールバック通知では、次を行う必要があります。

1.  トランザクションのデータをトランザクションに参加しているリソース マネージャーは、前の状態に復元します。

    通常、リソース マネージャーは、データベースの公開、永続的なストレージにログ ストリームからトランザクションの保存の初期データをコピーして、トランザクションのデータを復元します。 ログ ストリームを使用する方法の詳細については、次を参照してください。 [ktm を使用するログ ストリーム](using-log-streams-with-ktm.md)します。

2.  呼び出す[ **ZwRollbackComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntrollbackcomplete)します。

呼び出した後**ZwRollbackComplete**、resource manager を呼び出す必要があります[ **ZwClose** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntclose)登録ハンドルを閉じます。

リソース マネージャーが、ロールバック操作を開始した場合、そのクライアント インターフェイスを使用して、トランザクションが失敗したクライアントに通知があります。

 

 




