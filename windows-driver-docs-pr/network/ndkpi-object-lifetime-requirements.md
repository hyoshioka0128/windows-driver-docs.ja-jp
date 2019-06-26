---
title: NDKPI オブジェクト有効期間要件
description: このセクションでは、NDKPI オブジェクトの有効期間の要件を説明します。
ms.assetid: 94993523-D0D7-441E-B95C-417800840BAC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7c382c56af12e56e48c54033d9414b4be82bc18
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364038"
---
# <a name="ndkpi-object-lifetime-requirements"></a>NDKPI オブジェクト有効期間要件


## <a name="how-ndk-objects-are-created-used-and-closed"></a>NDK オブジェクトを作成、使用、および終了する方法


NDK コンシューマーでは、そのオブジェクトに対して、NDK プロバイダーの作成関数を呼び出すことによって NDK オブジェクトの作成要求を開始します。

コンシューマーが作成する関数を呼び出す際に渡して、 *NdkCreateCompletion* ([*NDK\_FN\_作成\_完了*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_create_completion)) をパラメーターとして。

コンシューマーでは、さまざまな要求を開始オブジェクトのディスパッチ テーブルを渡すことで、プロバイダーの関数を呼び出すことによって、 *NdkRequestCompletion* ([*NDK\_FN\_要求\_完了*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_request_completion)) をパラメーターとして完了コールバック。

コンシューマーがプロバイダーを呼び出してオブジェクトを不要になったとき*NdkCloseObject* ([*NDK\_FN\_閉じる\_オブジェクト*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_close_object)) 関数に渡して、オブジェクトの終了要求を開始、 *NdkCloseCompletion* ([*NDK\_FN\_閉じます\_完了*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_close_completion)) をパラメーターとしてコールバック。

このようなすべての関数は、プロバイダーは、要求を完了するコンシューマーのコールバック関数を呼び出します。 この呼び出しは、プロバイダーが (たとえば、オブジェクトを閉じる)、操作が完了し、コンシューマーに制御を返すことに、コンシューマーを示します。

## <a name="the-rules-for-completion-callbacks"></a>完了コールバックの規則


プロバイダーがコンシューマーを呼び出して、プロバイダーがコンシューマーの要求でオブジェクトを作成、 *NdkCreateCompletion*コールバック オブジェクトが使用できる状態であることを示します。

コンシューマーを返す最初のコールバックを待つことがなく、同じオブジェクトに対して他のプロバイダーの関数を呼び出すことができます。

コンシューマーは呼び出しません、 *NdkCloseObject*そのオブジェクトのすべてのプロバイダーの関数が返されるまで、オブジェクトの関数。

ただし、プロバイダー関数は、完了要求を開始する場合、コンシューマーは、自由に呼び出す*NdkCloseObject*からその完了コールバック内でも、provider 関数が返された場合。

プロバイダーの関数は、次のいずれかの手順を実行して、コールバックから戻る前に完了要求を開始できます。

-   完了コールバックの直接呼び出し
-   別のスレッドに完了要求のキュー

実質的に、プロバイダーは完了要求を開始することによって、コンシューマーにコントロールを返します。 プロバイダーでは、オブジェクトは、プロバイダーが、完了要求が開始した後、いつでも閉じることができますと仮定する必要があります。

**注**  完了要求を開始した後は、デッドロックを防ぐため、プロバイダーはありますか。

-   完了コールバックが戻るされるまでは、オブジェクトの他の操作を実行しません。
-   オブジェクトを維持するために必要なメジャーがかかる場合は、プロバイダーは絶対にオブジェクトをタッチする必要があります。

 

## <a name="example-consumer-provider-interaction"></a>以下に例を示します。コンシューマー プロバイダーの操作


次のシナリオを考えてみましょう。

1.  コンシューマーがコネクタを作成します ([**NDK\_コネクタ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_connector)) を呼び出して、 *NdkConnect* ([*NDK\_FN\_CONNECT*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_connect))。
2.  プロバイダー接続要求を処理、ヒット、障害およびのコンテキストでは、コンシューマーの完了時のコールバックを呼び出し、 *NdkConnect* (内部の実装を選択するためのインライン エラーを返す) ではなく呼び出し。
3.  コンシューマーは*NdkCloseObject*この完了コールバックのコンテキストで場合でも、 *NdkConnect*呼び出しがまだコンシューマーに返されません。

プロバイダーのデッドロックを回避するコネクタ オブジェクトが 2 の手順の後に接触する必要があります (内で完了コールバックが開始したときに、ポイント、 *NdkConnect*呼び出します)。

## <a name="closing-antecedent-and-successor-objects"></a>継続元と後続のオブジェクトを閉じる


呼び出すコンシューマー、プロバイダーを準備する必要があります、 *NdkCloseObject*コンシューマー呼び出される前に継続元のオブジェクトを閉じる関数*NdkCloseObject*の後続のオブジェクト。 場合は、コンシューマーは、次のプロバイダーが行う必要がありますに示します。

-   つまり後続のすべてのオブジェクトが閉じられるまで、プロバイダーは、継続元のオブジェクトを閉じていない必要があります、プロバイダーは、状態を返す必要があります\_終了からの保留要求し、実行する (を呼び出して、登録済み*NdkCloseCompletion*終了要求の関数) 後続のすべてのオブジェクトが閉じられるとします。
-   コンシューマーが呼び出した後、継続元のオブジェクトを使用しない*NdkCloseObject*そのため、プロバイダーは、継続元のオブジェクトにさらにプロバイダーの関数が失敗したため、処理を追加する必要はありません (ただしを選択した場合ことがあります)。
-   プロバイダーが影響を与えません他側 - 最後の後続のオブジェクトが閉じられるまでそれ以外の場合 (下 NDK リスナー閉じる場合は必要な副作用を参照) に必要な場合を除き、逆参照する、単純なように終了要求を扱うことがあります。

プロバイダーは継続元のオブジェクトを閉じる要求を完了する必要があります (など、 [ **NDK\_アダプター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_adapter)終了要求) の後継で、実行中のクローズ完了コールバックの前にオブジェクトは、プロバイダーを返します。 これは、NDK コンシューマーを安全にアンロードを許可します。

NDK コンシューマーを呼び出しません*NdkCloseObject*の[ **NDK\_アダプター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_adapter) (ブロッキング呼び出し) オブジェクトから、コンシューマーのコールバック関数内で。

## <a name="closing-adapter-objects"></a>アダプター オブジェクトを閉じる


次のシナリオを考えてみましょう。

1.  コンシューマーは*NdkCloseObject*完了キュー (CQ) オブジェクト。
2.  プロバイダーが返すステータス\_保留中、およびそれ以降は、コンシューマーの完了時のコールバックを呼び出します。
3.  この完了コールバック内でコンシューマー信号イベントがこれで、NDK を閉じるには、[ok]\_アダプター。
4.  別のスレッドによってこのシグナルは、アクティブになり、終了、 [ **NDK\_アダプター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_adapter)アンロードに進みます。
5.  コンシューマーの CQ クローズ完了コールバックが呼び出されたスレッドが、コンシューマーのコールバック関数内にあるただし、(たとえば、関数[エピローグ](https://docs.microsoft.com/cpp/build/prolog-and-epilog)) コンシューマー ドライバーをアンロードしても安全でないため、します。
6.  完了コールバック コンテキストがのみのコンテキストであるために、コンシューマーはコンシューマー ドライバーが自体セーフ アンロードの問題を解決できません、イベントで通知できます。

位置、コンシューマー保証するすべてのコールバックのコントロールを返しますが、ポイントが必要があります。 この点では、NDKPI では場合にクローズ要求を[ **NDK\_アダプター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_adapter)コントロールを返します。 なお**NDK\_アダプター**終了要求は、ブロック呼び出しです。 ときに、 **NDK\_アダプター**を閉じる要求を返しますから降下するすべてのオブジェクトに対するすべてのコールバックが保証されます**NDK\_アダプター**オブジェクトにコントロールが返されますが、プロバイダー。

## <a name="completing-close-requests"></a>閉じる要求を完了します。


プロバイダーでは、までオブジェクトを閉じる要求を完了する必要がありますできません。

-   保留中のオブジェクトの非同期要求がすべて完了 (つまり、完了コールバックが返されるをプロバイダーに)。
-   すべてのコンシューマーのイベントのコールバック (たとえば、 *NdkCqNotificationCallback* ([*NDK\_FN\_CQ\_通知\_コールバック*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_cq_notification_callback))、CQ は、 *NdkConnectEventCallback* ([*NDK\_FN\_CONNECT\_イベント\_コールバック* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_connect_event_callback)) リスナーで) が、プロバイダーに返されます。

プロバイダーがクローズ完了コールバックが呼び出された後、または閉じる要求に状態が返された後にない複数のコールバックが発生することを保証する必要があります\_成功します。 終了要求ではフラッシュの必要なまたは保留中の非同期要求のキャンセルを開始する必要がありますもことに注意してください。

**注**  論理的に従い、上記、NDK コンシューマーを呼び出してはならないこと*NdkCloseObject*の[ **NDK\_アダプター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_adapter)(ブロッキング呼び出し) オブジェクトから、コンシューマーのコールバック関数内で。

 

## <a name="related-topics"></a>関連トピック


[ネットワーク ダイレクト カーネル プロバイダー インターフェイス (NDKPI)](network-direct-kernel-programming-interface--ndkpi-.md)

 

 






