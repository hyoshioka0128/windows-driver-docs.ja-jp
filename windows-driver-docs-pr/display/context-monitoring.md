---
title: コンテキストの監視
description: 監視対象フェンスオブジェクトはフェンス同期の高度な形式で、CPU コアまたはグラフィックスプロセッシングユニット (GPU) エンジンが特定のフェンスオブジェクトをシグナルまたは待機できるようにします。これにより、GPU エンジン間での同期が非常に柔軟になります。CPU コアと GPU エンジン。
ms.assetid: B593FC24-3F8B-4C8A-BBF9-8EF88B748536
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d1bfe4cce518e3c8c57c549588239bb3718fbc0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839044"
---
# <a name="context-monitoring"></a>コンテキストの監視


監視対象フェンスオブジェクトはフェンス同期の高度な形式で、CPU コアまたはグラフィックスプロセッシングユニット (GPU) エンジンが特定のフェンスオブジェクトをシグナルまたは待機できるようにします。これにより、GPU エンジン間での同期が非常に柔軟になります。CPU コアと GPU エンジン。

## <a name="span-id_monitored_fence_creationspanspan-id_monitored_fence_creationspanspan-id_monitored_fence_creationspan-monitored-fence-creation"></a><span id="_Monitored_fence_creation"></span><span id="_monitored_fence_creation"></span><span id="_MONITORED_FENCE_CREATION"></span>監視対象フェンスの作成


監視対象フェンスオブジェクトは、新しい同期オブジェクトの種類**D3DDDI\_監視\_フェンス**で[*CreateSynchronizationObjectCb*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createsynchronizationobjectcb) callback を呼び出すことによって作成されます。

監視対象フェンスオブジェクトは、次の属性と共に作成されます。

-   初期値
-   フラグ (待機とシグナル動作の指定)

作成時に、グラフィックスカーネルは次の項目で構成されるフェンスオブジェクトを返します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">項目</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="hSyncObject"></span><span id="hsyncobject"></span><span id="HSYNCOBJECT"></span>hSyncObject</p></td>
<td align="left"><p>同期オブジェクトへのハンドル。 グラフィックスカーネルの呼び出しで参照するために使用されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="FenceValueCPUVirtualAddress"></span><span id="fencevaluecpuvirtualaddress"></span><span id="FENCEVALUECPUVIRTUALADDRESS"></span>FenceValueCPUVirtualAddress</p></td>
<td align="left"><p>CPU のフェンス値 (64bits) の読み取り専用マッピング。 このアドレスは、他のプラットフォームでの i/o の一貫性、UC (キャッシュされていない) をサポートするプラットフォームの CPU の観点から、WB (キャッシュ可能) にマップされます。 このメモリ位置を読み取るだけで、フェンスの進行状況を CPU が追跡できるようにします。 CPU は、このメモリ位置への書き込みを許可されていません。 フェンスを知らせるために、CPU は<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_signalsynchronizationobjectfromcpucb" data-raw-source="[&lt;em&gt;SignalSynchronizationObjectFromCpuCb&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_signalsynchronizationobjectfromcpucb)"><em>Signal同期 Objectfromcpu cb</em></a>を呼び出す必要があります。</p>
<p><em>IoMmu</em>をサポートするアダプターでは、GPU アクセスにこのアドレスを使用する必要があります。 この場合、アドレスは読み取り/書き込みとしてマップされます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="FenceValueGPUVirtualAddress"></span><span id="fencevaluegpuvirtualaddress"></span><span id="FENCEVALUEGPUVIRTUALADDRESS"></span>FenceValueGPUVirtualAddress</p></td>
<td align="left"><p>GPU のフェンス値 (64bits) の読み取り/書き込みマッピング。 このアドレスは、それをサポートするプラットフォームで i/o の一貫性を要求するようにマップされます。 フェンスを知らせるために、GPU はこの GPU 仮想アドレスに直接書き込むことができます。</p>
<p>このアドレスは、 <em>IoMmu</em>gpu では使用できません。</p></td>
</tr>
</tbody>
</table>

 

フェンスの値は64ビットの値で、それぞれの仮想アドレスが64ビットの境界に合わせて調整されます。 Gpu は、新しい[**DXGK\_VIDSCHCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidschcaps)::**No64BitAtomics**フラグを使用して、CPU によって表示される64ビット値をアトミックに更新できるかどうかを宣言する必要があります。 GPU が32ビット値の更新だけをアトミックに行うことができる場合、OS はフェンスの周回文字を自動的に処理します。 ただし、未処理の待機とシグナルフェンスの値は、最後にシグナルを出したフェンス値から離れた **\_最大**/2 を超えることはできません。
## <a name="span-idgpu_signalspanspan-idgpu_signalspanspan-idgpu_signalspangpu-signal"></a><span id="GPU_signal"></span><span id="gpu_signal"></span><span id="GPU_SIGNAL"></span>GPU シグナル


GPU エンジンが仮想アドレスを使用して監視対象フェンスに書き込むことができない場合、ユーザーモードドライバーは、ソフトウェアシグナルパケットを GPU コンテキストにキューに追加する新しい[*Signal同期 Objectfroデバイス Pucb*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_signalsynchronizationobjectfromgpucb)コールバックを使用します。

GPU からフェンスを通知するために、ユーザーモードドライバーは、カーネルモデルを介さずに、コンテキストコマンドストリームにフェンス書き込みコマンドを直接挿入します。 カーネルがフェンスの進行状況を監視するメカニズムは、特定の GPU エンジンが、監視されているフェンスの基本または高度な実装をサポートしているかどうかによって異なります。

GPU でのコマンドバッファーの実行が完了すると、グラフィックスカーネルは、このプロセスでシグナル状態になる可能性のあるフェンスオブジェクトの一覧を処理し、現在のフェンス値を読み取り、待機処理が必要なものがあるかどうかを判断します。待機を解除します。

## <a name="span-id_gpu_waitspanspan-id_gpu_waitspanspan-id_gpu_waitspan-gpu-wait"></a><span id="_GPU_wait"></span><span id="_gpu_wait"></span><span id="_GPU_WAIT"></span>GPU 待機


GPU エンジンで監視されているフェンスを待機するには、まず、ユーザーモードドライバーが保留中のコマンドバッファーをフラッシュし、次に、フェンスオブジェクト (**hSyncObject**) を指定し、フェンスの[*値を指定*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_waitforsynchronizationobjectfromgpucb)します。待機しています。 グラフィックスカーネルは内部データベースへの依存関係をキューに配置し、ユーザーモードドライバーに直ちに戻ります。これにより、待機操作の背後で作業をキューに配置し続けることができます。 待機操作後に送信されたコマンドバッファーは、待機操作が完了するまで実行されるようにスケジュールされません。

## <a name="span-idcpu_signalspanspan-idcpu_signalspanspan-idcpu_signalspancpu-signal"></a><span id="CPU_signal"></span><span id="cpu_signal"></span><span id="CPU_SIGNAL"></span>CPU シグナル


CPU が監視対象フェンスオブジェクトを通知できるように、新しい[*Signal同期 Objectfromcpu cb*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_signalsynchronizationobjectfromcpucb)が追加されました。 監視対象のフェンスオブジェクトが CPU によって通知されると、グラフィックスカーネルは、ユーザーモードのリーダーにすぐに表示されるように、また、満たされているすべての待機処理をすぐに待機しないように、シグナル値を使用してフェンスのメモリ位置を更新します。

## <a name="span-idcpu_waitspanspan-idcpu_waitspanspan-idcpu_waitspancpu-wait"></a><span id="CPU_wait"></span><span id="cpu_wait"></span><span id="CPU_WAIT"></span>CPU 待機


CPU が監視対象フェンスオブジェクトで待機できるように、新しい[*Waitfor同期 Objectfromcpu cb*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_waitforsynchronizationobjectfromcpucb)が追加されました。 2つの形式の待機操作が可能です。 最初の形式では、 *Waitfor同期 Objectfromcpu cb*コールバックは待機が完了するまでブロックします。 2番目の形式では、 *Waitfor同期 Objectfromcpu cb*は、待機状態が満たされた後に通知される CPU イベントへのハンドルを取得します。

 

 





