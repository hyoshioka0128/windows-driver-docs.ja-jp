---
title: Windows 8 での TDR の変更
description: Windows 8 以降では、GPU タイムアウト検出と復旧 (TDR) の動作が変更され、アダプター全体のリセットを必要とせずに、個々の物理アダプターの一部をリセットできるようになりました。
ms.assetid: 5BC4F94C-2B45-44E2-8BBF-B455BB864A29
keywords:
- TDR (タイムアウト検出と回復) WDK 表示、Windows 8 での変更
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe4bcca805ba8389db2cc258d82d0a8d156421f6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829336"
---
# <a name="tdr-changes-in-windows-8"></a>Windows 8 での TDR の変更


Windows 8 以降では、GPU タイムアウト検出と復旧 (TDR) の動作が変更され、アダプター全体のリセットを必要とせずに、個々の物理アダプターの一部をリセットできるようになりました。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">Windows Display Driver Model (WDDM) の最小バージョン</td>
<td align="left">1.2</td>
</tr>
<tr class="even">
<td align="left">Windows の最小バージョン</td>
<td align="left">8</td>
</tr>
<tr class="odd">
<td align="left">ドライバーの実装—完全なグラフィックスとレンダーのみ</td>
<td align="left">必須</td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit" data-raw-source="[WHCK](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)">必要条件</a>とテスト</td>
<td align="left"><p><strong>デバイス...TDRResiliency</strong></p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idtdr_device_driver_interface__ddi_spanspan-idtdr_device_driver_interface__ddi_spanspan-idtdr_device_driver_interface__ddi_spantdr-device-driver-interface-ddi"></a><span id="TDR_device_driver_interface__DDI_"></span><span id="tdr_device_driver_interface__ddi_"></span><span id="TDR_DEVICE_DRIVER_INTERFACE__DDI_"></span>TDR device driver interface (DDI)


この動作の変更に対応するために、表示ミニポートドライバーは次の機能を実装する必要があります。

-   [*DxgkDdiQueryDependentEngineGroup*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_querydependentenginegroup)
-   [*DxgkDdiQueryEngineStatus*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_queryenginestatus)
-   [*DxgkDdiResetEngine*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_resetengine)

**注**  これらの関数をサポートするドライバーは、 [*DxgkDdiCollectDbgInfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_collectdbginfo)関数のレベルゼロの同期もサポートする必要があります。 これは、レベル0のミニポート呼び出しが影響を受けないようにするためです。リセット操作は続行できます。 *DxgkDdiCollectDbgInfo*の解説を参照してください。

 

これらの構造体は、新しい関数に関連付けられています。

-   [**DXGK\_DRIVERCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_drivercaps) (新しい**SupportPerEngineTDR**メンバー)
-   [**DXGK\_ENGINESTATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_enginestatus)
-   [**DXGKARG\_QUERYDEPENDENTENGINEGROUP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_querydependentenginegroup)
-   [**DXGKARG\_QUERYENGINESTATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_queryenginestatus)
-   [**DXGKARG\_RESETENGINE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_resetengine)

表示ミニポートドライバーは、 [**DXGK\_DRIVERCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_drivercaps)を設定することによって、これらの機能のサポートを示します。**SupportPerEngineTDR** member。この場合、 [*DxgkDdiQueryDependentEngineGroup*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_querydependentenginegroup)、 [*DxgkDdiQueryEngineStatus*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_queryenginestatus)、および[*DxgkDdiResetEngine*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_resetengine)の各関数を実装する必要があります。

## <a name="span-idtdr_process_descriptionspanspan-idtdr_process_descriptionspanspan-idtdr_process_descriptionspantdr-process-description"></a><span id="TDR_process_description"></span><span id="tdr_process_description"></span><span id="TDR_PROCESS_DESCRIPTION"></span>TDR プロセスの説明


グラフィックスでの一般的な安定性の問題は、エンドユーザーのコマンドまたは操作の処理中にシステムが完全にフリーズまたはハングしたときに発生します。 通常、GPU は通常はゲームプレイ中に大量のグラフィックス操作を処理することがビジー状態です。 画面の更新は行われず、ユーザーのシステムがフリーズしていると想定されます。 通常、ユーザーは数秒待ってから、電源ボタンを押してシステムを再起動します。

Windows Vista と Windows 7 の両方で、これらの問題が発生しているハングを検出し、応答性の高いデスクトップを動的に回復します。 システムは再起動されませんが、ほとんどの場合、再描画されると画面が点滅します。 ただし、一部の古い Microsoft DirectX アプリケーションでは、回復の最後に黒い画面が表示され、ユーザーはこれらのアプリケーションを再起動する必要があります。 これらの GPU ハングは、タイムアウト検出と回復エラー (TDRs) と呼ばれます。

この図は、タイムアウトの検出と回復プロセスを示しています。 このプロセスの詳細については、「[タイムアウトの検出と復旧」 (TDR)](timeout-detection-and-recovery.md)を参照してください。

![wddm による gpu のタイムアウト検出と復旧 (tdr)](images/timeoutdetectionrecoverygpusthroughwddm.jpg)

TDRs は、GPU コマンドの実行に時間がかかりすぎて完了できなかった場合、またはハードウェアがハングした場合に発生します。 TDRs を使用すると、オペレーティングシステムは UI が応答していないことを検出できます。

## <a name="span-idnodesspanspan-idnodesspanspan-idnodesspannodes"></a><span id="Nodes"></span><span id="nodes"></span><span id="NODES"></span>節


上記の TDR 関数で使用されているように、*ノード*は、個別にスケジュールできる1つの物理アダプターの複数の部分の1つです。 たとえば、3d ノード、ビデオデコードノード、およびコピーノードはすべて同じ物理アダプター内に存在することができ、各には[**Dxgkarg\_QUERYDEPENDENTENGINEGROUP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_querydependentenginegroup)の個別のノード序数値を割り当てることができます。[*DxgkDdiQueryDependentEngineGroup*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_querydependentenginegroup)の呼び出しでの**nodeordinal**メンバー。

物理アダプター内のノード数は、 [**DXGK\_DRIVERCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_drivercaps)の**Nbasymetricprocessingnodes**メンバーのディスプレイミニポートドライバーによって報告されます。**GpuEngineTopology**。

ノードの序数値は、コンテキストの作成時に、 [**Dxgkarg\_CREATECONTEXT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_createcontext)構造体の**nodeordinal**メンバーに渡されます。

## <a name="span-idenginesspanspan-idenginesspanspan-idenginesspanengines"></a><span id="Engines"></span><span id="engines"></span><span id="ENGINES"></span>エンジン


上記の TDR 関数で使用されているように、*エンジン*は、1つの論理アダプターとして機能する複数の物理アダプター (または gpu) の1つです。 DirectX graphics カーネルサブシステムではこのような構成がサポートされていますが、各エンジンのノード数は同じである必要があります。

たとえば、GPU スケジューラは、エンジン0が物理アダプター0に対応するものと見なします。 エンジン0のノード数は、アダプター1に対応するエンジン1と同じである必要があります。

## <a name="span-idengine_ordinal_value_at_context_creationspanspan-idengine_ordinal_value_at_context_creationspanspan-idengine_ordinal_value_at_context_creationspanengine-ordinal-value-at-context-creation"></a><span id="Engine_ordinal_value_at_context_creation"></span><span id="engine_ordinal_value_at_context_creation"></span><span id="ENGINE_ORDINAL_VALUE_AT_CONTEXT_CREATION"></span>コンテキスト作成時のエンジン序数値


コンテキストが作成されると、 [**Dxgkarg\_CREATECONTEXT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_createcontext)構造体の**EngineAffinity**メンバーで、エンジンの序数値に対応する1つのビットが設定されます。 このおよび他のスケジューラ関連の構造体の**EngineOrdinal**メンバーは、0から始まるインデックスです。 **EngineAffinity**の値は 1 &lt;&lt; **EngineOrdinal**で、 **EngineOrdinal**は**EngineAffinity**内の最上位のビット位置です。

## <a name="span-idpackets_unaffected_by_engine_resetspanspan-idpackets_unaffected_by_engine_resetspanspan-idpackets_unaffected_by_engine_resetspanpackets-unaffected-by-engine-reset"></a><span id="Packets_unaffected_by_engine_reset"></span><span id="packets_unaffected_by_engine_reset"></span><span id="PACKETS_UNAFFECTED_BY_ENGINE_RESET"></span>エンジンのリセットによる影響を受けないパケット


エンジンのリセットが完了する前に、正常に送信されたパケットをエンジンハードウェアキューに再送信して完全に処理するために、GPU スケジューラからドライバーが要求される場合があります。 ドライバーは、次のガイドラインに従って、このようなパケットを再送信する必要があります。

-   *パケットのページング*: ドライバーは、元のフェンス id でページングパケットを再送信するために、GPU スケジューラによって要求されます。最初に送信されたときと同じ順序で送信されます。 このようなパケットは、新しいパケットがハードウェアキューに追加される前に再送信されます。
-   *パケットのレンダリング*: GPU スケジューラはレンダーパケットの新しいフェンス id を割り当て、再送信します。

## <a name="span-idcalling_sequence_to_reset_an_enginespanspan-idcalling_sequence_to_reset_an_enginespanspan-idcalling_sequence_to_reset_an_enginespancalling-sequence-to-reset-an-engine"></a><span id="Calling_sequence_to_reset_an_engine"></span><span id="calling_sequence_to_reset_an_engine"></span><span id="CALLING_SEQUENCE_TO_RESET_AN_ENGINE"></span>エンジンをリセットするための呼び出しシーケンス


[*DxgkDdiResetEngine*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_resetengine)が成功すると、gpu スケジューラは、エンジンのリセット呼び出しから返された**LastAbortedFenceId**値が、ハードウェアキューの既存のフェンス id に対応していること、または gpu で最後に完了したフェンス id に対応していることを保証します。 後者の状況は、GPU タイムアウトが検出された後、エンジンリセットコールバックが呼び出される前に、ハードウェアキューが空になったときに発生する可能性があります。

GPU で最後に完了したフェンス ID の値は、常にドライバーによって維持される必要があります。これは、 **Dmapreempted**設定するためにも必要であるためです。[**Dxgkargcb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkargcb_notify_interrupt_data)の**LastCompletedFenceId**メンバーは、\_割り込み\_データプリエンプション割り込み通知構造を\_通知します。 最後に完了したフェンス ID は、次の状況でのみ高度なものにする必要があります。

-   パケットが完了した (割り込まれていない) 場合は、最後に完了したフェンス ID を、完了したパケットのフェンス ID に設定する必要があります。
-   [*DxgkDdiResetEngine*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_resetengine)が成功した場合は、最後に完了したフェンス ID を、エンジンのリセット呼び出しによって返される**LastCompletedFenceId**メンバーの値に設定する必要があります。
-   アダプター全体のリセットの場合、すべてのノードで最後に完了したフェンス ID は、リセット時に最後に送信されたフェンス ID に高度になる必要があります。

GPU スケジューラに示されているように、正常にエンジンがリセットされると、次のようになります。

1.  プリエンプションの試行が発行されます。
2.  GPU タイムアウトが検出されました。
3.  最後に送信されたフェンス Id と完了したフェンス Id のスナップショットは GPU スケジューラによって取得され、タイムアウトしたエンジンからの割り込みは無視されます。 これは、デバイスの割り込みレベルでの1つのアトミック操作です。
4.  この時点でハードウェアキューにパケットがない場合は、を終了します。 これは、手順2と3の間の時間枠でパケットが完了した場合に発生する可能性があります。
5.  キューに格納されているすべての Dpc がフラッシュされます。
6.  エンジンのリセットを準備します。
7.  [*DxgkDdiResetEngine*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_resetengine)を呼び出します。
8.  **LastAbortedFenceId**メンバーが最後に完了したフェンス id より小さい場合、または最後に送信されたフェンス id よりも大きい場合は、DirectX グラフィックスカーネルサブシステムによってシステムのバグチェックが発生します。 クラッシュダンプファイルの場合、エラーは、次の4つのパラメーターを持つ、**バグチェックの 0x119**によって示されます。
    -   0xA。ドライバーが無効な中断されたフェンス ID を報告したことを意味します
    -   **LastAbortedFenceId**ドライバーによって返される値
    -   最後に完了したフェンス ID
    -   内部オペレーティングシステムパラメーター

9.  **LastAbortedFenceId**値が有効な場合は、次のようにエンジンリセットの回復を続行します。 ページングパケットがエンジンのリセットによって影響を受けた場合、GPU スケジューラは、アダプター全体のリセットでエンジンリセットに従います。 そのページングパケットによって参照される割り当てを所有するすべてのデバイスは、エラー状態にもなります。 ただし、システムデバイス自体はエラー状態にはならず、リセットの完了後に実行を再開します。

## <a name="span-idspecial_casesspanspan-idspecial_casesspanspan-idspecial_casesspanspecial-cases"></a><span id="Special_cases"></span><span id="special_cases"></span><span id="SPECIAL_CASES"></span>特殊なケース


上記の手順 3. ~ 7. で、GPU でパケットが完了すると、特殊な状況が発生する可能性があります。 この場合、ドライバーの観点からハードウェアキューにパケットがない場合は、ドライバーによって最後に完了したパケットのフェンス ID に**LastAbortedFenceId**を設定する必要があります。 スケジューラの観点から見ると、このようなパケットは中断されているように見え、パケットが最終的に完了した場合でも、対応するデバイスはエラー状態になります。

ハードウェアが無効な状態であるため、またはハードウェアがノードをリセットできないためにリセット操作を実行できない場合は、ドライバーがエラー状態コードを返す必要があります。 GPU スケジューラは、エラー状態コードを受信すると、Windows 8 より前の[TDR 動作](timeout-detection-and-recovery.md)に従って、アダプター全体のリセットと再起動操作を実行します。

ドライバーが Windows 8 の TDR 動作をオプトインしている場合でも、GPU スケジューラが論理アダプター全体のリセットと再起動を要求する場合があります。 そのため、ドライバーは[*DxgkDdiResetFromTimeout*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_resetfromtimeout)関数と[*DxgkDdiRestartFromTimeout*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_restartfromtimeout)関数を実装する必要があり、そのセマンティクスは Windows 8 よりも前と同じです。 [*DxgkDdiResetEngine*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_resetengine)を使用して物理アダプターをリセットしようとすると、論理アダプターがリセットされます。 Windows デバッガーの **[分析]** コマンドを実行すると、TDR Recovery コンテキストの**Tdrreason**値が**TdrEngineTimeoutPromotedToAdapterReset** = 9 の新しい値に設定されていることが示されます。

## <a name="span-idhardware_certification_requirementsspanspan-idhardware_certification_requirementsspanspan-idhardware_certification_requirementsspanhardware-certification-requirements"></a><span id="Hardware_certification_requirements"></span><span id="hardware_certification_requirements"></span><span id="HARDWARE_CERTIFICATION_REQUIREMENTS"></span>ハードウェア認定の要件


ハードウェアデバイスがこの機能を実装するときに満たす必要がある要件の詳細[について](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)は、**デバイス...TDRResiliency**。

Windows 8 で追加された機能の確認については、「 [WDDM 1.2 の機能](wddm-v1-2-features.md)」を参照してください。

 

 





