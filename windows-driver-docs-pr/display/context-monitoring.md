---
title: コンテキストの監視
description: フェンスの監視対象オブジェクトは、高度なフォームの CPU コアまたはグラフィックス処理ユニット (GPU) エンジンを通知したり、GPU エンジン間または間で非常に柔軟な同期できるように、特定のフェンス オブジェクトで待機を許可するフェンスの同期CPU コアと GPU エンジン。
ms.assetid: B593FC24-3F8B-4C8A-BBF9-8EF88B748536
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed9c5aa9b0766e00e3a59ad11711157f75ed70ce
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581447"
---
# <a name="context-monitoring"></a>コンテキストの監視


フェンスの監視対象オブジェクトは、高度なフォームの CPU コアまたはグラフィックス処理ユニット (GPU) エンジンを通知したり、GPU エンジン間または間で非常に柔軟な同期できるように、特定のフェンス オブジェクトで待機を許可するフェンスの同期CPU コアと GPU エンジン。

## <a name="span-idmonitoredfencecreationspanspan-idmonitoredfencecreationspanspan-idmonitoredfencecreationspan-monitored-fence-creation"></a><span id="_Monitored_fence_creation"></span><span id="_monitored_fence_creation"></span><span id="_MONITORED_FENCE_CREATION"></span> 監視対象のフェンスの作成


フェンスの監視対象オブジェクトが呼び出すことによって作成された[ *CreateSynchronizationObjectCb* ](https://msdn.microsoft.com/library/windows/hardware/ff568897)新しい同期オブジェクトの種類でコールバックを**D3DDDI\_MONITORED\_フェンス**します。

次の属性と共にフェンスの監視対象オブジェクトが作成されます。

-   初期値
-   フラグ (その待機を指定して通知の動作)

作成時に、グラフィックス カーネルは、次の項目で構成されるフェンス オブジェクトを返します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">アイテム</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="hSyncObject"></span><span id="hsyncobject"></span><span id="HSYNCOBJECT"></span>hSyncObject</p></td>
<td align="left"><p>同期オブジェクトへのハンドルします。 グラフィックスのカーネルへの呼び出しで参照するために使用します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="FenceValueCPUVirtualAddress"></span><span id="fencevaluecpuvirtualaddress"></span><span id="FENCEVALUECPUVIRTUALADDRESS"></span>FenceValueCPUVirtualAddress</p></td>
<td align="left"><p>Cpu のフェンス値 (64 ビット) の読み取り専用マッピングです。 このアドレスがマップされている I/O の一貫性、一意性が他のプラットフォームでキャッシュを (無効) をサポートするプラットフォームの cpu の観点から (キャッシュ可能な) WB します。 フェンスの進行状況でこのメモリ位置を読み取るだけの追跡に CPU を使用できます。 CPU は、このメモリ位置に書き込むには使用できません。 フェンスを通知するには、CPU が呼び出しに必要な<a href="https://msdn.microsoft.com/library/windows/hardware/dn906360" data-raw-source="[&lt;em&gt;SignalSynchronizationObjectFromCpuCb&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/dn906360)"> <em>SignalSynchronizationObjectFromCpuCb</em></a>します。</p>
<p>サポートするアダプター <em>IoMmu</em> GPU アクセス用にこのアドレスを使用する必要があります。 アドレスがここでの読み取り/書き込みとしてマップされます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="FenceValueGPUVirtualAddress"></span><span id="fencevaluegpuvirtualaddress"></span><span id="FENCEVALUEGPUVIRTUALADDRESS"></span>FenceValueGPUVirtualAddress</p></td>
<td align="left"><p>GPU のフェンス値 (64 ビット) のマッピングを読み取り/書き込みです。 このアドレスは、それをサポートするプラットフォームでの I/O の一貫性を要求するようにマップされます。 フェンスを通知するには、GPU をこの GPU 仮想アドレスに直接書き込みが許可されます。</p>
<p>このアドレスで使用する必要がありますされません<em>IoMmu</em>Gpu します。</p></td>
</tr>
</tbody>
</table>

 

フェンスの値は、64 ビットの境界に整列、それぞれの仮想アドレスを含む 64 ビット値です。 Gpu が使用して、新しい CPU によって表示として 64 ビット値をアトミックに更新できるかどうかを宣言する必要があります[ **DXGK\_VIDSCHCAPS**](https://msdn.microsoft.com/library/windows/hardware/ff562863)::**No64BitAtomics**フラグ。 GPU のみの 32 ビット値をアトミックに更新できる場合は、OS はフェンス ラップアラウンド ケースを自動的に処理されます。 ただし未処理待機とシグナルのフェンス値にすることはできません、制限は配置以上**UINT\_最大**最後のシグナルのフェンス値から/2。
## <a name="span-idgpusignalspanspan-idgpusignalspanspan-idgpusignalspangpu-signal"></a><span id="GPU_signal"></span><span id="gpu_signal"></span><span id="GPU_SIGNAL"></span>GPU のシグナル


GPU エンジンがその仮想アドレスを使用して監視対象のフェンスへの書き込み可能でない場合、ユーザー モード ドライバーは、新しい使用して[ *SignalSynchronizationObjectFromGpuCb* ](https://msdn.microsoft.com/library/windows/hardware/dn906362)がキューに登録されるコールバックをソフトウェア GPU コンテキストにパケットを信号です。

GPU からフェンスを通知するには、ユーザー モード ドライバーは、カーネルのモデルを経由せず直接フェンス書き込みコマンドをコンテキスト コマンド ストリームに挿入します。 カーネルがフェンスの進行状況を監視するメカニズムは、特定の GPU エンジンが監視対象のフェンスの基本的なまたは高度な実装をサポートするかどうかによって異なります。

待機通知がこのプロセスの保留中のフェンス オブジェクトの一覧で、使用、現在のフェンス値を読み取るし、待機する必要がある処理があるかを確認、グラフィックスのカーネルに移動してコマンド バッファーには、GPU で実行が完了すると、待機されていません。

## <a name="span-idgpuwaitspanspan-idgpuwaitspanspan-idgpuwaitspan-gpu-wait"></a><span id="_GPU_wait"></span><span id="_gpu_wait"></span><span id="_GPU_WAIT"></span> GPU の待機


GPU エンジンの監視対象のフェンスでは、ユーザー モード ドライバーを待機するがその保留中のコマンドをフラッシュする最初の必要をバッファーし呼び出し[ *WaitForSynchronizationObjectFromGpuCb* ](https://msdn.microsoft.com/library/windows/hardware/dn906367) (オブジェクトのフェンスを指定します。**hSyncObject**) フェンス値を待機するいるとします。 グラフィックス カーネルでは、キューにその内部のデータベースへの依存関係し、待機操作の背後にあるキューに作業が継続されるように、ユーザー モード ドライバーにすぐに返します。 待機操作がないスケジュール実行までの待機操作が満たされた後に送信されたバッファーをコマンドします。

## <a name="span-idcpusignalspanspan-idcpusignalspanspan-idcpusignalspancpu-signal"></a><span id="CPU_signal"></span><span id="cpu_signal"></span><span id="CPU_SIGNAL"></span>CPU signal


新しい[ *SignalSynchronizationObjectFromCpuCb* ](https://msdn.microsoft.com/library/windows/hardware/dn906360)フェンスの監視対象オブジェクトを通知するために CPU を許可するが追加されました。 フェンスの監視対象オブジェクトが、CPU によってシグナルを受け取る、グラフィックスのカーネルで更新されますフェンスのメモリ位置シグナル値、ユーザー モードのリーダーとすぐに解除待機にすぐに表示になるため、満足の待機処理。

## <a name="span-idcpuwaitspanspan-idcpuwaitspanspan-idcpuwaitspancpu-wait"></a><span id="CPU_wait"></span><span id="cpu_wait"></span><span id="CPU_WAIT"></span>CPU 待機


新しい[ *WaitForSynchronizationObjectFromCpuCb* ](https://msdn.microsoft.com/library/windows/hardware/dn906366)フェンスの監視対象オブジェクトで待機する CPU を許可するが追加されました。 待機操作の 2 つの形式を利用できます。 最初の形式、 *WaitForSynchronizationObjectFromCpuCb*コールバックは、待機が満たされているまでをブロックします。 2 番目の形式で*WaitForSynchronizationObjectFromCpuCb*ハンドルを待機条件が満たされた後に通知される CPU イベントに移動します。

 

 





