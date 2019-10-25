---
title: ロールバック操作の処理
description: ロールバック操作の処理
ms.assetid: d36bfac8-47dc-4fcd-a6e2-feb27d244630
keywords:
- トランザクション WDK KTM、トランザクションのロールバック
- トランザクションのロールバック WDK KTM
- リソースマネージャー WDK KTM、ローリングバックトランザクション
- トランザクションクライアント WDK KTM、トランザクションのロールバック
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ac94689514060d498bff992977c8b51055d78c6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836481"
---
# <a name="handling-rollback-operations"></a>ロールバック操作の処理


リソースマネージャー、トランザクションクライアント、または KTM は、トランザクションがコミットされていないと判断した場合 (通常はエラーが検出されたため)、トランザクションをロールバックできます。

トランザクションをロールバックするために、リソースマネージャーは[**ZwRollbackEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrollbackenlistment)を呼び出すことができます。 リソースマネージャーは、トランザクションに参加するために[**Zwcreateenlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreateenlistment)を呼び出した後、 [**Zwの完了**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntpreparecomplete)を呼び出す前に、いつでもトランザクションをロールバックできます。

トランザクションクライアントは、 [**ZwRollbackTransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrollbacktransaction)を呼び出すことによってトランザクションをロールバックできます。 トランザクションクライアントは、トランザクションを作成するために[**Zwcreatetransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreatetransaction)を呼び出した後、いつでも[**zwcreatetransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommittransaction)を呼び出す前にトランザクションをロールバックできます。

さらに、トランザクションクライアントは、 [**Zwsetinformationtransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntsetinformationtransaction)を呼び出して、トランザクションのタイムアウト値を設定できます。 指定された時間内にコミットされていない場合、KTM はトランザクションをロールバックします。

**ZwRollbackEnlistment**または**ZwRollbackTransaction**の呼び出しが行われた場合、またはタイムアウト値を超えた場合、KTM は\_トランザクションを送信して、すべてのリソースマネージャーに\_ロールバック[通知](transaction-notifications.md)を通知します。

各リソースマネージャーは、トランザクションを受信し\_ロールバック通知を通知\_、次の操作を行う必要があります。

1.  トランザクションのデータを、リソースマネージャーがトランザクションに参加させる前の状態に復元します。

    通常、リソースマネージャーは、トランザクションの保存された初期データをログストリームからデータベースの永続ストレージにコピーすることによって、トランザクションのデータを復元します。 ログストリームの使用方法の詳細については、「 [KTM でのログストリームの使用](using-log-streams-with-ktm.md)」を参照してください。

2.  [**ZwRollbackComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrollbackcomplete)を呼び出します。

**ZwRollbackComplete**を呼び出した後、リソースマネージャーは[**zwclose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose)を呼び出して、参加リストハンドルを閉じる必要があります。

リソースマネージャーがロールバック操作を開始した場合、トランザクションが失敗したことをクライアントに通知するには、そのクライアントインターフェイスを使用する必要があります。

 

 




