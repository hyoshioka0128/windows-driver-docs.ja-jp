---
title: タイムアウト検出と復旧 (TDR)
description: タイムアウト検出と復旧 (TDR)
ms.assetid: f410eec7-026f-41e0-8c60-72f651659ead
keywords:
- (タイムアウト検出と回復) TDR WDK の表示、説明
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 42468138a6fdef65f9ee4ea9ef49a761754a99c0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375779"
---
# <a name="timeout-detection-and-recovery-tdr"></a>タイムアウト検出と復旧 (TDR)


グラフィックスの安定性の最も一般的な問題の 1 つには、コンピューターが「ハング」または実際には、エンドユーザーのコマンドまたは操作を処理している間は、完全に「固定」が表示されるときに発生します。 エンドユーザーは、通常数秒を待機し、コンピューターを再起動することにしました。 コンピューターの固定された外観は、GPU がゲーム プレイ中に処理を要するのグラフィカルな操作を通常処理でビジー状態のために通常発生します。 GPU がディスプレイの画面を更新できませんし、固定された、コンピューターが表示されます。

Windows Vista 以降では、オペレーティング システムを完全に「停止」コンピューターが表示される状況を検出しようとします。 オペレーティング システムは、動的にデスクトップが再び応答するために固定された状況から回復を試みます。 このプロセスの検出と回復と呼ばれる*タイムアウト検出と回復*(TDR)。 TDR プロセスで、オペレーティング システムの GPU のスケジューラを呼び出すディスプレイ ミニポート ドライバーの[ *DxgkDdiResetFromTimeout* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_resetfromtimeout)ドライバーを再初期化し、GPU をリセットする関数。 そのため、エンドユーザーでは、エクスペリエンスが大幅に改善オペレーティング システムを再起動する必要はありません。

ハング検出からのみ表示される成果物は、回復には、画面のちらつきです。 この画面では、オペレーティング システムは、これにより、画面の再描画されるグラフィックス スタックの一部をリセットしたときに結果がちらつきます。 Windows 表示 Driver Model (WDDM) 1.2 以降がディスプレイのミニポート ドライバーに準拠している場合、ちらつきがなくなります (を参照してください[WDDM 1.2 以降のシームレスな状態遷移を提供する](seamless-state-transitions-in-wddm-1-2-and-later.md))。 一部のレガシ Microsoft DirectX アプリケーション (たとえば、9.0 より前の DirectX のバージョンに準拠している DirectX アプリケーション) は、この回復の最後に黒の画面に表示可能性があります。 エンドユーザーは、これらのアプリケーションを再起動する必要があります。

このシーケンス TDR プロセスを簡単に説明します。

## <a name="span-idtimeoutdetectioninthewindowsdisplaydrivermodelwddmspanspan-idtimeoutdetectioninthewindowsdisplaydrivermodelwddmspanspan-idtimeoutdetectioninthewindowsdisplaydrivermodelwddmspantimeout-detection-in-the-windows-display-driver-model-wddm"></a><span id="Timeout_detection_in_the_Windows_Display_Driver_Model__WDDM_"></span><span id="timeout_detection_in_the_windows_display_driver_model__wddm_"></span><span id="TIMEOUT_DETECTION_IN_THE_WINDOWS_DISPLAY_DRIVER_MODEL__WDDM_"></span>Windows Display Driver Model (WDDM) のタイムアウト検出


DirectX グラフィックスのカーネル サブシステム (Dxgkrnl.sys) の一部では、GPU スケジューラは、GPU に特定のタスクの実行にかかる時間の許容時間より長い時間ことを検出します。 GPU のスケジューラは、し、この特定のタスクを切断しようとします。 切断操作には、実際の TDR タイムアウトである「待機」のタイムアウトがあります。 この手順は、プロセスのタイムアウト検出フェーズではこのためです。 Windows Vista 以降のオペレーティング システムで既定のタイムアウト期間は、2 秒です。 GPU は、完了または TDR のタイムアウト期間内の現在のタスクを横取りできることはできません、GPU が固定されているオペレーティング システムを診断します。

タイムアウト検出の発生を防ぐためには、ハードウェア ベンダーはグラフィック操作 (つまり、ダイレクト メモリ アクセス (DMA) バッファー完了) に取る生産性とゲーム プレイなどのエンド ユーザー シナリオの 2 秒確認してください。

## <a name="span-idpreparationforrecoveryspanspan-idpreparationforrecoveryspanspan-idpreparationforrecoveryspanpreparation-for-recovery"></a><span id="Preparation_for_recovery"></span><span id="preparation_for_recovery"></span><span id="PREPARATION_FOR_RECOVERY"></span>復旧の準備


オペレーティング システムの GPU スケジューラ呼び出しディスプレイ ミニポート ドライバーの[ *DxgkDdiResetFromTimeout* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_resetfromtimeout)ドライバー、オペレーティング システムにタイムアウトが検出されたことを通知する関数。 ドライバーはそれ自体を再初期化する必要がありますし、GPU をリセットします。 さらに、ドライバーはメモリへのアクセスを停止する必要があり、ハードウェアにはアクセスする必要があります。 オペレーティング システムとドライバー ハードウェアと事後の診断に役立つ可能性があるその他の状態情報を収集します。

## <a name="span-iddesktoprecoveryspanspan-iddesktoprecoveryspanspan-iddesktoprecoveryspandesktop-recovery"></a><span id="Desktop_recovery"></span><span id="desktop_recovery"></span><span id="DESKTOP_RECOVERY"></span>デスクトップの修復


オペレーティング システムでは、グラフィックス スタックの適切な状態をリセットします。 これは Dxgkrnl.sys の一部でも、ビデオ メモリ マネージャーは、ビデオ メモリからのすべての割り当てを削除します。 ディスプレイのミニポート ドライバーでは、GPU ハードウェアの状態をリセットします。 グラフィックス スタックは、最終的な操作を実行し、応答性の状態にデスクトップを復元します。 前述のように、一部のレガシ DirectX アプリケーションをこの回復では、これらのアプリケーションを再起動するには、エンドユーザーが必要ですが、最後に黒いだけレンダリング可能性があります。 適切に記述された DirectX 9Ex と DirectX 10 テクノロジのデバイスの削除を処理する以降のアプリケーションは引き続き正常に動作します。 アプリケーションは、リリースし、マイクロソフトの Direct3D デバイスとすべてのデバイスのオブジェクトを再作成する必要があります。 DirectX アプリケーションの回復方法の詳細については、Windows SDK を参照してください。

## <a name="span-idrelatedtdrtopicsspanspan-idrelatedtdrtopicsspanspan-idrelatedtdrtopicsspanrelated-tdr-topics"></a><span id="Related_TDR_topics"></span><span id="related_tdr_topics"></span><span id="RELATED_TDR_TOPICS"></span>TDR の関連トピック


TDR プロセスを説明し、レジストリ キーの TDR デバッグを有効にします。

[繰り返し発生する GPU のハングと復元の制限](limiting-repetitive-gpu-hangs-and-recoveries.md)

[TDR エラー メッセージング](tdr-error-messaging.md)

[TDR レジストリ キー](tdr-registry-keys.md)

[Windows 8 での TDR の変更](tdr-changes-in-windows-8.md)

 

 





