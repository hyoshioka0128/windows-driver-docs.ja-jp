---
title: 回復操作の処理
description: 回復操作の処理
ms.assetid: 35149bb9-fd48-44d3-a9fd-0e631aa0e853
keywords:
- トランザクション WDK KTM、トランザクションの復旧
- トランザクションの回復 WDK KTM
- トランザクション処理システム WDK KTM、トランザクションの復旧
- TP WDK KTM、トランザクションの復旧
- ログストリーム WDK KTM, トランザクションの復旧
- 仮想クロック値 WDK KTM、トランザクションの復旧
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 149d9568561723053854137aa796585b0de43b63
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838653"
---
# <a name="handling-recovery-operations"></a>回復操作の処理


*復旧*操作では、トランザクション処理システム (TPS) は、[ログストリーム](using-log-streams-with-ktm.md)内の情報から状態を回復しようとします。 回復操作が完了すると、すべてのトランザクションがコミット済みまたはロールバック状態になり、すべてのリソースデータが既知の良好な状態である必要があります。

TP は、すべてのトランザクションが終了する前に停止することがあります。 たとえば、オペレーティングシステムがクラッシュする可能性があります。 そのため、リソースマネージャーは、実行が開始されるたびに復旧操作を開始する必要があります。 復旧操作では、トランザクションが不完全であるかどうかを判断しようとします。 不完全なトランザクションがログに見つかった場合、復旧操作では、これらのトランザクションのコミットまたはロールバックが試行されます。

KTM ベースの TP の場合、各復旧操作は2つの手順で構成されます。 最初の手順では、トランザクションマネージャーオブジェクトのログストリームから情報を回復します。 2番目の手順では、リソースマネージャーのログストリームから情報を回復します。

TP は、すべてのログストリームの末尾に復旧できます。また、リソースマネージャーが[仮想クロック値](using-virtual-clock-values.md)を保持している場合は、指定されたクロック値まで回復できます。

### <a name="recovering-information-from-a-transaction-manager-objects-log-stream"></a>トランザクションマネージャーオブジェクトのログストリームからの情報の回復

リソースマネージャーは、 [**Zwcreatetransactionmanager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreatetransactionmanager)または[**zwcreatetransactionmanager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntopentransactionmanager)を呼び出した直後に、 [**zwの**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrecovertransactionmanager)transactionmanager を呼び出す必要があります。 **Zw回復**するルーチンは、トランザクションマネージャーオブジェクトに属しているログストリームを読み取ります。 このルーチンは、KTM が作成した最後の[再開領域](reading-restart-records-from-a-clfs-stream.md)から開始して、ログストリーム内の復旧情報からトランザクションマネージャーオブジェクト (すべてのトランザクション、参加リスト、およびリソースマネージャーを含む) の状態を再構築します。ストリームの末尾で終了します。

指定した仮想クロック値まで最後の再起動領域から回復するために、リソースマネージャーは**ZwZwRollforwardTransactionManager transactionmanager**ではなく、 [](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrollforwardtransactionmanager)を呼び出すことができます。

### <a name="recovering-information-from-a-resource-managers-log-stream"></a>リソースマネージャーのログストリームから情報を回復する

リソースマネージャーは、 [**Zwcreateresourcemanager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreateresourcemanager)または[**zwopenresourcemanager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntopenresourcemanager)を呼び出した直後に、 [**zwの**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrecoverresourcemanager)resourcemanager を呼び出す必要があります。 **Zw回復マネージャー**ルーチンは、各リソースマネージャーの参加リストに関連付けられているトランザクションを復旧しようとします。

リソースマネージャーが**Zw回復マネージャー**を呼び出すと、KTM によってトランザクション\_通知され、各リソースマネージャーの参加リストの[通知](transaction-notifications.md)\_復旧できます。 リソースマネージャーは、トランザクションの1つを受信するたびに[**Zwの参加リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrecoverenlistment)を呼び出す必要があります\_通知\_回復します。

リソースマネージャーが**Zw回復参加リスト**を呼び出すと、KTM は次のいずれかの通知を送信します。

-   コミット\_通知するトランザクション\_

    リソースマネージャーは、ログストリーム内の情報を使用してトランザクションをコミットした後、 [**Zwcommitcomplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommitcomplete)を呼び出す必要があります。

-   トランザクション\_通知\_ロールバック

    リソースマネージャーは、ログストリーム内の情報を使用してトランザクションをロールバックし、次に[**ZwRollbackComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrollbackcomplete)を呼び出す必要があります。

-   トランザクション\_通知\_INDOUBT

    KTM はトランザクションの状態を特定しておらず、後でコミットまたはロールバックの通知を送信します。

通常、KTM は、TP が停止して再起動される前に、 [**Zwに**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntpreparecomplete)呼び出されたすべてのリソースマネージャーが完了したと判断した場合に、\_コミット通知を通知\_トランザクションを送信します。 KTM は、1つまたは複数のリソースマネージャーが**Zwの完了**を呼び出していないと判断した場合に、\_ロールバック通知を通知\_トランザクションを送信します。

KTM によってトランザクションが送信された後、各登録について\_復旧通知を通知\_、最後\_回復通知を\_に通知\_トランザクションを送信します。

リソースマネージャーが**ZwZwRollforwardTransactionManager transactionmanager**ではなくを呼び出した場合は、 **ZwRollforwardTransactionManager**に指定された仮想時計の値までのみ回復する必要があります。

リソースマネージャーは、 [**Zwsetinformationenlistment リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntsetinformationenlistment)を呼び出して、カスタマイズされた回復情報を設定できます。 KTM は、この情報を保存してログストリームに書き込みますが、KTM は情報を解釈しません。 リソースマネージャーは、 [**Zwqueryinformationenlistment リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntqueryinformationenlistment)を呼び出すことによって、いつでも回復情報を取得できます。

[優れたトランザクションマネージャー](creating-a-superior-transaction-manager.md)は、復旧操作中に\_クエリ通知を回復\_に通知\_トランザクションを受け取ることがあります。

 

 




