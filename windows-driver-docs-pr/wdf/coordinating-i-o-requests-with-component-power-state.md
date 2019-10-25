---
title: コンポーネントの電源状態での I/O 要求の調整
description: コンポーネントの電源状態での I/O 要求の調整
ms.assetid: CF74B946-BF62-481A-B8AA-DD106DDB94CA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1beb028b93983a500d92c875db09a0b758fedf2b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845621"
---
# <a name="coordinating-io-requests-with-component-power-state"></a>コンポーネントの電源状態での I/O 要求の調整


\[は KMDF にのみ適用され\]

複数コンポーネントのデバイス用の KMDF ドライバーは、アクティブな状態のコンポーネントにのみ要求を送信する必要があります。 通常、ドライバーはコンポーネントまたはコンポーネントのセットに i/o キューを割り当てます。

最初に1つのコンポーネントに割り当てられたキューを考えてみます。 コンポーネントがアクティブになると、ドライバーはキューを開始し、コンポーネントがアイドル状態になるとキューを停止します。 そのため、KMDF がキューの要求ハンドラーを呼び出すと、デバイスは完全に (D0) 状態になり、必要なコンポーネントがアクティブになります。 要求ハンドラーは、コンポーネントハードウェアに安全にアクセスできます。

同じ概念は、一連のコンポーネントに割り当てられたキューにも適用されます。 この場合、セット内のすべてのコンポーネントがアクティブになると、ドライバーによってキューが開始されます。 いずれかのコンポーネントがアイドル状態になると、ドライバーはキューを停止します。

このトピックでは、複数コンポーネントのデバイスの KMDF ドライバーが、コンポーネントのさまざまな組み合わせを必要とする複数の要求の種類に関連する状況で、このようなサポートを実装する方法について説明します。

## <a name="example"></a>例


ドライバーでサポートされている要求の種類ごとに、必要なコンポーネントを特定します。 たとえば、3つのコンポーネント (A、B、および C) を持つデバイスについて考えてみます。要求のコンポーネントの要件は次のようになっています。

| 要求の種類 | 必要なコンポーネント |
|--------------|-------------------|
| 確認が完了していないエイリアスの横には、            | 0、2               |
| B            | 1                 |
| C            | 0、1、2             |

 

この例では、要求の種類ごとに1つずつ、3つの異なるセットのコンポーネントがあります。
ドライバーは、デバイスに既定で1つの電源管理対象 i/o キューを提供します。さらに、各コンポーネントのセットに対応する1つの追加の電源管理キューも提供します。 上記の例では、ドライバーによって1つのプライマリキューと3つのセカンダリキューが作成されます。1つは各コンポーネントセットに対応します。 このキュー構成を次の図に示します。

![複数のコンポーネントデバイスのキュー実装](images/multicompqueues.png)

ドライバーは、各コンポーネントセットのビットマスクを保持します。 ビットマスクの各ビットは、コンポーネントの1つのアクティブ/アイドル状態を表します。 ビットが設定されている場合、コンポーネントはアクティブです。 ビットがオフの場合、コンポーネントはアイドル状態になります。

要求が到着すると、最上位レベルのキューの[要求ハンドラー](request-handlers.md)によって、要求が必要とするコンポーネントが決定され、それぞれに対して[**PoFxActivateComponent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxactivatecomponent)が呼び出されます。 要求ハンドラーは、そのコンポーネントのセットに対応するセカンダリ i/o キューに要求を転送します。

コンポーネントがアクティブになると、電源管理フレームワーク (PoFx) はドライバーの[*ComponentActiveConditionCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_component_active_condition_callback)ルーチンを呼び出します。 このコールバックでは、ドライバーは、そのコンポーネントが表される各ビットマスクで、指定されたコンポーネントに対応するビットを設定します。 特定のビットマスク内のすべてのビットが設定されている場合は、対応するセット内のすべてのコンポーネントがアクティブになります。 完全にアクティブになっているコンポーネントセットごとに、ドライバーは[**Wdfioqueuestart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuestart)を呼び出して、対応するセカンダリ i/o キューを開始します。

たとえば、上記の架空のデバイスを考えてみましょう。 コンポーネント1と2がアイドル状態のときに、コンポーネント0がアクティブになっているとします。 コンポーネント2がアクティブになると、PoFx はそのコンポーネントの[*ComponentActiveConditionCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_component_active_condition_callback)ルーチンを呼び出します。 要求の種類 A および C はコンポーネント2を使用するので、ドライバーはこの2つの要求の種類のビットマスクを操作します。 要求の種類 A のビットマスクのすべてのビットが設定されているので、ドライバーは要求の種類 A のキューを開始します。ただし、すべてのビットが要求の種類 C に設定されているわけではありません (コンポーネント1はアイドル状態のままです)。 ドライバーは、要求の種類 C のキューを開始しません。

セカンダリ i/o キューが開始されると、フレームワークはキューに格納されている要求の配信を開始します。 セカンダリ i/o キューの[要求ハンドラー](request-handlers.md)では、ドライバーは要求を安全に処理できます。これは、コンポーネントがアクティブで、各要求のコンポーネントで電源参照が取得されているためです。

ドライバーは、要求の処理を完了すると、要求を使用していた各コンポーネントに対して[**PoFxIdleComponent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxidlecomponent)を呼び出し、要求を完了します。 コンポーネントを使用する要求がそれ以上ない場合、power framework はドライバーの[*ComponentIdleConditionCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_component_idle_condition_callback)ルーチンを呼び出します。

このコールバックでは、ドライバーは、そのコンポーネントが表される各ビットマスクで、指定されたコンポーネントに対応するビットをクリアします。 指定されたビットマスクが、対応するセット内の最初のコンポーネントがアイドル状態に遷移することを示している場合、ドライバーは[**Wdfioqueuestop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuestop)を呼び出して、対応するセカンダリ i/o キューを停止します。 これにより、ドライバーは、対応するセット内のすべてのコンポーネントがアクティブでない限り、キューが要求をディスパッチしないようにします。

上記の例をもう一度検討します。 すべてのコンポーネントがアクティブであり、すべてのキューが開始されているとします。 コンポーネント1がアイドル状態になると、PoFx はコンポーネント1の[*ComponentIdleConditionCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_component_idle_condition_callback)ルーチンを呼び出します。 このコールバックでは、ドライバーはコンポーネント1を使用するので、要求の種類 B と C のビットマスクを操作します。 コンポーネント1は、これらの要求の種類の両方でアイドル状態になる最初のコンポーネントであるため、ドライバーは、要求の種類 B と C のキューを停止します。

この時点で、コンポーネント0がアイドル状態になるとします。 コンポーネント0の[*ComponentIdleConditionCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_component_idle_condition_callback)では、ドライバーは、要求の種類 A および C のビットマスクを操作します。コンポーネント0は、要求の種類 A に対してアイドル状態になる最初のコンポーネントであるため (コンポーネント2はまだアクティブ)、ドライバーは要求の種類 A のキューを停止します。ただし、要求の種類が C の場合、コンポーネント0は、アイドル状態になる最初のコンポーネントではありません。 ドライバーは、要求の種類 C のキューを停止しません (これは以前の動作でした)。

この例で説明されている手法を使用するには、ドライバーが各セカンダリキューの[*EvtIoCanceledOnQueue*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_canceled_on_queue)コールバック関数も登録する必要があります。 セカンダリキュー内で要求がキャンセルされた場合、ドライバーはこのコールバックを使用して、対応する各コンポーネントに対して[**PoFxIdleComponent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxidlecomponent)を呼び出すことができます。 これにより、要求をセカンダリキューに転送する前に、要求ハンドラーが[**PoFxActivateComponent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxactivatecomponent)を呼び出したときに実行した電源参照が解放されます。

 

 





