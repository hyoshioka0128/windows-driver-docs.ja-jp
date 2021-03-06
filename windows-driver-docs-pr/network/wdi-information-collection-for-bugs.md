---
title: バグの WDI 情報の収集
description: すべての重要なソフトウェアのバグは避けられないです。
ms.assetid: 551CA7DD-EB1A-41FB-A3D7-472DA7020B51
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d29048e376f6c0faa5e8d5497125c327eb71c1d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374714"
---
# <a name="wdi-information-collection-for-bugs"></a>バグの WDI 情報の収集


すべての重要なソフトウェアのバグは避けられないです。 ドライバーの開発フェーズでバグとデバッグのアクティビティは、作業の重要な一部である必要です。 バグは、オペレーティング システム、WDI UE、または WDI LE 可能性がある会社の共同作業を必要があります。 根本原因をすばやく絞り込むことに関連する情報を収集するために重要になります。 収集する情報は、バグの性質によってさまざまです。 さらに情報を収集するバグの再現のイテレーションは、必要な場合がありますが、可能な限りこれらのイテレーションを削減することが重要です。 最初にいくつかのルールを示します。

## <a name="os-crash-without-kernel-debugger-attached"></a>カーネル デバッガーをアタッチせずに OS クラッシュ


オペレーティング システムでは、クラッシュ ダンプを生成します。 クラッシュ ダンプ、ミニ ダンプと完全なダンプなどのさまざまな種類があります。 ミニ ダンプは小規模ですが、トリアージに便利ですがよくあります。 ルートの順序で完全なダンプが必要なほとんどの場合、問題が発生します。 ドライバーの開発中に完全なダンプを有効にして、自己ホスト型のフェーズをお勧めします。 完全なダンプを有効にします。

1.  右クリックし、デスクトップから**この PC**選択**プロパティ**します。
2.  **詳細** タブに移動して、**起動と回復**セクションをクリックして、**設定しています.** ボタンをクリックします。
3.  **デバッグ情報の書き込み**セクションで、選択**カーネル メモリ ダンプ**(なく**自動メモリ ダンプ**)。

%Windir% にメモリ ダンプ ファイルを生成するオペレーティング システムのクラッシュが発生したときに\\memory.dmp します。
## <a name="os-crash-with-kernel-debugger-attached"></a>カーネル デバッガーをアタッチの OS クラッシュ


開発者や QA カーネル デバッガーがアタッチ可能な場合があります。 カーネル デバッガーでは、何か問題が、さらに詳しく調査する方向をすぐに確認できます。 Kd コマンド '[ **! 分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze) – v' バグ チェック後に実行する最初のコマンドとして役に立ちます。 このコマンドは、クラッシュが発生したモジュールと、クラッシュの原因 (バグの確認コード) 内の場所を指します。

## <a name="when-reset-recovery-is-invoked"></a>回復のリセットが呼び出されるとき


回復のリセットが呼び出されたときに、ライブ カーネル ダンプを収集する機能で WDI の回復のリセット機能をビルドします。 カーネル ダンプでは、根本原因の事後調査することができます。 %Windir% ダンプが収集されるライブ カーネル\\LiveKernelDumps します。

### <a name="reset-recovery-triggers"></a>回復のトリガーをリセットします。

現在の復旧のリセットのトリガーは、以下に示します。 トリガーの詳細については、今後追加される可能性があります。

-   UE、LE に送信される WDI コマンド (M3) のタイムアウトを検出します。
-   UE WDI タスク (M4)、LE に送信のタイムアウトを検出します。
-   LE、検出し、ファームウェアのハングを示します。
-   ユーザー モードでは、リセットの回復を要求します。 これは現在のインターネット接続が切断に対してのみです。 NIC が接続されているし、インターネットに接続、wlansvc は、インターネットが失われるステート マシンを起動します。 インターネット接続が失われ、35 秒以内に回復できません場合、wlansvc が WDI リセットの回復を開始することを要求します。 35 秒のタイムアウトは、今後変更される可能性が。

### <a name="events-for-reset-recovery-triggers"></a>イベント トリガーのリセットの回復

WDI は、回復のリセットのトリガーを受信すると、システム イベント ログにエラー イベントを記録する NDIS を呼び出します。 イベントは LE 名であり、ID は 5002 です。 最後の 2 つの Dword は\[TriggerType、ActiveWdiCommand\]します。 現在のトリガーの種類は、以下に示します。

-   コマンド\_タイマー\_経過 (1)
-   タスク\_タイマー\_経過 (2)
-   リセット\_RECOVERY\_OID\_要求 (3)
-   リセット\_RECOVERY\_ファームウェア\_STALLED (4)

トリガーの種類がリセットされた場合、ActiveWdiCommand は 0 (アクティブなコマンドなし) にあります\_回復\_OID\_要求またはリセット\_RECOVERY\_ファームウェア\_STALLED します。

このスクリーン ショットは、eventvwr system.evtx を示す例を表示します。 トリガーの種類は 3 で、アクティブなコマンドはありません。

![wdi event log screenshot](images/wdi-event-log-screenshot.png)

## <a name="when-wi-fi-malfunctions"></a>Wi-fi が正しく動作しません。


クラッシュのない Wi-fi が期待どおりに機能しない場合は、収集し、トレース ログを分析します。 かどうか、問題は、WDI UE、LE、wlan に限定して\_dbg トレースに関しては、オペレーティング システムのイベントを表示するがあります。 Wlan\_dbg にプライベート シンボルのオペレーティング システムを必要とする WPP イベントが含まれています。 元の etl トレースは、予約されています、通信に含まれる必要があります。

## <a name="connected-standby-issues"></a>スタンバイの問題の接続


場合によっては、Wi-fi の NIC が省電力に移動できません (デバイス\_power\_状態\_Dx)。 それ以外の時間デバイス ウェイク アップ頻繁にします。 SleepStudy レポートは、最初のレベルのトリアージに便利です。 SleepStudy イベントが常に、動作が、CS セッションは 10 分を超える場合のみ収集されます。 イベントは永続的でも (たとえば、スタディ事後分析を検査することができます)。 SleepStudy を生成するには、管理者コマンド プロンプトで次のコマンドラインを実行します。

```CMD
Powercfg /SleepStudy
```

SleepStudy report.html をという名前のレポート ファイルが生成されます。 Windiir % の外部に開く必要があります\\システム。 レポートは、どのようなモジュールが非常に低電力状態 (DRIPS) からのシステムを維持することによって分割します。 さらにもコンポーネントが追いついて Wi-fi NIC (Dx) 外分類できることです。

 

 





