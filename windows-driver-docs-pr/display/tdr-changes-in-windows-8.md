---
title: Windows 8 での TDR の変更
description: GPU のタイムアウト検出と復旧 (TDR) の動作の Windows 8 以降では、アダプターのリセットを要求する代わりに、リセットする物理アダプターの個々 の部分を許可する変更されました。
ms.assetid: 5BC4F94C-2B45-44E2-8BBF-B455BB864A29
keywords:
- (タイムアウト検出と回復) TDR WDK の表示、Windows 8 での変更
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5a7ad0cd9205de14e01b4ccb197090c856f68298
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571062"
---
# <a name="tdr-changes-in-windows-8"></a>Windows 8 での TDR の変更


GPU のタイムアウト検出と復旧 (TDR) の動作の Windows 8 以降では、アダプターのリセットを要求する代わりに、リセットする物理アダプターの個々 の部分を許可する変更されました。

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
<td align="left">ドライバーの実装: 完全なグラフィックスとレンダリングのみ</td>
<td align="left">必須</td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit" data-raw-source="[WHCK](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)">WHCK</a>要件とテスト</td>
<td align="left"><p><strong>Device.Graphics.TDRResiliency</strong></p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idtdrdevicedriverinterfaceddispanspan-idtdrdevicedriverinterfaceddispanspan-idtdrdevicedriverinterfaceddispantdr-device-driver-interface-ddi"></a><span id="TDR_device_driver_interface__DDI_"></span><span id="tdr_device_driver_interface__ddi_"></span><span id="TDR_DEVICE_DRIVER_INTERFACE__DDI_"></span>TDR デバイス ドライバー インターフェイス (DDI)


この動作の変更に合わせて、ディスプレイ ミニポート ドライバーは、これらの関数を実装する必要があります。

-   [*DxgkDdiQueryDependentEngineGroup*](https://msdn.microsoft.com/library/windows/hardware/hh451407)
-   [*DxgkDdiQueryEngineStatus*](https://msdn.microsoft.com/library/windows/hardware/hh451411)
-   [*DxgkDdiResetEngine*](https://msdn.microsoft.com/library/windows/hardware/hh451418)

**注**  これらの関数をサポートしているドライバーのサポート レベル 0 の同期があります、 [ *DxgkDdiCollectDbgInfo* ](https://msdn.microsoft.com/library/windows/hardware/ff559595)関数。 これは、そのレベル 0 ミニポートの呼び出しの影響を受けませんが、リセット操作を続行できることを確認します。 「解説」を参照してください。 *DxgkDdiCollectDbgInfo*します。

 

これらの構造は、新しい関数に関連付けられました。

-   [**DXGK\_DRIVERCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff561062) (新しい**SupportPerEngineTDR**メンバー)
-   [**DXGK\_ENGINESTATUS**](https://msdn.microsoft.com/library/windows/hardware/hh464023)
-   [**DXGKARG\_QUERYDEPENDENTENGINEGROUP**](https://msdn.microsoft.com/library/windows/hardware/hh451294)
-   [**DXGKARG\_QUERYENGINESTATUS**](https://msdn.microsoft.com/library/windows/hardware/hh451299)
-   [**DXGKARG\_RESETENGINE**](https://msdn.microsoft.com/library/windows/hardware/hh451303)

ディスプレイのミニポート ドライバーを設定してこれらの関数のサポートを示します、 [ **DXGK\_DRIVERCAPS**](https://msdn.microsoft.com/library/windows/hardware/ff561062).**SupportPerEngineTDR**メンバー、その場合、実装する必要があります、 [ *DxgkDdiQueryDependentEngineGroup*](https://msdn.microsoft.com/library/windows/hardware/hh451407)、 [ *DxgkDdiQueryEngineStatus*](https://msdn.microsoft.com/library/windows/hardware/hh451411)、および[ *DxgkDdiResetEngine* ](https://msdn.microsoft.com/library/windows/hardware/hh451418)関数。

## <a name="span-idtdrprocessdescriptionspanspan-idtdrprocessdescriptionspanspan-idtdrprocessdescriptionspantdr-process-description"></a><span id="TDR_process_description"></span><span id="tdr_process_description"></span><span id="TDR_PROCESS_DESCRIPTION"></span>TDR プロセスの説明


一般的な安定性問題をグラフィックスでは、システムが完全にフリーズやハングした、エンドユーザーのコマンドまたは操作の処理中に表示されたらに発生します。 通常、GPU は、ゲーム プレイ中に、負荷の高いグラフィックスの操作を通常処理でビジー状態です。 画面の更新が発生しないと、ユーザーは、システムが固定されていることを想定します。 ユーザーは、通常は数秒待ってからして、電源ボタンを押して、システムを再起動します。

Windows Vista と Windows 7 の両方をこれら問題のある状況がハングし、応答性の高いデスクトップを動的に回復を検出するために再試行してください。 システムは再起動されませんが、ほとんどの場合、画面のちらつきが再描画されるようにします。 ただし、一部の古い Microsoft DirectX アプリケーションの回復の最後に黒い画面をレンダリングして、ユーザーがこれらのアプリケーションを再起動する必要があります。 これらの GPU のハングがタイムアウト検出と回復エラー (TDRs) と呼ばれます。

図では、タイムアウト検出と回復プロセスを示します。 このプロセスの詳細については、[タイムアウト検出と復旧 (TDR)](timeout-detection-and-recovery.md)を参照してください。

![タイムアウト検出と wddm を通じて gpu の復旧 (tdr)](images/timeoutdetectionrecoverygpusthroughwddm.jpg)

TDRs は GPU コマンドが完了に時間が取得や、ハードウェアがハングしたときに発生します。 TDRs は、UI が応答していないことを検出するために、オペレーティング システムを有効にします。

## <a name="span-idnodesspanspan-idnodesspanspan-idnodesspannodes"></a><span id="Nodes"></span><span id="nodes"></span><span id="NODES"></span>ノード


上記の TDR 関数で使用するため、*ノード*は個別にスケジュールする単一の物理アダプターの複数の部分の 1 つです。 例、3-D ノード、ビデオのデコード ノードおよびコピーのノードにすべて存在できます、同じ物理アダプターとで別のノードの序数値を割り当てることができる各、 [ **DXGKARG\_QUERYDEPENDENTENGINEGROUP**](https://msdn.microsoft.com/library/windows/hardware/hh451294).**NodeOrdinal**メンバーへの呼び出しで[ *DxgkDdiQueryDependentEngineGroup*](https://msdn.microsoft.com/library/windows/hardware/hh451407)します。

物理アダプター内のノードの数がでディスプレイのミニポート ドライバーによって報告された、 **NbAsymetricProcessingNodes**のメンバー [ **DXGK\_DRIVERCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff561062).**GpuEngineTopology**します。

ノードの序数値が渡された、 **NodeOrdinal**のメンバー、 [ **DXGKARG\_CREATECONTEXT** ](https://msdn.microsoft.com/library/windows/hardware/ff557567)コンテキストが作成されるときに構造体します。

## <a name="span-idenginesspanspan-idenginesspanspan-idenginesspanengines"></a><span id="Engines"></span><span id="engines"></span><span id="ENGINES"></span>エンジン


上記の TDR 関数で使用するため、*エンジン*論理アダプターが 1 つとしてまとめてその動作は、複数の物理アダプター (または Gpu) のいずれか。 DirectX グラフィックスのカーネル サブシステムはこのような構成をサポートしていますが、各エンジンは同じ数のノードである必要がありますが必要です。

たとえば、GPU のスケジューラはエンジン 0 の物理アダプターに対応する 0 と見なします。 0 をエンジンには、アダプターが 1 に対応する、1、エンジンと同じ数のノードの必要があります。

## <a name="span-idengineordinalvalueatcontextcreationspanspan-idengineordinalvalueatcontextcreationspanspan-idengineordinalvalueatcontextcreationspanengine-ordinal-value-at-context-creation"></a><span id="Engine_ordinal_value_at_context_creation"></span><span id="engine_ordinal_value_at_context_creation"></span><span id="ENGINE_ORDINAL_VALUE_AT_CONTEXT_CREATION"></span>エンジンの序数値にコンテキストの作成


エンジンを表す序数値に対応する 1 つのビットが設定されて、コンテキストが作成されたときに、 **EngineAffinity**のメンバー、 [ **DXGKARG\_CREATECONTEXT** ](https://msdn.microsoft.com/library/windows/hardware/ff557567)構造体。 **EngineOrdinal**これと他のスケジューラに関連する構造体のメンバーは、0 から始まるインデックス。 値**EngineAffinity** 1 は、 &lt; &lt; **EngineOrdinal**、および**EngineOrdinal**で最上位ビット位置は、 **EngineAffinity**します。

## <a name="span-idpacketsunaffectedbyengineresetspanspan-idpacketsunaffectedbyengineresetspanspan-idpacketsunaffectedbyengineresetspanpackets-unaffected-by-engine-reset"></a><span id="Packets_unaffected_by_engine_reset"></span><span id="packets_unaffected_by_engine_reset"></span><span id="PACKETS_UNAFFECTED_BY_ENGINE_RESET"></span>エンジンのリセットにより影響を受けていないパケット


GPU スケジューラによってドライバーを求められる場合が、遅すぎるエンジンのリセットが完了する前に完全に処理するエンジン ハードウェア キューに送信されたパケットを再実行してください。 ドライバーは、このようなパケットを再送信する次のガイドラインに従う必要があります。

-   *ページング パケット*:ドライバーを最初に送信されたように、元のフェンス Id と同じ順序でページング パケットを再送信する GPU のスケジューラによって求められます。 新しいパケットがハードウェア キューに追加される前に、このようなすべてのパケットを再送信されます。
-   *パケットをレンダリング*:GPU スケジューラはレンダリング パケット フェンスに新しい Id を割り当てるし、それらを再送信します。

## <a name="span-idcallingsequencetoresetanenginespanspan-idcallingsequencetoresetanenginespanspan-idcallingsequencetoresetanenginespancalling-sequence-to-reset-an-engine"></a><span id="Calling_sequence_to_reset_an_engine"></span><span id="calling_sequence_to_reset_an_engine"></span><span id="CALLING_SEQUENCE_TO_RESET_AN_ENGINE"></span>呼び出しシーケンス エンジンをリセットするには


ときに[ *DxgkDdiResetEngine* ](https://msdn.microsoft.com/library/windows/hardware/hh451418)成功すると、GPU スケジューラにより、 **LastAbortedFenceId**エンジン リセット呼び出しから返される値に対応するいずれか、既存フェンス ID または GPU 上で最後の完成したフェンス ID に、ハードウェア キューでです。 後者の場合は、GPU のタイムアウトが検出されたが、エンジンはコールバックをリセットする前に呼び出されるハードウェア キューが空にするときに発生します。

GPU 上で最後の完成したフェンス ID 値で維持しなければならない、ドライバーによって常にも設定する必要があるため、 **DmaPreempted**.**LastCompletedFenceId**のメンバー、 [ **DXGKARGCB\_通知\_割り込み\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff557538)優先権割り込み通知構造体。 最後の完成したフェンス ID は、このような状況でのみ高度な必要があります。

-   パケットは、(プリエンプトされない) が完了したら、完了したフェンスの最後の ID を設定して、完了したパケットのフェンス ID にください。
-   ときに[ *DxgkDdiResetEngine* ](https://msdn.microsoft.com/library/windows/hardware/hh451418)成功すると、前回完了したフェンス ID の値に設定する必要があります、 **LastCompletedFenceId**エンジンによって返されるメンバーの呼び出しをリセットします。
-   アダプター全体の設定にリセット上のすべてのノードの ID は、最後に移すことは前回完了したフェンスはリセット時にフェンスの ID を送信します。

GPU スケジューラから見た次の成功のエンジンのリセットを時間的順序に示します。

1.  プリエンプションの試行が発行されます。
2.  GPU のタイムアウトが検出されました。
3.  GPU のスケジューラによって最後に送信し、完了したフェンス Id のスナップショットが作成され、タイムアウトのエンジンからの割り込みが無視されます。 これは、デバイスの割り込みのレベルで 1 つのアトミック操作です。
4.  ない場合のパケット ハードウェア キューでこの時点で、次のように終了します。 これは、手順 2 および 3 の間の時間枠内にパケットが完了した場合に発生することができます。
5.  すべてのキューに置かれた Dpc がフラッシュされます。
6.  エンジンをリセットするために準備します。
7.  呼び出す[ *DxgkDdiResetEngine*](https://msdn.microsoft.com/library/windows/hardware/hh451418)します。
8.  場合、 **LastAbortedFenceId**メンバーが最後にフェンスの ID を完了するかは前回送信されたフェンス ID よりも大きいよりも少ない、DirectX グラフィックスのカーネルのサブシステムがシステムのバグチェックが発生します。 メッセージによって、クラッシュ ダンプ ファイルにエラーが表示**バグチェック 0x119**、これら 4 つのパラメーターを持ちます。
    -   0 xa、中止されたフェンスの無効な ID が報告されたドライバーの意味
    -   **LastAbortedFenceId**ドライバーによって返される値
    -   最後の完成したフェンス ID
    -   内部のオペレーティング システムのパラメーター

9.  場合、 **LastAbortedFenceId**値が有効では、次のようにエンジンのリセットの回復を続行します。 ページング パケットがエンジン リセットにより影響を受けた場合、GPU のスケジューラは、アダプター全体がリセット リセット エンジンに従います。 ページング パケットによって参照される割り当てを所有しているすべてのデバイスは、エラーの状態に格納されます。 ただし、システム デバイス自体がエラー状態に配置しないと、リセットが完了したら、実行を再開します。

## <a name="span-idspecialcasesspanspan-idspecialcasesspanspan-idspecialcasesspanspecial-cases"></a><span id="Special_cases"></span><span id="special_cases"></span><span id="SPECIAL_CASES"></span>特殊なケース


特殊な状況は、手順 3. および上記で説明した 7 の間での GPU でパケットが完了したときに発生します。 この場合、 **LastAbortedFenceId**から見ると、ドライバーのハードウェア キューでパケットがない場合、最後に完了したパケットのフェンス ID に、ドライバーによって設定する必要があります。 スケジューラの観点からは、このようなパケットが中止された、対応するデバイスは、パケットが最終的に完了した場合でも、エラー状態に格納されますに表示されます。

ドライバーは、ハードウェアが無効な状態であるためリセット操作を実行できない場合、またはハードウェアが、ノードをリセットすることはできないため、ドライバーはエラー状態コードを返す必要があります。 GPU のスケジューラは、エラー状態コードを受信する場合、アダプターのリセットと再起動操作の次を実行、 [TDR 動作](timeout-detection-and-recovery.md)Windows 8 より前です。

場合でも、ドライバーが Windows 8 の TDR の動作を選択して、ありますの場合、GPU のスケジューラがリセットと全体の論理アダプターの再起動を要求したときにします。 そのため、ドライバーを実装する必要がありますも、 [ *DxgkDdiResetFromTimeout* ](https://msdn.microsoft.com/library/windows/hardware/ff559815)と[ *DxgkDdiRestartFromTimeout* ](https://msdn.microsoft.com/library/windows/hardware/ff559820)関数、およびその意味では、Windows 8 より前と同じままです。 物理アダプターをリセットしようと[ *DxgkDdiResetEngine* ](https://msdn.microsoft.com/library/windows/hardware/hh451418)論理のアダプターのリセットに潜在顧客、 **! 分析**Windows デバッガーのコマンドを表示します。**TdrReason** TDR 復旧のコンテキストの値の新しい値に設定されます**TdrEngineTimeoutPromotedToAdapterReset** 9 を = です。

## <a name="span-idhardwarecertificationrequirementsspanspan-idhardwarecertificationrequirementsspanspan-idhardwarecertificationrequirementsspanhardware-certification-requirements"></a><span id="Hardware_certification_requirements"></span><span id="hardware_certification_requirements"></span><span id="HARDWARE_CERTIFICATION_REQUIREMENTS"></span>ハードウェア認定要件


この機能を実装するときにハードウェア デバイスが満たす必要のある要件については、関連するを参照してください[WHCK ドキュメント](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)で**Device.Graphics.TDRResiliency**します。

参照してください[WDDM 1.2 機能](wddm-v1-2-features.md)に Windows 8 で追加された機能の説明。

 

 





