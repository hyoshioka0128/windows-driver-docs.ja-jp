---
title: タイムアウトの検出と復旧 (TDR)
description: タイムアウトの検出と復旧 (TDR)
ms.assetid: f410eec7-026f-41e0-8c60-72f651659ead
keywords:
- TDR (タイムアウト検出と復旧) WDK 表示、説明
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 474467b6860913a78a7f66c2ef4e2501545e4e32
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829320"
---
# <a name="timeout-detection-and-recovery-tdr"></a>タイムアウトの検出と復旧 (TDR)


グラフィックスにおける最も一般的な安定性の問題の1つは、コンピューターが "ハング" するか、完全に "フリーズ" されているときです。実際には、エンドユーザーのコマンドまたは操作を処理しています。 通常、エンドユーザーは数秒待ってから、コンピューターの再起動を決定します。 通常、コンピューターがフリーズしている状況は、GPU が通常はゲーム再生中に大量のグラフィック操作を処理するためにビジー状態であるために発生します。 GPU はディスプレイ画面を更新せず、コンピューターがフリーズした状態で表示されます。

Windows Vista 以降では、オペレーティングシステムは、コンピューターが完全に "フリーズ" されていると思われる状況を検出しようとします。 次に、オペレーティングシステムは、デスクトップが再び応答するように、凍結された状況から動的に回復しようとします。 この検出と復旧のプロセスは *、タイムアウトの検出と復旧*(TDR) と呼ばれています。 TDR プロセスでは、オペレーティングシステムの GPU スケジューラがディスプレイミニポートドライバーの[*DxgkDdiResetFromTimeout*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_resetfromtimeout)関数を呼び出して、ドライバーを再初期化し、GPU をリセットします。 そのため、エンドユーザーはオペレーティングシステムを再起動する必要がなく、エクスペリエンスが大幅に向上します。

ハング検出から回復まで表示されるアイテムは、画面のちらつきだけです。 この画面では、オペレーティングシステムによってグラフィックススタックの一部がリセットされ、画面が再描画されると、結果がちらつきます。 ディスプレイミニポートドライバーが Windows Display Driver Model (WDDM) 1.2 以降に準拠している場合は、このちらつきが解消されます (「 [wddm 1.2 以降でのシームレスな状態遷移の提供](seamless-state-transitions-in-wddm-1-2-and-later.md)」を参照してください)。 一部のレガシ Microsoft DirectX アプリケーション (たとえば、9.0 より前の DirectX バージョンに準拠する DirectX アプリケーションなど) は、この回復の最後に黒い画面に表示されることがあります。 エンドユーザーは、これらのアプリケーションを再起動する必要があります。

このシーケンスでは、TDR プロセスについて簡単に説明します。

## <a name="span-idtimeout_detection_in_the_windows_display_driver_model__wddm_spanspan-idtimeout_detection_in_the_windows_display_driver_model__wddm_spanspan-idtimeout_detection_in_the_windows_display_driver_model__wddm_spantimeout-detection-in-the-windows-display-driver-model-wddm"></a><span id="Timeout_detection_in_the_Windows_Display_Driver_Model__WDDM_"></span><span id="timeout_detection_in_the_windows_display_driver_model__wddm_"></span><span id="TIMEOUT_DETECTION_IN_THE_WINDOWS_DISPLAY_DRIVER_MODEL__WDDM_"></span>Windows Display Driver Model (WDDM) でのタイムアウトの検出


DirectX グラフィックスカーネルサブシステム (Dxgkrnl) の一部である GPU スケジューラは、GPU が特定のタスクを実行するのに許容される時間を超えていることを検出します。 次に、GPU スケジューラは、この特定のタスクを横取りしようとします。 プリエンプト操作には、実際の TDR タイムアウトである "wait" タイムアウトがあります。 この手順は、プロセスのタイムアウト検出フェーズです。 Windows Vista 以降のオペレーティングシステムの既定のタイムアウト期間は2秒です。 GPU が TDR のタイムアウト期間内に現在のタスクを完了またはプリエンプトできない場合、オペレーティングシステムは GPU が固定されていることを診断します。

タイムアウトの検出が行われないように、ハードウェアベンダーは、グラフィックス操作 (つまり、ダイレクトメモリアクセス (DMA) バッファーの完了) がエンドユーザーのシナリオ (生産性やゲームプレイなど) で2秒以内に実行されることを保証する必要があります。

## <a name="span-idpreparation_for_recoveryspanspan-idpreparation_for_recoveryspanspan-idpreparation_for_recoveryspanpreparation-for-recovery"></a><span id="Preparation_for_recovery"></span><span id="preparation_for_recovery"></span><span id="PREPARATION_FOR_RECOVERY"></span>回復の準備


オペレーティングシステムの GPU スケジューラは、ディスプレイミニポートドライバーの[*DxgkDdiResetFromTimeout*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_resetfromtimeout)関数を呼び出して、オペレーティングシステムがタイムアウトを検出したことをドライバーに通知します。 ドライバーは、それ自体を再初期化し、GPU をリセットする必要があります。 また、ドライバーはメモリへのアクセスを停止する必要があり、ハードウェアにアクセスすることはできません。 オペレーティングシステムとドライバーによってハードウェアおよびその他の状態情報が収集され、事後診断に役立つ可能性があります。

## <a name="span-iddesktop_recoveryspanspan-iddesktop_recoveryspanspan-iddesktop_recoveryspandesktop-recovery"></a><span id="Desktop_recovery"></span><span id="desktop_recovery"></span><span id="DESKTOP_RECOVERY"></span>デスクトップの回復


オペレーティングシステムによって、グラフィックススタックの適切な状態がリセットされます。 Dxgkrnl の一部でもあるビデオメモリマネージャーは、ビデオメモリからすべての割り当てを削除します。 ディスプレイミニポートドライバーは、GPU ハードウェアの状態をリセットします。 グラフィックススタックは最後のアクションを実行し、デスクトップを応答性の高い状態に復元します。 既に説明したように、一部のレガシ DirectX アプリケーションは、この回復の最後に黒のみを表示することがあります。この場合、エンドユーザーはこれらのアプリケーションを再起動する必要があります。 適切に記述された DirectX 9Ex および DirectX 10 以降のデバイスの削除テクノロジを処理するアプリケーションは、引き続き正常に動作します。 アプリケーションは、Microsoft Direct3D デバイスとデバイスのすべてのオブジェクトを解放してから、再作成する必要があります。 DirectX アプリケーションの回復方法の詳細については、Windows SDK を参照してください。

## <a name="span-idrelated_tdr_topicsspanspan-idrelated_tdr_topicsspanspan-idrelated_tdr_topicsspanrelated-tdr-topics"></a><span id="Related_TDR_topics"></span><span id="related_tdr_topics"></span><span id="RELATED_TDR_TOPICS"></span>関連する TDR のトピック


これらのトピックでは、TDR のデバッグを有効にする TDR プロセスとレジストリキーについて説明します。

[繰り返し発生する GPU のハングと回復の制限](limiting-repetitive-gpu-hangs-and-recoveries.md)

[TDR のエラーメッセージ](tdr-error-messaging.md)

[TDR レジストリキー](tdr-registry-keys.md)

[Windows 8 での TDR の変更点](tdr-changes-in-windows-8.md)

 

 





