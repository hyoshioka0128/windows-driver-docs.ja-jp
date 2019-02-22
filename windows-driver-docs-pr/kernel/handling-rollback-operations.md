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
ms.openlocfilehash: 74e93ae910fc9008d1c623334d6b4b4a27b24655
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527868"
---
# <a name="handling-rollback-operations"></a>ロールバック操作の処理


リソース マネージャー、トランザクションのクライアントまたは KTM できるトランザクションをロールバックすること、トランザクションはコミットできません必要がありますと判断した場合 (通常、エラーが検出されたため)。

リソース マネージャーを呼び出すことができます、トランザクションをロールバックする[ **ZwRollbackEnlistment**](https://msdn.microsoft.com/library/windows/hardware/ff567083)します。 マネージャーが呼び出されて、リソースの後に[ **ZwCreateEnlistment** ](https://msdn.microsoft.com/library/windows/hardware/ff566422) 、トランザクションに参加させるにはトランザクションをロールバックして呼び出す前に、いつでも、 [ **ZwPrepareComplete**](https://msdn.microsoft.com/library/windows/hardware/ff567037)します。

トランザクションのクライアントはトランザクションをロールバック呼び出して[ **ZwRollbackTransaction**](https://msdn.microsoft.com/library/windows/hardware/ff567086)します。 トランザクションのクライアントが呼び出された後[ **ZwCreateTransaction** ](https://msdn.microsoft.com/library/windows/hardware/ff566429)トランザクションを作成することできますトランザクションをロールバックして呼び出す前に、いつでも、 [ **ZwCommitTransaction**](https://msdn.microsoft.com/library/windows/hardware/ff566420)します。

トランザクションのクライアントが呼び出すことによって、トランザクションのタイムアウト値を設定するさらに、 [ **ZwSetInformationTransaction**](https://msdn.microsoft.com/library/windows/hardware/ff567104)します。 KTM トランザクションをロールバック、一定の時間でコミットされていない場合。

呼び出し時に**ZwRollbackEnlistment**または**ZwRollbackTransaction**を行うと、タイムアウト値を超えると、KTM をトランザクション送信または\_通知\_ロールバック[通知](transaction-notifications.md)すべてのリソース マネージャーにします。

各リソース マネージャーがトランザクションを受信すると\_通知\_ロールバック通知では、次を行う必要があります。

1.  トランザクションのデータをトランザクションに参加しているリソース マネージャーは、前の状態に復元します。

    通常、リソース マネージャーは、データベースの公開、永続的なストレージにログ ストリームからトランザクションの保存の初期データをコピーして、トランザクションのデータを復元します。 ログ ストリームを使用する方法の詳細については、次を参照してください。 [ktm を使用するログ ストリーム](using-log-streams-with-ktm.md)します。

2.  呼び出す[ **ZwRollbackComplete**](https://msdn.microsoft.com/library/windows/hardware/ff567081)します。

呼び出した後**ZwRollbackComplete**、resource manager を呼び出す必要があります[ **ZwClose** ](https://msdn.microsoft.com/library/windows/hardware/ff566417)登録ハンドルを閉じます。

リソース マネージャーが、ロールバック操作を開始した場合、そのクライアント インターフェイスを使用して、トランザクションが失敗したクライアントに通知があります。

 

 




