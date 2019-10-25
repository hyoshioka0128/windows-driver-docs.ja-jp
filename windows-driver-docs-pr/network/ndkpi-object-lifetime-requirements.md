---
title: NDKPI オブジェクト有効期間要件
description: このセクションでは、NDKPI オブジェクトの有効期間の要件について説明します。
ms.assetid: 94993523-D0D7-441E-B95C-417800840BAC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 24af158942b2d42e86919f09f7a41c9091e099e7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831897"
---
# <a name="ndkpi-object-lifetime-requirements"></a>NDKPI オブジェクト有効期間要件


## <a name="how-ndk-objects-are-created-used-and-closed"></a>NDK オブジェクトの作成、使用、および終了のしくみ


NDK コンシューマーは、そのオブジェクトの NDK プロバイダーの create 関数を呼び出すことによって、NDK オブジェクトの作成要求を開始します。

コンシューマーが create 関数を呼び出すと、 *NdkCreateCompletion* ([*NDK\_FN\_作成\_完了*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_create_completion)) がパラメーターとして渡されます。

コンシューマーは、オブジェクトのディスパッチテーブルでプロバイダー関数を呼び出すことによってさまざまな要求を開始し、 *Ndkrequestcompletion* ([*NDK\_FN\_REQUEST\_completion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_request_completion)) の完了コールバックをパラメーターとして渡します。

オブジェクトが不要になった場合、コンシューマーは、プロバイダーの*Ndkcloseobject* ([*ndk\_FN\_close\_object*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_close_object)) 関数を呼び出して、オブジェクトのクローズ要求を開始し、 *NdkCloseCompletion* (ndk を渡します。[ *\_FN\_終了\_完了*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_close_completion)) コールバックをパラメーターとして指定します。

このようなすべての関数に対して、プロバイダーは、コンシューマーのコールバック関数を呼び出して要求を完了します。 この呼び出しは、プロバイダーが操作を完了した (たとえば、オブジェクトを終了する) ことをコンシューマーに示し、コンシューマーに制御を返します。

## <a name="the-rules-for-completion-callbacks"></a>完了コールバックの規則


プロバイダーがコンシューマーの要求でオブジェクトを作成した場合、プロバイダーは、コンシューマーの*NdkCreateCompletion*コールバックを呼び出して、オブジェクトが使用できる状態であることを示します。

コンシューマーは、最初のコールバックが返されるのを待たずに、同じオブジェクトの他のプロバイダー関数を呼び出すことができます。

コンシューマーは、オブジェクトのすべてのプロバイダー関数が返されるまで、オブジェクトの*Ndkcloseobject*関数を呼び出しません。

ただし、プロバイダー関数が完了要求を開始した場合、プロバイダー関数が返されていない場合でも、コンシューマーはその完了コールバック内から*Ndkcloseobject*を呼び出すことができます。

プロバイダー関数は、次のいずれかの方法で、コールバックから戻る前に完了要求を開始できます。

-   完了コールバックの直接呼び出し
-   別のスレッドへの完了要求をキューに置いています

プロバイダーは、完了要求を実行することで、実質的に制御をコンシューマーに返します。 プロバイダーは、プロバイダーが完了要求を開始した後で、いつでもオブジェクトを閉じることができることを前提としています。

**注意**   完了要求を開始した後、デッドロックを防止するために、プロバイダーは次のいずれかを実行する必要があります。

-   完了コールバックが戻るまで、オブジェクトに対して他の操作を実行しません。
-   プロバイダーがオブジェクトを完全にタッチする必要がある場合は、オブジェクトをそのまま保持するために必要な手段を取ります。

 

## <a name="example-consumer-provider-interaction"></a>例: コンシューマープロバイダーとの対話


次のシナリオを考えてみましょう。

1.  コンシューマーはコネクタ ([**ndk\_コネクタ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_connector)) を作成し、 *ndkconnect* ([*ndk\_FN\_CONNECT*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_connect)) を呼び出します。
2.  プロバイダーは接続要求を処理し、エラーが発生すると、 *Ndkconnect*呼び出しのコンテキストでコンシューマーの完了コールバックを呼び出します (内部実装の選択によってインラインエラーを返すのではありません)。
3.  *Ndkconnect*の呼び出しがまだコンシューマーに返されていない場合でも、コンシューマーはこの完了コールバックのコンテキストで*Ndkcloseobject*を呼び出します。

デッドロックを回避するには、プロバイダーは、手順 2 ( *Ndkconnect*呼び出し内で完了コールバックを開始した時点) の後にコネクタオブジェクトをタッチしないようにする必要があります。

## <a name="closing-antecedent-and-successor-objects"></a>継続元オブジェクトと後続オブジェクトを閉じる


コンシューマーが後続オブジェクトの*Ndkcloseobject*を呼び出す前に、プロバイダーが*ndkcloseobject*関数を呼び出して継続元オブジェクトを閉じるように準備する必要があります。 コンシューマーがこれを実行する場合、プロバイダーは次のことを行う必要があります。

-   プロバイダーは、すべての後続オブジェクトが閉じられるまで、継続元オブジェクトを閉じないようにする必要があります。つまり、プロバイダーは終了要求から保留中のステータス\_を返し、終了のために登録された*NdkCloseCompletion*関数を呼び出して完了する必要があります。要求) を終了します。
-   コンシューマーは、 *Ndkcloseobject*を呼び出した後に、継続元オブジェクトを使用しません。したがって、プロバイダーは、継続元オブジェクトでのその他のプロバイダー関数の失敗に対する処理を追加する必要はありません (ただし、これが選択されている場合もあります)。
-   プロバイダーは、不要な場合を除き、最後の後続のオブジェクトが閉じられるまで他の副作用を持たない単純な逆参照のような close 要求を処理する場合があります (必要な副作用がある、以下の NDK listener のクローズケースを参照してください)。

後続のオブジェクトの進行中のクローズ完了コールバックがプロバイダーに返される前に、プロバイダーは、( [**NDK\_アダプター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_adapter)のクローズ要求を含む) 継続元オブジェクトに対して close 要求を完了することはできません。 これは、NDK コンシューマーが安全にアンロードできるようにするためです。

NDK コンシューマーは、コンシューマーコールバック関数内から[**ndk\_アダプター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_adapter)オブジェクト (ブロッキング呼び出し) の*ndkcloseobject*を呼び出しません。

## <a name="closing-adapter-objects"></a>アダプターオブジェクトを閉じる


次のシナリオを考えてみましょう。

1.  コンシューマーは、完了キュー (CQ) オブジェクトで*Ndkcloseobject*を呼び出します。
2.  プロバイダーは状態\_PENDING を返し、後でコンシューマーの完了コールバックを呼び出します。
3.  この完了コールバック内では、NDK\_アダプターを閉じることができるようになったことを示すイベントがコンシューマーから通知されます。
4.  別のスレッドがこの信号によってウェイクアップされ、 [**NDK\_アダプター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_adapter)を閉じ、アンロードに進みます。
5.  ただし、コンシューマーの CQ close 完了コールバックが呼び出されたスレッドが、コンシューマーのコールバック関数 (たとえば、関数[エピローグ](https://docs.microsoft.com/cpp/build/prolog-and-epilog)) の内部にある可能性があるため、コンシューマードライバーのアンロードは安全ではありません。
6.  完了コールバックコンテキストは、コンシューマーがイベントを通知できる唯一のコンテキストであるため、コンシューマードライバーは、セーフアンロードの問題自体を解決できません。

すべてのコールバックがコントロールを返したことをコンシューマーが確実に保証できるポイントが必要です。 NDKPI では、このポイントは[**NDK\_アダプター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_adapter)のクローズ要求が制御を返す場合になります。 **NDK\_アダプター**の終了要求はブロック呼び出しであることに注意してください。 **Ndk\_アダプター**のクローズ要求が返されたときに、その**ndk\_アダプター**オブジェクトからのすべてのオブジェクトのすべてのコールバックがプロバイダーに制御を返したことが保証されます。

## <a name="completing-close-requests"></a>終了要求の完了


プロバイダーは、次のまでオブジェクトに対して close 要求を完了することはできません。

-   オブジェクトに対するすべての保留中の非同期要求が完了しました (つまり、完了コールバックがプロバイダーに返されます)。
-   すべてのコンシューマーのイベントコールバック (たとえば、 *NdkCqNotificationCallback* ([*ndk\_fn\_CQ\_NOTIFICATION\_CALLBACK*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_cq_notification_callback)) On CQ、 *NDKCONNECTEVENTCALLBACK* ([*ndk\_FN\_リスナーの接続\_イベント\_コールバック*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_connect_event_callback)) がプロバイダーに返されます。

プロバイダーは、クローズ完了コールバックが呼び出された後、またはクローズ要求によってステータス\_成功が返された後にコールバックが発生しないことを保証する必要があります。 クローズ要求では、保留中の非同期要求のフラッシュまたはキャンセルも開始する必要があることに注意してください。

ここでは、NDK コンシューマーがコンシューマーコールバック関数内から[**ndk\_アダプター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_adapter)オブジェクト (ブロッキング呼び出し) の*ndkcloseobject*を呼び出すことができないと**いうことを**、論理的に  ます。

 

## <a name="related-topics"></a>関連トピック


[ネットワークダイレクトカーネルプロバイダーインターフェイス (NDKPI)](network-direct-kernel-programming-interface--ndkpi-.md)

 

 






