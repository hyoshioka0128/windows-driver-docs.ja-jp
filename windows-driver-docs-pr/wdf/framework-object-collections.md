---
title: フレームワーク オブジェクトのコレクション
description: フレームワーク オブジェクトのコレクション
ms.assetid: e3f29be6-ee4c-487a-8c85-18be8b6a5cdc
keywords:
- フレームワークオブジェクト WDK KMDF、コレクション
- コレクション WDK KMDF
- フレームワークコレクションオブジェクト WDK KMDF
- オブジェクトコレクション WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15ead2c00ce24a40be79a1d988ac4c32c931f34a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823701"
---
# <a name="framework-object-collections"></a>フレームワーク オブジェクトのコレクション





ドライバーは、フレームワーク*コレクションオブジェクト*によって表されるコレクションに framework オブジェクトをグループ化できます。

たとえば、大量の i/o 要求を表すフレームワーク要求オブジェクトをドライバーが受け取った場合、ドライバーは、大量の要求を、 [i/o ターゲット](using-i-o-targets.md)に送信できる小さな要求に分割することが必要になる場合があります。 大きい要求を小さいものに分割するには、ドライバーは小さい要求を表す一連の要求オブジェクトを作成する必要があります。 ドライバーによって作成された要求オブジェクトを追跡するために、ドライバーはコレクションオブジェクトを作成し、コレクションに追加することがあります。

通常、オブジェクトコレクション内のオブジェクトは、単一の種類のフレームワークオブジェクトで構成されますが、ドライバーは、さまざまな種類のオブジェクトで構成されるコレクションを作成できます。

また、ドライバーはコレクションのコレクションを作成することもできます。 つまり、コレクションはコレクションオブジェクトのセットで構成されます。

フレームワークベースのドライバーは、オブジェクトコレクションに対して次の操作を実行できます。

-   コレクションオブジェクトを作成します。

    新しいコレクションを作成するために、ドライバーは[**Wdfcollectioncreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcollection/nf-wdfcollection-wdfcollectioncreate)を呼び出すことができます。

-   オブジェクトをコレクションに追加します。

    オブジェクトをコレクションに追加するために、ドライバーは[**Wdfcollectionadd**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcollection/nf-wdfcollection-wdfcollectionadd)を1回以上呼び出すことができます。 **Wdfcollectionadd**を呼び出すたびに、オブジェクトがコレクションの末尾に追加され、追加されたオブジェクトの参照カウントがインクリメントされます。

-   オブジェクトをコレクションから削除します。

    コレクションからオブジェクトを削除し、その参照カウントをデクリメントするために、ドライバーは[**wdfcollectionremove**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcollection/nf-wdfcollection-wdfcollectionremove)または[**Wdfcollectionremoveitem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcollection/nf-wdfcollection-wdfcollectionremoveitem)を呼び出すことができます。 オブジェクトが削除されると、削除されたオブジェクトの後にあるすべてのオブジェクトのインデックスが自動的にデクリメントされます。

-   コレクション内のオブジェクトの数を取得します。

    コレクションに含まれるオブジェクトの数を確認するために、ドライバーは[**WdfCollectionGetCount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcollection/nf-wdfcollection-wdfcollectiongetcount)を呼び出すことができます。

-   コレクション内のオブジェクトへのハンドルを取得します。

    ドライバーが[**Wdfcollectiongetitem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcollection/nf-wdfcollection-wdfcollectiongetitem)を呼び出して、入力引数としてインデックス値を指定した場合、ドライバーは、インデックス値に関連付けられているオブジェクトへのハンドルを受け取ります。 (インデックス値が0の場合は、コレクション内の最初のオブジェクト、1のインデックス値が2番目のオブジェクトを表します。同様に、リンクリストのようになります。 ドライバーがコレクションから項目*i*を削除すると、item *i*+ 1 が item *i*になります)。

    ドライバーは、 [**Wdfcollectiongetfirstitem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcollection/nf-wdfcollection-wdfcollectiongetfirstitem)または[**Wdfcollectiongetfirstitem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcollection/nf-wdfcollection-wdfcollectiongetlastitem)を呼び出して、コレクションに追加された最初または最後の項目へのハンドルを取得することもできます。

-   コレクションをロックします。

    ドライバーは、 [**Wdfwaitlockacquire**](https://msdn.microsoft.com/library/windows/hardware/ff551168)を呼び出して、IRQL = パッシブ\_レベルのコレクションへのアクセスを同期するか、IRQL = DISPATCH\_Level で[**WdfSpinLockAcquire**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550040(v=vs.85)) synchronize アクセスを呼び出すことができます。 ドライバーがロックを取得した後、このコレクションには、 **Wdfwaitlockacquire**または**WdfSpinLockAcquire**も呼び出すドライバー内の他のコードからアクセスすることはできません。 コレクションに対して操作を完了した後、ドライバーは[**Wdfwaitlockrelease**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfsync/nf-wdfsync-wdfwaitlockrelease)を呼び出す必要があります。

    [**Wdfwaitlockacquire**](https://msdn.microsoft.com/library/windows/hardware/ff551168)または[**WdfSpinLockAcquire**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550040(v=vs.85))を呼び出しても、他のコードが**Wdfwaitlockacquire**または**WdfSpinLockAcquire**を呼び出さない場合、ドライバー内の他のコードがコレクションに同時にアクセスするのを防ぐことはできません。

-   コレクションを削除します。

    コレクションオブジェクトを削除するために、ドライバーは[**Wdfobjectdelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)を呼び出すことができます。 ただし、通常は、コレクションを作成するときにドライバーが親オブジェクトを指定し、親オブジェクトを削除するときに、フレームワークによってコレクションオブジェクトが削除されます。

    たとえば、大量の i/o 要求を小さい要求に分割できるように、ドライバーが要求オブジェクトのセットを作成する場合、サイズの大きい i/o 要求の要求オブジェクトをコレクションオブジェクトの親オブジェクトにすることができます。 最終的に、ドライバーの i/o ターゲットは、小さい要求を完了するために[**Wdfrequestcomplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)を呼び出します。 この時点で、ドライバーは大きな i/o 要求に対して**Wdfrequestcomplete**を呼び出すことができます。これにより、フレームワークは、要求オブジェクトとその子オブジェクトを削除します。コレクションオブジェクト。

    フレームワークは、削除されていないオブジェクトを含むコレクションオブジェクトを削除すると、そのオブジェクトをコレクションから削除し、参照カウントをデクリメントしますが、コレクションオブジェクトのみを削除します。

場合によっては、ドライバーがコレクション内のすべてのオブジェクトを調べる必要があります。 この状況を示すコード例を次に示します。

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

 

 





