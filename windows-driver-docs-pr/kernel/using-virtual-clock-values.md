---
title: 仮想クロック値の使用
description: 仮想クロック値の使用
ms.assetid: de01b0f1-86b1-4e7d-af22-84dbbe3a3f83
keywords:
- 仮想のクロック値 WDK KTM
- カーネル トランザクション マネージャ WDK、仮想のクロック値
- KTM WDK、仮想のクロック値
- トランザクション WDK KTM、仮想のクロック値
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 451719c34ad3abd491a4f370cbce920284fa6910
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372188"
---
# <a name="using-virtual-clock-values"></a>仮想クロック値の使用


KTM では、トランザクション マネージャーの各オブジェクトに対して仮想クロックを提供します。 リソース マネージャーを呼び出すと[ **ZwCreateTransactionManager**](https://msdn.microsoft.com/library/windows/hardware/ff566430)KTM では、仮想のクロックにオブジェクトの値を 1 に設定します。 KTM では、コミット操作を開始するたびに仮想のクロックの値をインクリメントします。 KTM では、そのログ ストリームに書き込み、たびにログ レコードで仮想のクロックの現在の値が含まれます。

リソース マネージャーを呼び出すと[ **ZwRecoverTransactionManager**](https://msdn.microsoft.com/library/windows/hardware/ff567079)KTM にログ ストリームの記録、ストリームの末尾までが読み取られ、最後の値をトランザクション マネージャー オブジェクトの仮想のクロックの値を設定、オブジェクトのログ ストリームでその it を検索します。

リソース マネージャーを呼び出すと[ **ZwRollforwardTransactionManager**](https://msdn.microsoft.com/library/windows/hardware/ff567089)KTM は指定されたクロックの値、最大ストリーム レコード ログを読み取り、トランザクション マネージャー オブジェクトの仮想のクロックの値が設定クロックの値を指定します。

Ktm をトランザクション マネージャー オブジェクトの仮想のクロックの値を変更するには、リソース マネージャーおよび優先的なトランザクション マネージャーが、通常がない時刻の値を変更します。

### <a name="when-to-modify-virtual-clock-values"></a>仮想のクロックの値を変更するタイミング

通常、トランザクション処理システム (TPS) は、TP では、コンポーネントが複数のログ ストリームを同期しよう場合を除き、仮想の時刻値を変更する必要はありません。

たとえば、前-prepare/準備/コミットのシーケンス中に相互通信する複数のリソース マネージャーが、TP に含まれているとします。 また、各リソース マネージャーが一意のログ ストリームを持つトランザクション マネージャー オブジェクトを作成するとします。 KTM が、回復操作中に同じポイントにすべてのリソース マネージャーの状態を復元することを確認するには、これらのリソース マネージャーは、次の手順を使用可能性があります。

-   いずれかの KTM から受信した最新の仮想のクロック値を渡す 1 つのリソース マネージャーが別の通信を行うとき別またはリソース マネージャー。

-   リソース マネージャーが仮想のクロックの値を受け取る KTM ルーチンを呼び出すたびに (このトピックでは、次のセクションを参照)、KTM または別のリソース マネージャーから受信した最上位のクロックの値を渡します。

-   各 resource manager では、仮想の時刻値をそのログ ストリームに書き込み、ロールバックや回復操作の実行時に、これらの値を使用します。

次の手順を各トランザクション マネージャー オブジェクトがほぼ KTM を格納する仮想クロック値またはと正確に一致します。 そのため、回復操作、KTM をそのログ ストリームを読み取る場合、またはロールバック操作により、リソース マネージャーのログ ストリームの読み取りを復元またはロールバックは同期のログ ストリームに基づいています。

### <a name="how-to-modify-virtual-clock-values"></a>仮想の時刻値を変更する方法

リソース マネージャーは、新しい値を渡すことによって仮想クロックの値を変更できます[ **ZwPrePrepareComplete**](https://msdn.microsoft.com/library/windows/hardware/ff567040)、 [ **ZwPrepareComplete**](https://msdn.microsoft.com/library/windows/hardware/ff567037)、[ **ZwCommitComplete**](https://msdn.microsoft.com/library/windows/hardware/ff566418)、 [ **ZwRollbackComplete**](https://msdn.microsoft.com/library/windows/hardware/ff567081)、 [ **ZwReadOnlyEnlistment**](https://msdn.microsoft.com/library/windows/hardware/ff567074)、または[ **ZwSinglePhaseReject**](https://msdn.microsoft.com/library/windows/hardware/ff567113)します。

[優先的なトランザクション マネージャー](creating-a-superior-transaction-manager.md)に新しい値を渡すことによって仮想クロックの値を変更できます[ **ZwPrePrepareEnlistment**](https://msdn.microsoft.com/library/windows/hardware/ff567044)、 [ **ZwPrepareEnlistment** ](https://msdn.microsoft.com/library/windows/hardware/ff567039)、 [ **ZwCommitEnlistment**](https://msdn.microsoft.com/library/windows/hardware/ff566419)、または[ **ZwReadOnlyEnlistment**](https://msdn.microsoft.com/library/windows/hardware/ff567074)します。

さらに、resource manager または優先的なトランザクション マネージャーを使用する、 [ **ResourceManagerNotification** ](https://msdn.microsoft.com/library/windows/hardware/ff561077)コールバック ルーチンは、コールバック ルーチンを受け取る仮想クロック値を変更できます。 KTM では、更新された値が保存されます。

Resource manager または優先的なトランザクション マネージャーは、新しいクロックの値を KTM に合格した場合、KTM は、クロックの現在の値より大きい場合にのみ、新しい値を保存します。 それ以外の場合、KTM は、クロックの現在の値を保持します。

リソース マネージャーおよび優先的なトランザクション マネージャー値を取得できます、トランザクション マネージャー オブジェクトの仮想のクロックを呼び出して、 [ **ZwQueryInformationTransactionManager** ](https://msdn.microsoft.com/library/windows/hardware/ff567058)ルーチン。

 

 




