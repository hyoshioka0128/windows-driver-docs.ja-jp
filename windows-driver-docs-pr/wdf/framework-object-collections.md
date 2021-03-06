---
title: フレームワーク オブジェクトのコレクション
description: フレームワーク オブジェクトのコレクション
ms.assetid: e3f29be6-ee4c-487a-8c85-18be8b6a5cdc
keywords:
- framework は、WDK KMDF、コレクションをオブジェクトします。
- WDK KMDF のコレクション
- framework のコレクション オブジェクト WDK KMDF
- オブジェクトのコレクション WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9021fce6e571bc110c4965eeb885d6d99ba480ae
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384462"
---
# <a name="framework-object-collections"></a>フレームワーク オブジェクトのコレクション





ドライバーは、framework のオブジェクトをグループ化によって表されるコレクションに*framework のコレクション オブジェクト*します。

たとえば、ドライバーは、大規模な I/O 要求を表す framework 要求オブジェクトを受信する場合、ドライバーに送信できる小規模の要求に、大きな要求を分割する必要があります、 [I/O ターゲット](using-i-o-targets.md)します。 大きな要求を細かく分割、ドライバーは、一連の小さな要求を表す要求オブジェクトを作成する必要があります。 これらのドライバーが作成した要求オブジェクトを追跡するのには、ドライバー可能性がありますコレクション オブジェクトを作成し、コレクションに追加します。

通常、framework のオブジェクトの 1 つの型のオブジェクトのコレクション内のオブジェクトで構成されますが、ドライバーは、さまざまな種類のオブジェクトで構成されるコレクションを作成できます。

ドライバーは、コレクションのコレクションを作成することもできます。 つまり、コレクションは、一連のコレクション オブジェクトで構成できます。

フレームワーク ベースのドライバーでは、オブジェクトのコレクションでは、次の操作を実行できます。

-   コレクション オブジェクトを作成します。

    新しいコレクションを作成するドライバーを呼び出すことができます[ **WdfCollectionCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfcollection/nf-wdfcollection-wdfcollectioncreate)します。

-   オブジェクトをコレクションに追加します。

    オブジェクトをコレクションに追加するドライバーを呼び出すことができます[ **WdfCollectionAdd**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfcollection/nf-wdfcollection-wdfcollectionadd)、1 つまたは複数の時刻。 呼び出しごとに**WdfCollectionAdd**コレクションの末尾にオブジェクトを追加し、追加されたオブジェクトの参照カウントをインクリメントします。

-   オブジェクトをコレクションから削除します。

    ドライバーを呼び出すことができますをコレクションからオブジェクトを削除し、その参照カウントをデクリメント、 [ **WdfCollectionRemove** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfcollection/nf-wdfcollection-wdfcollectionremove)または[ **WdfCollectionRemoveItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfcollection/nf-wdfcollection-wdfcollectionremoveitem). オブジェクトが削除されると、削除された後にすべてのオブジェクトは、インデックスを自動的にデクリメントがあります。

-   コレクション内のオブジェクトの数を取得します。

    コレクションが含まれているオブジェクトの数を決定するには、ドライバーを呼び出すことができます[ **WdfCollectionGetCount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfcollection/nf-wdfcollection-wdfcollectiongetcount)します。

-   コレクション内のオブジェクトを識別するハンドルを取得します。

    ドライバーを呼び出す場合[ **WdfCollectionGetItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfcollection/nf-wdfcollection-wdfcollectiongetitem)、入力引数としてインデックス値を指定するには、ドライバーが、インデックス値に関連付けられているオブジェクトを識別するハンドルを受信します。 (コレクションの最初のオブジェクトを表すインデックス値は 0、1 つのインデックス値を表す 2 つ目のオブジェクト、およびリンク リストなどのようになってします。 ときに項目、ドライバーを削除します*は*、コレクションから項目*は*項目になります +1*は*)。

    ドライバーを呼び出すことも[ **WdfCollectionGetFirstItem** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfcollection/nf-wdfcollection-wdfcollectiongetfirstitem)または[ **WdfCollectionGetLastItem** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfcollection/nf-wdfcollection-wdfcollectiongetlastitem)最初と最後の項目を識別するハンドルを取得するにはコレクションに追加されました。

-   コレクションをロックします。

    ドライバーを呼び出すことができます[ **WdfWaitLockAcquire** ](https://msdn.microsoft.com/library/windows/hardware/ff551168)アクセスを同期する IRQL でコレクションに = パッシブ\_レベル、またはそれが呼び出すことができます[ **WdfSpinLockAcquire**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550040(v=vs.85))のアクセスを同期 IRQL = ディスパッチ\_レベル。 呼び出すことも、ドライバーでは、他のコードでコレクションにアクセスすることはできません後、ドライバーは、ロックを取得する**WdfWaitLockAcquire**または**WdfSpinLockAcquire**します。 コレクションに対する操作を完了すると、ドライバーを呼び出す必要があります[ **WdfWaitLockRelease**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfsync/nf-wdfsync-wdfwaitlockrelease)します。

    呼び出す[ **WdfWaitLockAcquire** ](https://msdn.microsoft.com/library/windows/hardware/ff551168)または[ **WdfSpinLockAcquire** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550040(v=vs.85))同時に、ドライバーからの他のコードを妨げませんその他のコードにも要求されていない場合、コレクションにアクセスする**WdfWaitLockAcquire**または**WdfSpinLockAcquire**します。

-   コレクションを削除します。

    コレクション オブジェクトを削除するドライバーを呼び出すことができます[ **WdfObjectDelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectdelete)します。 一般的には、ただし、ドライバーを指定、親オブジェクト、コレクションを作成すると、フレームワークは、親オブジェクトを削除するときにコレクション オブジェクトを削除します。

    たとえば、ドライバーは、小さな要求に大規模な I/O 要求を中断にするように一連の要求オブジェクトを作成する場合は、オブジェクトのコレクション オブジェクトの親オブジェクト、大規模な I/O 要求の要求を行う、ことができます。 最終的に、ドライバーの I/O ターゲットを呼び出す[ **WdfRequestComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcomplete)小さな要求を完了します。 ドライバーがその時点で呼び出すことができます**WdfRequestComplete**大きなの I/O 要求の要求オブジェクトとその子オブジェクトを削除するためにフレームワークの原因: コレクション オブジェクト。

    含むコレクション オブジェクトをオブジェクトが削除されていないフレームワークの削除、フレームワークからのオブジェクトを削除しますが、デクリメント、コレクションの参照がカウント、コレクション オブジェクトのみを削除します。

場合があります、ドライバーでは、コレクション内のオブジェクトのすべてを調べる必要があります。 次のコード例では、このような状況を示しています。

```cpp
WdfWaitLockAcquire(CollectionLockHandle, NULL);
ItemCount = WdfCollectionGetCount(CollectionHandle);
for (i=0; i<ItemCount; i++) {
    ObjectHandle = WdfCollectionGetItem(CollectionHandle, i);
    // 1. Call object-specific methods to obtain object properties.
    // 2. Perform object-specific operations.
    }
WdfWaitLockRelease(CollectionLockHandle);
```

 

 





