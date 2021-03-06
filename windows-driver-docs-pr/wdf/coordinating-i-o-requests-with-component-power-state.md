---
title: コンポーネントの電源状態での I/O 要求の調整
description: コンポーネントの電源状態での I/O 要求の調整
ms.assetid: CF74B946-BF62-481A-B8AA-DD106DDB94CA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 758124bb7fea4b017a0da143d59f4327b26ad783
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382411"
---
# <a name="coordinating-io-requests-with-component-power-state"></a>コンポーネントの電源状態での I/O 要求の調整


\[KMDF にのみ適用されます。\]

複数コンポーネントのデバイスの KMDF ドライバーでは、アクティブな状態にあるコンポーネントに要求を送信する必要がありますのみです。 通常、ドライバーは、コンポーネントまたはコンポーネントのセットへの I/O キューを割り当てます。

まず、1 つのコンポーネントに割り当てられているキューも検討してください。 ドライバーは、コンポーネントがアクティブになり、コンポーネントがアイドル状態になったときに、キューを停止するときに、キューを起動します。 そのため、KMDF がキューの要求ハンドラーを呼び出すときに、デバイスが完全に入った (D0) の状態、および必須コンポーネントがアクティブです。 要求ハンドラーは、コンポーネントのハードウェアを安全にアクセスできます。

同じ概念は、一連のコンポーネントに割り当てられているキューに適用されます。 この場合、ドライバーは、アクティブなすべてのコンポーネント セットの場合、キューを開始します。 コンポーネントのいずれかがアイドル状態になったときに、ドライバーは、キューを停止します。

このトピックでは、複数コンポーネントのデバイスの KMDF ドライバーがさまざまなコンポーネントの組み合わせを必要とする複数の要求の種類に関連する状況でこのようなサポートを実装可能性がある方法について説明します。

## <a name="example"></a>例


ドライバーでサポートされている要求の種類に必要なコンポーネントを特定します。 たとえば、3 つのコンポーネントを持つデバイスがあるとします。0、1 および 2、ドライバーが次の 3 つの種類の要求を受信します。A、B、および C要求のコンポーネントの要件は次のとおりです。

| 要求の種類 | 必要なコンポーネント |
|--------------|-------------------|
| A            | 0,2               |
| B            | 1                 |
| C            | 0,1,2             |

 

この例では、要求の種類ごとに 1 つのコンポーネントの 3 つの異なるセットがあります。
1 つの既定、デバイスの I/O キューの電源管理対象に加えて 1 つ追加電源管理対象のキュー コンポーネントの各セットに対応するドライバーが用意されています。 上記の例では、ドライバーは、1 つのプライマリ キューと各コンポーネントのセットに対応する 1 つ、3 つのセカンダリ キューを作成します。 このキューの構成は、次の図に示されます。

![コンポーネントの複数のデバイスのキューの実装](images/multicompqueues.png)

ドライバーは、各コンポーネントのセットに対応するビットマスクを保持します。 ビットマスクの各ビットは、コンポーネントの 1 つのアクティブまたはアイドル状態を表します。 ビットが設定されている場合、コンポーネントはアクティブです。 ビットがオフの場合、コンポーネントがアイドル状態にします。

要求が到着すると、[要求ハンドラー](request-handlers.md)要求が必要があるあり、呼び出しの最上位レベルのキュー コンポーネントを決定します[ **PoFxActivateComponent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxactivatecomponent)ごと。 要求ハンドラーは、そのコンポーネントのセットに対応するセカンダリの I/O キューに要求を転送します。

コンポーネントがアクティブになった、電源管理フレームワーク (PoFx) 呼び出し、ドライバーの[ *ComponentActiveConditionCallback* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_component_active_condition_callback)ルーチン。 このコールバックは、ドライバーは、そのコンポーネントが表される各ビットマスク内の指定したコンポーネントに対応するビットを設定します。 すべての指定されたビットマスクのビットを設定すると、すべてのセットの対応するコンポーネントはアクティブです。 ドライバーの呼び出しは完全にアクティブな各コンポーネント セット、 [ **WdfIoQueueStart** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuestart)を対応するセカンダリ I/O キューを開始します。

たとえば、上記の仮想デバイスを検討してください。 1 と 2 のコンポーネントがアイドル状態には、そのコンポーネントの 0 がアクティブであるとします。 PoFx にそのコンポーネントの呼び出しコンポーネント 2 がアクティブになると、 [ *ComponentActiveConditionCallback* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_component_active_condition_callback)ルーチン。 ドライバーは、これら 2 つの要求の種類のビットマスクを操作するために、タイプ A および C 使用コンポーネント 2 を要求します。 ドライバーが要求タイプ A のキューを開始するようになりましたが要求の種類に対応するビットマスク内のすべてのビットが設定されているのでただし、すべてのビットは要求の種類 C の設定 (コンポーネント 1 ではまだアイドル状態)。 ドライバーが要求の種類 C. のキューを開始できません。

セカンダリの I/O キューを開始すると、フレームワークは、キューに格納されている要求の配信を開始します。 [要求ハンドラー](request-handlers.md)セカンダリの I/O キューのドライバーが安全に要求を処理コンポーネントがアクティブで、電源の参照が、要求の各コンポーネントに取得されているためです。

ドライバーでは、要求の処理が完了したら、それを呼び出す[ **PoFxIdleComponent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxidlecomponent)の各コンポーネントを要求は、使用していたし、要求を完了します。 コンポーネントを使用して要求がある場合、電源のフレームワークが、ドライバーの[ *ComponentIdleConditionCallback* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_component_idle_condition_callback)ルーチン。

このコールバックで、そのコンポーネントが表される各ビットマスク内の指定したコンポーネントに対応するビットはクリアされます。 ドライバーを呼び出す場合、指定されたビットマスクは、コンポーネントがアイドル状態に遷移するセットの対応する 1 つ目であることを示します、 [ **WdfIoQueueStop** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuestop)対応するセカンダリ I/O を停止するにはキューです。 これにより、ドライバーにより、エントリのすべてのセットの対応するコンポーネントがアクティブでない場合、キューは要求がディスパッチされません。

上記の例では、もう一度考えてみましょう。 すべてのコンポーネントがアクティブしたがってすべてのキューを起動します。 PoFx を呼び出すコンポーネント 1 がアイドル状態になったときに、 [ *ComponentIdleConditionCallback* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_component_idle_condition_callback)コンポーネント 1 の日常的な。 このコールバックで、ドライバーはコンポーネント 1 を使用するために要求の種類 B と C のビットマスクを操作します。 コンポーネント 1 は、これら両方の要求の種類のアイドル状態になる最初のコンポーネントであるため、ドライバーが B と C の要求の種類のキューを停止します

この時点であるとする 0 のコンポーネントがアイドル状態になります。 [ *ComponentIdleConditionCallback* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_component_idle_condition_callback) 0、コンポーネントのドライバーが要求の種類、および c. のビットマスクを操作します。0 のコンポーネントが最初のコンポーネントのアイドル状態になるため、要求を入力 (コンポーネント 2 がアクティブなまま)、ドライバーは、A. タイプの要求のキューを停止します。ただし、要求の種類 C、0 のコンポーネントでないアイドル状態になる最初のコンポーネント。 ドライバーでは、要求の種類 C が (もしこれ以前) のキューは停止しません。

この例で説明した手法を使用するドライバーを登録する必要がありますも、 [ *EvtIoCanceledOnQueue* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_canceled_on_queue)セカンダリ キューごとのコールバック関数。 ドライバーがこのコールバックを使用して呼び出しを要求をセカンダリ キューの中にキャンセルできる場合は、 [ **PoFxIdleComponent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxidlecomponent)要素ごとに対応します。 要求ハンドラーが呼び出されたときにかかった power 参照をそのリリースに行う[ **PoFxActivateComponent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxactivatecomponent)セカンダリ キューに要求を転送する前にします。

 

 





