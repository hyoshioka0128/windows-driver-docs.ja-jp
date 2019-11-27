---
title: 仮想クロック値の使用
description: 仮想クロック値の使用
ms.assetid: de01b0f1-86b1-4e7d-af22-84dbbe3a3f83
keywords:
- 仮想クロック値 WDK KTM
- カーネルトランザクションマネージャー WDK、仮想クロック値
- KTM WDK、仮想クロック値
- トランザクション WDK KTM、仮想クロック値
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce58b80603856f2311357e66b621eba6c91fbba7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835815"
---
# <a name="using-virtual-clock-values"></a>仮想クロック値の使用


KTM は、各トランザクションマネージャーオブジェクトの仮想時計を提供します。 リソースマネージャーが[**Zwcreatetransactionmanager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreatetransactionmanager)を呼び出すと、KTM によってオブジェクトの仮想クロック値が1に設定されます。 KTM は、コミット操作が開始されるたびに、仮想クロック値をインクリメントします。 KTM がログストリームに書き込むたびに、ログレコードに現在の仮想クロック値が含まれます。

リソースマネージャーが[**Zwを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrecovertransactionmanager)呼び出すと、KTM は、ストリームの最後までログストリームレコードを読み取り、トランザクションマネージャーオブジェクトの仮想クロック値を、オブジェクトのログストリームで最後に検出された値に設定します。

リソースマネージャーが[**ZwRollforwardTransactionManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrollforwardtransactionmanager)を呼び出すと、KTM は、指定されたクロック値までログストリームレコードを読み取り、トランザクションマネージャーオブジェクトの仮想クロック値を指定されたクロック値に設定します。

KTM を使用すると、リソースマネージャーと上位トランザクションマネージャーはトランザクションマネージャーオブジェクトの仮想クロック値を変更できますが、通常はクロック値を変更する必要はありません。

### <a name="when-to-modify-virtual-clock-values"></a>仮想クロック値を変更する場合

通常、TP 内のコンポーネントが複数のログストリームを同期しようとしない限り、トランザクション処理システム (TPS) は仮想クロック値を変更する必要はありません。

たとえば、事前準備/準備/コミットシーケンス中に相互に通信する複数のリソースマネージャーが TP に含まれているとします。 また、各リソースマネージャーが一意のログストリームを持つトランザクションマネージャーオブジェクトを作成するとします。 KTM によって復旧操作中にすべてのリソースマネージャーの状態が同じ時点に復元されるようにするには、これらのリソースマネージャーが次の手順を使用することがあります。

-   あるリソースマネージャーが別のリソースマネージャーと通信すると、KTM または他のリソースマネージャーから受信した最新の仮想クロック値が渡されます。

-   リソースマネージャーは、仮想クロック値を受け取る KTM ルーチンを呼び出すたびに (このトピックの次のセクションを参照)、KTM または別のリソースマネージャーから受信したクロックの最大値を渡します。

-   各リソースマネージャーは、仮想クロック値をログストリームに書き込み、ロールバックまたは回復操作を実行するときにこれらの値を使用します。

これらの手順を実行すると、各トランザクションマネージャーオブジェクトの KTM ストアに格納されている仮想クロック値がほぼまたは完全に一致するようになります。 したがって、復旧操作によって KTM がログストリームを読み取る場合、またはロールバック操作によってリソースマネージャーがログストリームを読み取る場合、復旧またはロールバックは同期されたログストリームに基づきます。

### <a name="how-to-modify-virtual-clock-values"></a>バーチャルクロック値を変更する方法

リソースマネージャーは、 [**ZwpreZwRollbackComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntprepreparecomplete)、 [**zw**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntpreparecomplete)complete、 [**zwcommitcomplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommitcomplete)、 [](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrollbackcomplete)、 [**ZwReadOnlyEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntreadonlyenlistment)、または[**ZwSinglePhaseReject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntsinglephasereject)に新しい値を渡すことによって、仮想クロックの値を変更できます。

[上位トランザクションマネージャー](creating-a-superior-transaction-manager.md)は、 [**ZwpreZwReadOnlyEnlistment 参加リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntpreprepareenlistment)、 [**zw 参加**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntprepareenlistment)リスト、zwcommit参加リスト、または[](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommitenlistment) [](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntreadonlyenlistment)に新しい値を渡すことによって、仮想クロックの値を変更できます。

また、 [**ResourceManagerNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-ptm_rm_notification)コールバックルーチンを使用する resource manager または上位トランザクションマネージャーは、コールバックルーチンが受け取る仮想クロック値を変更できます。 次に、更新された値が KTM によって保存されます。

リソースマネージャーまたは上位のトランザクションマネージャーが新しいクロック値を KTM に渡すと、KTM は、現在のクロック値より大きい場合にのみ新しい値を保存します。 それ以外の場合、KTM は現在のクロック値を保持します。

リソースマネージャーと上位のトランザクションマネージャーは、 [**Zwqueryinformationtransactionmanager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntqueryinformationtransactionmanager)ルーチンを呼び出すことによって、トランザクションマネージャーオブジェクトの仮想クロック値を取得できます。

 

 




