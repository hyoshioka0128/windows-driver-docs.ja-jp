---
title: プロセッサ電源管理 (PPM) の通知
description: 各プロセッサの電源管理 (PPM) 通知、PEP の AcceptProcessorNotification コールバック ルーチンを受信する通知の種類を示す通知パラメーターとデータ構造体を指すデータ パラメーターが付属します。指定した通知の種類の情報を格納します。
ms.assetid: 4BA89D0F-78F0-44DF-BC9B-0F9F3256CD59
keywords:
- AcceptProcessorNotification コールバック
ms.date: 01/17/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7a7e925c079a0b727c558c9020ce6a88e3fffaaf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369138"
---
# <a name="processor-power-management-ppm-notifications"></a>プロセッサ電源管理 (PPM) の通知
各プロセッサの電源管理 (PPM) 通知、PEP の AcceptProcessorNotification コールバック ルーチンを受信する通知の種類を示す通知パラメーターとデータ構造体を指すデータ パラメーターが付属します。指定した通知の種類の情報を格納します。

この呼び出しでは、通知のパラメーターは、通知の種類を示す PEP_NOTIFY_PPM_XXX 定数値に設定されます。 データのパラメーターは、この通知の種類に関連付けられている PEP_PPM_XXX 構造体型を指します。

次のプロセッサの電源管理 (PPM) 通知 Id は、AcceptProcessorNotification コールバック ルーチンで使用されます。

## <a name="pepnotifyppmquerycapabilities"></a>PEP_NOTIFY_PPM_QUERY_CAPABILITIES 
ターゲットのプロセッサに、PEP のデバイス ハンドルを含む処理 A PEPHANDLE 構造体。 通知では、特定のプロセッサを使用しない場合に、NULL がこれになります。

通知 PEP_NOTIFY_PPM_QUERY_CAPABILITIES 値。

データ。 PEP_PPM_QUERY_CAPABILITIES 構造へのポインター。
PEP、PEP の電源管理機能の照会されることを通知します。

Windows の電源管理フレームワーク (PoFx) は、PEP は、電源管理機能の照会されたときに、この通知を送信します。 これにより、プロセッサの初期化時に行われ、システムでプロセッサごとに送信されます。

X86 または AMD64 プロセッサを搭載したプラットフォームでは、プロセッサのパフォーマンス コントロールの ACPI インターフェイスを使用する必要があります。

PEP_NOTIFY_PPM_QUERY_CAPABILITIES 通知を送信するには、PoFx は、PEP の AcceptProcessorNotification コールバック ルーチンを呼び出します。 この呼び出しでは、通知のパラメーター値は、PEP_NOTIFY_PPM_QUERY_CAPABILITIES と PEP_PPM_QUERY_CAPABILITIES 構造体へのデータ パラメーターのポイントが。

AcceptProcessorNotification ルーチンに常に IRQL でと呼ばれる PEP_NOTIFY_PPM_QUERY_CAPABILITIES 通知、PASSIVE_LEVEL を = です。

PASSIVE_LEVEL
 
## <a name="pepnotifyppmqueryidlestates"></a>PEP_NOTIFY_PPM_QUERY_IDLE_STATES 
通知 PEP_NOTIFY_PPM_QUERY_IDLE_STATES 値。

データ。 PEP_PPM_QUERY_IDLE_STATES 構造へのポインター。
アイドル状態の詳細については、PEP を通知します。

PEP_NOTIFY_PPM_QUERY_IDLE_STATES 通知を送信するには、PoFx は、PEP の AcceptProcessorNotification コールバック ルーチンを呼び出します。 この呼び出しでは、通知のパラメーター値は、PEP_NOTIFY_PPM_QUERY_IDLE_STATES と PEP_PPM_QUERY_IDLE_STATES 構造体へのデータ パラメーターのポイントが。

AcceptProcessorNotification ルーチンに常に IRQL でと呼ばれる PEP_NOTIFY_PPM_QUERY_IDLE_STATES 通知、PASSIVE_LEVEL を = です。

PASSIVE_LEVEL
 
## <a name="pepnotifyppmidleselect"></a>PEP_NOTIFY_PPM_IDLE_SELECT 
通知 PEP_NOTIFY_PPM_IDLE_SELECT 値。

データ。 PEP_PPM_IDLE_SELECT 構造へのポインター。
アイドル状態の選択の PEP に通知します。

PEP_NOTIFY_PPM_IDLE_SELECT 通知を送信するには、PoFx は、PEP の AcceptProcessorNotification コールバック ルーチンを呼び出します。 この呼び出しでは、通知のパラメーター値は、PEP_NOTIFY_PPM_IDLE_SELECT と PEP_PPM_IDLE_SELECT 構造体へのデータ パラメーターのポイントが。

AcceptProcessorNotification ルーチンに常に IRQL でと呼ばれる PEP_NOTIFY_PPM_IDLE_SELECT 通知、PASSIVE_LEVEL を = です。

PASSIVE_LEVEL
 
## <a name="pepnotifyppmidlecancel"></a>PEP_NOTIFY_PPM_IDLE_CANCEL 
通知 PEP_NOTIFY_PPM_IDLE_CANCEL 値。

データ。 PEP_PPM_IDLE_CANCEL 構造へのポインター。
キャンセル操作の PEP に通知します。

PEP_NOTIFY_PPM_IDLE_CANCEL 通知を送信するには、PoFx は、PEP の AcceptProcessorNotification コールバック ルーチンを呼び出します。 この呼び出しでは、通知のパラメーター値は、PEP_NOTIFY_PPM_IDLE_CANCEL と PEP_PPM_IDLE_CANCEL 構造体へのデータ パラメーターのポイントが。

AcceptProcessorNotification ルーチンに常に IRQL でと呼ばれる PEP_NOTIFY_PPM_IDLE_CANCEL 通知、PASSIVE_LEVEL を = です。

PASSIVE_LEVEL
 
## <a name="pepnotifyppmidleexecute"></a>PEP_NOTIFY_PPM_IDLE_EXECUTE 
ターゲットのプロセッサに、PEP のデバイス ハンドルを含む処理 A PEPHANDLE 構造体。 通知では、特定のプロセッサを使用しない場合に、NULL がこれになります。

通知 PEP_NOTIFY_PPM_IDLE_EXECUTE 値。

PEP_PPM_IDLE_EXECUTE または PEP_PPM_IDLE_EXECUTE_V2 構造体へのデータ。 ポインター。
現在のプロセッサを指定のアイドル状態に遷移する PEP に送信されます。

Windows の電源管理フレームワーク (PoFx) では、現在のプロセッサを指定のアイドル状態に遷移する PEP にこの通知を送信します。 

PEP では、スリープ状態の移行で影響を受ける可能性がありますコア システム リソースの OS を通知するなど、以前に選択したアイドル状態にハードウェアを準備することができます。 プロセッサ アイドル状態に遷移する停止命令を実行にする必要があります。 関数がアイドル状態から戻るとき、PEP は、OS のスリープ解除時にアクティブになる可能性があります、コア システムのリソースへの通知など、ハードウェアのセットアップを取り消す必要があります。 場合は、PEP はエラー状態に返す必要があり、プロセッサ (およびプラットフォーム) のアイドル状態を実行できません。

アイドル状態の連携のとれたインターフェイスを使用する場合、OS は、アイドル状態の遷移によって入力される調整のアイドル状態の一覧でフィールドの CoordinatedStateCount と CoordinatedState フィールドを含む PEP_PPM_IDLE_EXECUTE_V2 構造体を使用します。 存在する場合、PlatformState フィールドは入力されている最下位のプラットフォームの調整のアイドル状態を指定します。 

アイドル状態の連携のとれたインターフェイスを使用していないときに、OS は PEP_PPM_IDLE_EXECUTE 構造体を使用します。 

PEP_NOTIFY_PPM_IDLE_EXECUTE 通知に割り込みを無効になっている AcceptProcessorNotification ルーチンが呼び出されます。
 
## <a name="pepnotifyppmidlecomplete"></a>PEP_NOTIFY_PPM_IDLE_COMPLETE 
ターゲットのプロセッサに、PEP のデバイス ハンドルを含む処理 A PEPHANDLE 構造体。 

通知 PEP_NOTIFY_PPM_IDLE_COMPLETE 値。

PEP_PPM_IDLE_COMPLETE または PEP_PPM_IDLE_COMPLETE_V2 構造体へのポインターをデータ A.
PEP に、現在のプロセッサがアイドル状態の遷移を完了したからウェイク アップすることを通知します。

Windows の電源管理フレームワーク (PoFx) は、現在のプロセッサがアイドル状態の遷移を完了したからウェイク アップするときに、この通知を送信します。 プラットフォームには、プラットフォームのアイドル状態の移行が実行されていた場合、ウェイクするための最初のプロセッサは終了されているプラットフォームのアイドル状態を示します。 、プラットフォームのアイドル状態の移行で使用される同期の種類に応じて、最初のプロセッサ プラットフォームのアイドル状態からの復帰をしても、プラットフォームのアイドル状態にするプロセッサ可能性がありますできません。 

プロセッサには、詳細なアイドル状態が実行されていた場合、PEP がコアのコンテキストを復元するか、またはコア リソースが復元されたことを OS に通知する完了通知を受信するまで待機する必要があります。 OS には、execute 通知が完了すると、復元されているこれらのリソースが必要です。 ハイパーバイザーが有効にすると、PEP のみ通知を受け取る終了時に PEP_PROCESSOR_IDLE_STATE_UNKNOWN に設定された ProcessorState フィールドとプラットフォームのアイドル状態から。 

アイドル状態の連携のとれたインターフェイスを使用する場合、OS はアイドル状態の遷移によって終了する調整のアイドル状態の一覧で、CoordinatedStateCount と CoordinatedState のフィールドを含む PEP_PPM_IDLE_COMPLETE_V2 構造を使用します。 存在する場合、PlatformState フィールドはから、抜けている最下位のプラットフォームの調整のアイドル状態を指定します。 緩やかな同期が使用されている場合このプロセッサで終了する調整のアイドル状態のセットが入力した、連携のとれたのアイドル状態のセットから異なる場合がありますに注意してください。 

アイドル状態の連携のとれたインターフェイスを使用していないときに、OS は PEP_PPM_IDLE_COMPLETE 構造体を使用します。 

PEP_NOTIFY_PPM_IDLE_COMPLETE 通知の場合は、AcceptProcessorNotification ルーチンは、割り込みを無効にして、呼び出すし、ターゲット プロセッサでは常に実行します。
 
## <a name="pepnotifyppmisprocessorhalted"></a>PEP_NOTIFY_PPM_IS_PROCESSOR_HALTED 
ターゲットのプロセッサに、PEP のデバイス ハンドルを含む処理 A PEPHANDLE 構造体。 通知では、特定のプロセッサを使用しない場合に、NULL がこれになります。

通知 PEP_NOTIFY_PPM_IS_PROCESSOR_HALTED 値。

データ。 PEP_PPM_IS_PROCESSOR_HALTED 構造へのポインター。
指定したプロセッサが選択されているアイドル状態で中断されているかどうかを決定する、PEP に送信されます。

Windows の電源管理フレームワーク (PoFx) では、指定したプロセッサが選択されているアイドル状態で中断されているかどうかを判断する PEP にこの通知を送信します。 OS では、この通知を使用して、セカンダリのプロセッサがアイドル状態のプラットフォームを調整するときにアイドル状態に遷移を完全に完了かどうか確認してください。 PEP は、ターゲットのプロセッサ (など、コアは停止してハードウェア レジスタをチェック) によって発生安全にプラットフォームのアイドル状態の遷移を状態に達したことを保証する必要があります。 この通知は、プロセッサがアイドル状態になったことを示します、いったんそのプロセッサする必要がありますウェイク アップしないようには、OS が明示的に要求しない限り。 

PEP は、IDLE_SELECT と IDLE_COMPLETE 通知の間でいつでもこの通知が表示されます。 アイドル状態の遷移中に最大で 1 回この通知を受け取ることが保証されます。 

PEP_NOTIFY_PPM_IS_PROCESSOR_HALTED 通知の場合は、AcceptProcessorNotification ルーチンは、IRQL で、割り込みを無効になっている、任意の IRQL では呼び出され、ターゲット プロセッサでは実行されません。

&LT; HIGH_LEVEL を =
 
## <a name="pepnotifyppminitiatewake"></a>PEP_NOTIFY_PPM_INITIATE_WAKE 
ターゲットのプロセッサに、PEP のデバイス ハンドルを含む処理 A PEPHANDLE 構造体。

通知 PEP_NOTIFY_PPM_INITIATE_WAKE 値。

構造体へのデータ。 ポインター。
中断不可能なアイドル状態からのスリープ解除を開始する指定されたプロセッサの PEP に送信されます。

Windows の電源管理フレームワーク (PoFx) を中断不可能なアイドル状態からのスリープ解除を開始する指定されたプロセッサの PEP にこの通知を送信します。 PEP は、NeedInterruptForCompletion を使用してターゲットのプロセッサにウェイク アップの状態を返す必要があります。 プロセッサがアイドル状態からのウェイク アップを終了する割り込みが必要な場合は TRUE を返します。 ここで、PEP は、ターゲット プロセッサは、この通知を処理からの戻り時に中断が可能なことを確認する必要があります。 ターゲット プロセッサが既に実行中や、最終的には、アイドル状態の終了 (またはが行う処理中) の生成ソフトウェア割り込みを必要とせず NeedInterruptForCompletion を FALSE に設定する必要があります。


注、PEP は、同じプロセッサをこの通知を同時に受信しません。
 

PEP_NOTIFY_PPM_INITIATE_WAKE 通知の場合は、AcceptProcessorNotification ルーチンに割り込みを無効になっている、任意の IRQL で呼び出され、ターゲット プロセッサでは実行されません。

&LT; HIGH_LEVEL を =
 
## <a name="pepnotifyppmqueryfeedbackcounters"></a>PEP_NOTIFY_PPM_QUERY_FEEDBACK_COUNTERS 
ターゲットのプロセッサに、PEP のデバイス ハンドルを含む処理 A PEPHANDLE 構造体。 通知では、特定のプロセッサを使用しない場合に、NULL がこれになります。

通知 PEP_NOTIFY_PPM_QUERY_FEEDBACK_COUNTERS 値。

データ。 PEP_PPM_QUERY_FEEDBACK_COUNTERS 構造へのポインター。
サポートされているフィードバック カウンターの一覧については、PEP が照会されることを PEP に通知します。

Windows 電源管理フレームワーク (PoFx) は、プロセッサの初期化をサポートしているフィードバック カウンターの一覧については、PEP の照会でこの通知を送信します。

AcceptProcessorNotification ルーチンに常に IRQL でと呼ばれる PEP_NOTIFY_PPM_QUERY_FEEDBACK_COUNTERS 通知、PASSIVE_LEVEL を = です。

PASSIVE_LEVEL
 
## <a name="pepnotifyppmfeedbackread"></a>PEP_NOTIFY_PPM_FEEDBACK_READ 
ターゲットのプロセッサに、PEP のデバイス ハンドルを含む処理 A PEPHANDLE 構造体。 通知では、特定のプロセッサを使用しない場合に、NULL がこれになります。

通知 PEP_NOTIFY_PPM_FEEDBACK_READ 値。

データ。 PEP_PPM_FEEDBACK_READ 構造へのポインター。
フィードバック カウンターの現在の値のクエリが対象に、PEP を通知します。

Windows の電源管理フレームワーク (PoFx) は、フィードバック カウンターの現在の値を照会する必要がある場合、この通知を送信します。 

割り込みを無効になっているこの通知を送信できます。 カウンターの Affinitized フィールドが設定されている場合、この通知は、ターゲット プロセッサで実行されます。 それ以外の場合、この通知は、すべてのプロセッサから実行することがあります。

PEP_NOTIFY_PPM_FEEDBACK_READ 通知の場合、IRQL で AcceptProcessorNotification ルーチンを呼び出すことができます = DISPATCH_LEVEL します。

DISPATCH_LEVEL
 
## <a name="pepnotifyppmqueryperfcapabilities"></a>PEP_NOTIFY_PPM_QUERY_PERF_CAPABILITIES 
ターゲットのプロセッサに、PEP のデバイス ハンドルを含む処理 A PEPHANDLE 構造体。 通知では、特定のプロセッサを使用しない場合に、NULL がこれになります。

通知 PEP_NOTIFY_PPM_QUERY_PERF_CAPABILITIES 値。

データ。 PEP_PPM_QUERY_PERF_CAPABILITIES 構造へのポインター。
プラットフォームでサポートされているパフォーマンスの範囲内のクエリが対象に、PEP を通知します。

Windows 電源管理フレームワーク (PoFx) は、クエリ パフォーマンスの範囲をプラットフォームでサポートされているプロセッサの初期化でこの通知を送信します。 PEP_PPM_QUERY_PERF_CAPABILITIES 構造体の DomainId と DomainMembers のフィールドは、プラットフォームにパフォーマンスの状態のドメインを表すために使用されます。 各プロセッサは、1 つだけのパフォーマンス状態のドメインのメンバーです。 オペレーティング システムは、パフォーマンスのドメインのすべてのプロセッサがまとめてパフォーマンスを変更することを確認します。 

AcceptProcessorNotification ルーチンに常に IRQL でと呼ばれる PEP_NOTIFY_PPM_QUERY_PERF_CAPABILITIES 通知、PASSIVE_LEVEL を = です。

PASSIVE_LEVEL
 
## <a name="pepnotifyppmperfconstraints"></a>PEP_NOTIFY_PPM_PERF_CONSTRAINTS 
ターゲットのプロセッサに、PEP のデバイス ハンドルを含む処理 A PEPHANDLE 構造体。 

通知 PEP_NOTIFY_PPM_PERF_CONSTRAINTS 値。

データ。 PEP_PPM_PERF_CONSTRAINTS 構造へのポインター。
プロセッサの現在操作上の制約のクエリが対象に、PEP を通知します。

Windows の電源管理フレームワーク (PoFx) は、プロセッサの現在操作上の制約を検査する必要がある場合、この通知を送信します。 PEP では、コントロール コード GUID_PPM_PERF_CONSTRAINT_CHANGE で電源管理を実行することによって、プロセッサのパフォーマンスの制約を再評価する OS の要求を開始します。 InBuffer および OutBuffer NULL にする必要があります。 

PEP は、プロセッサの電源制御トランザクションを発行する前に、プロセッサの PEP_DPM_DEVICE_STARTED 通知を受信するまで待つ必要があります。 

AcceptProcessorNotification ルーチンに常に IRQL でと呼ばれる PEP_NOTIFY_PPM_PERF_CONSTRAINTS 通知、PASSIVE_LEVEL を = です。

PASSIVE_LEVEL
 
## <a name="pepnotifyppmperfset"></a>PEP_NOTIFY_PPM_PERF_SET 
ターゲットのプロセッサに、PEP のデバイス ハンドルを含む処理 A PEPHANDLE 構造体。 通知では、特定のプロセッサを使用しない場合に、NULL がこれになります。

通知 PEP_NOTIFY_PPM_PERF_SET 値。

データ。 PEP_PPM_PERF_SET 構造へのポインター。
PEP に、プロセッサの現在の操作のパフォーマンスを変更する必要があることを通知します。

Windows の電源管理フレームワーク (PoFx) は、プロセッサの現在の業績を変更する必要がある場合、この通知を送信します。 すべてのプロセッサ上の実行中には、この通知を送信できます。

AcceptProcessorNotification ルーチンに常に IRQL でと呼ばれる、PEP_NOTIFY_PPM_PERF_SET 通知 DISPATCH_LEVEL を = です。

DISPATCH_LEVEL
 
## <a name="pepnotifyppmparkselection"></a>PEP_NOTIFY_PPM_PARK_SELECTION 
ターゲットのプロセッサに、PEP のデバイス ハンドルを含む処理 A PEPHANDLE 構造体。 通知では、特定のプロセッサを使用しない場合に、NULL がこれになります。

通知 PEP_NOTIFY_PPM_PARK_SELECTION 値。

データ。 PEP_PPM_PARK_SELECTION 構造へのポインター。
PEP に OS を指定ようで保管するにプロセッサ コアの推奨セットを選択することを通知します。

Windows の電源管理フレームワーク (PoFx) は、PEP のコア パーキングする推奨セットを選択するように指示するには、この通知を送信します。

2 つの関数を実行する、PEP_NOTIFY_PPM_PARK_SELECTION がオーバー ロードされています。 

(システムのすべてのプロセッサのセット) からプロセッサを保持する必要があります、PEP の選択を使用して、保留中ルーティングするがあります。 PEP の選択 (保留中ルーティングではないすべてのプロセッサのセット) からプロセッサに割り込みを受信する必要があり、割り込みを受け取ってはならないことができます。 Windows では、OS を実行する 2 つの識別するために、PEP の手段が提供されません。 結果として、PEP では、特定の一連の入力 (AdditionalUnparkedProcessors 数と PoPreference) では、この通知を受信すると、何らかの外部イベントの PEP の基本設定が変更しない限り、一貫性のある出力 (PepPreference) を提供する必要があります。 

AcceptProcessorNotification ルーチンに常に IRQL でと呼ばれる、PEP_NOTIFY_PPM_PARK_SELECTION 通知 DISPATCH_LEVEL を = です。

DISPATCH_LEVEL
 
## <a name="pepnotifyppmcststates"></a>PEP_NOTIFY_PPM_CST_STATES 
ターゲットのプロセッサに、PEP のデバイス ハンドルを含む処理 A PEPHANDLE 構造体。 通知では、特定のプロセッサを使用しない場合に、NULL がこれになります。

通知 PEP_NOTIFY_PPM_CST_STATES 値。

データ。 PEP_PPM_CST_STATES 構造へのポインター。
ACPI 定義 C-状態のプロセッサでサポートされているセットを示すために、PEP に送信します。 

Windows 電源管理フレームワーク (PoFx) は、ACPI 定義 C-状態のプロセッサでサポートされているセットを示すために PEP にこの通知を送信します。 この通知が最初に、PEP は、プロセッサの PEP_NOTIFY_PPM_QUERY_IDLE_STATES_V2 通知を受信する前に 1 回送信される送受信もう一度いつでもそのプロセッサ _CST オブジェクトが変更されたことを示す Notify(0x81) します。

AcceptProcessorNotification ルーチンに常に IRQL でと呼ばれる PEP_NOTIFY_PPM_CST_STATES 通知、PASSIVE_LEVEL を = です。

PASSIVE_LEVEL
 
## <a name="pepnotifyppmqueryplatformstates"></a>PEP_NOTIFY_PPM_QUERY_PLATFORM_STATES 
ターゲットのプロセッサに、PEP のデバイス ハンドルを含む処理 A PEPHANDLE 構造体。 通知では、特定のプロセッサを使用しない場合に、NULL がこれになります。

通知 PEP_NOTIFY_PPM_QUERY_PLATFORM_STATES 値。

データ。 PEP_PPM_QUERY_PLATFORM_STATES 構造へのポインター。
PEP をサポートするプラットフォームのアイドル状態の数を照会するプロセッサの初期化に送信されます。

Windows 電源管理フレームワーク (PoFx) は、サポートされるプラットフォームのアイドル状態の数を照会するプロセッサの初期化時、PEP にこの通知を送信します。 この通知は、ブート時に 1 回送信されます。 0 以外のプラットフォームの状態数が返された後、PEP を開始するプロセッサのアイドル状態の遷移中にアイドル状態のプラットフォームを選択します。

AcceptProcessorNotification ルーチンに常に IRQL でと呼ばれる PEP_NOTIFY_PPM_QUERY_PLATFORM_STATES 通知、PASSIVE_LEVEL を = です。

PASSIVE_LEVEL
 
## <a name="pepnotifyppmquerylpsettings"></a>PEP_NOTIFY_PPM_QUERY_LP_SETTINGS 
通知 PEP_NOTIFY_PPM_QUERY_LP_SETTINGS 値。

データ。 PEP_PPM_QUERY_LP_SETTINGS 構造へのポインター。
PEP_NOTIFY_PPM_QUERY_LP_SETTINGS 通知を送信するには、PoFx は、PEP の AcceptProcessorNotification コールバック ルーチンを呼び出します。 この呼び出しでは、通知のパラメーター値は、PEP_NOTIFY_PPM_QUERY_LP_SETTINGS と PEP_PPM_QUERY_LP_SETTINGS 構造体へのデータ パラメーターのポイントが。

AcceptProcessorNotification ルーチンに常に IRQL でと呼ばれる PEP_NOTIFY_PPM_QUERY_LP_SETTINGS 通知、PASSIVE_LEVEL を = です。

PASSIVE_LEVEL
 
## <a name="pepnotifyppmqueryidlestatesv2"></a>PEP_NOTIFY_PPM_QUERY_IDLE_STATES_V2 
ターゲットのプロセッサに、PEP のデバイス ハンドルを含む処理 A PEPHANDLE 構造体。 通知では、特定のプロセッサを使用しない場合に、NULL がこれになります。

通知 PEP_NOTIFY_PPM_QUERY_IDLE_STATES_V2 値。

データ。 PEP_PPM_QUERY_IDLE_STATES_V2 構造へのポインター。
プロセッサの初期化時、PEP をサポートするアイドル状態の一覧を照会するために使用します。

Windows 電源管理フレームワーク (PoFx) は、この通知をサポートしているアイドル状態の一覧のクエリ プロセッサの初期化時、PEP に送信します。 

Count メンバーには、アイドル状態の配列のサイズを指定します。 プロセッサのドライバーは、この通知を送信する前に、PEP_NOTIFY_PPM_QUERY_CAPABILITIES でアイドル状態の数を照会します。 

PEP は、サポートされる各アイドル状態に関する情報を IdleStates 配列に格納します。 アイドル状態の状態は、電源/消費量を増やすの移行コストが高い順に一覧に表示する必要があります。 PEP は、各プロセッサのアイドル状態の同じ一覧を報告する必要はありません。 

AcceptProcessorNotification ルーチンに常に IRQL でと呼ばれる PEP_NOTIFY_PPM_QUERY_IDLE_STATES_V2 通知、PASSIVE_LEVEL を = です。

PASSIVE_LEVEL
 
## <a name="pepnotifyppmqueryplatformstate"></a>PEP_NOTIFY_PPM_QUERY_PLATFORM_STATE 
ターゲットのプロセッサに、PEP のデバイス ハンドルを含む処理 A PEPHANDLE 構造体。 通知では、特定のプロセッサを使用しない場合に、NULL がこれになります。

通知 PEP_NOTIFY_PPM_QUERY_PLATFORM_STATE 値。

データ。 PEP_PPM_QUERY_PLATFORM_STATE 構造へのポインター。
1 つのプラットフォームのアイドル状態のプロパティを照会する PEP に送信されます。

Windows 電源管理フレームワーク (PoFx) は、1 つのプラットフォームのアイドル状態のプロパティを照会するプロセッサの初期化でこの通知を送信します。 

PEP_PPM_QUERY_PLATFORM_STATE 構造体の StateIndex パラメーターは、クエリ対象のプラットフォームのアイドル状態のインデックスを指定します。 プロセッサのドライバーは、この通知を送信する前に、PEP_NOTIFY_PPM_QUERY_PLATFORM_STATES でサポートされているプラットフォームのアイドル状態の数を照会します。 そうすると、プロセッサのドライバーでは、各プラットフォームのアイドル状態の 1 つの PEP_NOTIFY_PPM_QUERY_PLATFORM_STATE 通知が送付されます。 プロセッサのドライバーは、PEP のすべてのプロセッサが登録された後までには、この通知の送信を待機します。 

PEP は、プラットフォームのアイドル状態に関する情報を状態構造体に格納します。 プラットフォームのアイドル状態は、電源/消費量を増やすの移行コストが高い順に表示する必要があります。 

AcceptProcessorNotification ルーチンに常に IRQL でと呼ばれる PEP_NOTIFY_PPM_QUERY_PLATFORM_STATE 通知、PASSIVE_LEVEL を = です。

PASSIVE_LEVEL
 
## <a name="pepnotifyppmtestidlestate"></a>PEP_NOTIFY_PPM_TEST_IDLE_STATE 
ターゲットのプロセッサに、PEP のデバイス ハンドルを含む処理 A PEPHANDLE 構造体。 通知では、特定のプロセッサを使用しない場合に、NULL がこれになります。

通知 PEP_NOTIFY_PPM_TEST_IDLE_STATE 値。

データ。 PEP_PPM_TEST_IDLE_STATE 構造へのポインター。
指定されたプロセッサのプロセッサやプラットフォームの指定されたアイドル状態が入力するかどうかをテストするために使用します。

Windows の電源管理フレームワーク (PoFx) は、指定されたプロセッサのプロセッサやプラットフォームの指定されたアイドル状態が入力するかどうかをテストするには、この通知を送信します。 アイドル状態を入力できる場合、PEP は拒否コード PEP_IDLE_VETO_NONE を入力し、アイドル状態の移行を完了します。 何らかの理由によりアイドル状態の移行を完了できない場合、PEP は、0 以外の拒否コードに格納します。 

0x80000000 を 0 xffffffff の範囲の重要なの拒否コードは、OS の使用状況のために予約されており、使用することはできません。
 

この通知が送信されるときに、OS は既に検証プラットフォーム アイドル状態に移行するためのデバイスとプロセッサの制約を含む、プロセッサやプラットフォームの選択されているアイドル状態に関連付けられているすべての制約を満たしていること。 

OS は enterable が常にあります。 プロセッサまたはプロセッサのアイドル状態をインデックス 0 の場合を除き、プラットフォームのアイドル状態を入力する前に、この通知が送信されます。 PEP_IDLE_VETO_NONE でこの通知を完了しても、OS が指定されたアイドル状態を入力するとは限りません。 この通知に割り込みを無効になっています。 この通知は常に、ターゲット プロセッサで実行されます。 

PEP_NOTIFY_PPM_TEST_IDLE_STATE 通知に割り込みを無効になっている AcceptProcessorNotification ルーチンが呼び出されます。
 
## <a name="pepnotifyppmidlepreexecute"></a>PEP_NOTIFY_PPM_IDLE_PRE_EXECUTE 
ターゲットのプロセッサに、PEP のデバイス ハンドルを含む処理 A PEPHANDLE 構造体。 通知では、特定のプロセッサを使用しない場合に、NULL がこれになります。

通知 PEP_NOTIFY_PPM_IDLE_PRE_EXECUTE 値。

PEP_PPM_IDLE_EXECUTE または PEP_PPM_IDLE_EXECUTE_V2 構造体へのデータ。 ポインター。
指定されたアイドル状態に遷移するシステムを準備する、PEP に送信されます。

Windows の電源管理フレームワーク (PoFx) では、指定されたアイドル状態に遷移するシステムを準備する PEP にこの通知を送信します。 OS がプロセッサを移行のこの通知が正常に完了すると、関連付けられた C 状態を入力してアイドル状態にします。 PEP がない場合はエラー状態に返す必要がありますし、プロセッサ (およびプラットフォーム) のアイドル状態にシステムを準備できません。 

ハイパーバイザーが有効にすると、PEP はのみに PEP_PROCESSOR_IDLE_STATE_UNKNOWN 設定 ProcessorState フィールドとプラットフォームのアイドル状態に入ったときにこの通知を受信します。 

アイドル状態の連携のとれたインターフェイスを使用する場合、OS は、アイドル状態の遷移によって入力される調整のアイドル状態の一覧でフィールドの CoordinatedStateCount と CoordinatedState フィールドを含む PEP_PPM_IDLE_EXECUTE_V2 構造体を使用します。 存在する場合、PlatformState フィールドは入力されている最下位のプラットフォームの調整のアイドル状態を指定します。 

アイドル状態の連携のとれたインターフェイスを使用していないときに、OS は PEP_PPM_IDLE_EXECUTE 構造体を使用します。 

PEP_NOTIFY_PPM_IDLE_PRE_EXECUTE 通知の場合は、AcceptProcessorNotification ルーチンは、割り込みを無効にして、呼び出すし、ターゲット プロセッサでは常に実行します。
 
## <a name="pepnotifyppmupdateplatformstate"></a>PEP_NOTIFY_PPM_UPDATE_PLATFORM_STATE 
ターゲットのプロセッサに、PEP のデバイス ハンドルを含む処理 A PEPHANDLE 構造体。 通知では、特定のプロセッサを使用しない場合に、NULL がこれになります。

通知 PEP_NOTIFY_PPM_UPDATE_PLATFORM_STATE 値。

データ。 PEP_PPM_QUERY_PLATFORM_STATE 構造へのポインター。
PEP にプロセッサがプラットフォームのアイドル状態の特性を更新する Notify(0x81) を受け取ったことを通知します。

Windows の電源管理フレームワーク (PoFx) は、プロセッサがプラットフォームのアイドル状態の特性を更新する Notify(0x81) を受信したときに、この通知を送信します。 この通知は、各プラットフォームのアイドル状態の 1 回送信されます。 PEP が通知 (つまり、AcceptProcessorNotification コールバックから返します FALSE) を受け付けない場合、プラットフォームのアイドル状態最近からの以前の定義が受け入れられます PEP_NOTIFY_PPM_QUERY_PLATFORM_STATE または PEP_NOTIFY_PPM_UPDATE_PLATFORM_STATE の通知が保持されます。 

この通知は、PEP_NOTIFY_PPM_QUERY_PLATFORM_STATE 通知として同じデータ バッファーを使用します。 

AcceptProcessorNotification ルーチンに常に IRQL でと呼ばれる PEP_NOTIFY_PPM_UPDATE_PLATFORM_STATE 通知、PASSIVE_LEVEL を = です。

PASSIVE_LEVEL
 
## <a name="pepnotifyppmqueryplatformstateresidencies"></a>PEP_NOTIFY_PPM_QUERY_PLATFORM_STATE_RESIDENCIES 
ターゲットのプロセッサに、PEP のデバイス ハンドルを含む処理 A PEPHANDLE 構造体。 通知では、特定のプロセッサを使用しない場合に、NULL がこれになります。

通知 PEP_NOTIFY_PPM_QUERY_PLATFORM_STATE_RESIDENCIES 値。

データ。 PEP_PPM_PLATFORM_STATE_RESIDENCIES 構造へのポインター。
起動後に、各プラットフォームのアイドル状態に費やされた実際の累積時間をキャプチャする必要がありますが、PEP を通知します。

Windows 電源管理フレームワーク (PoFx) は、起動後に、各プラットフォームのアイドル状態に費やされた実際の累積時間をキャプチャする PEP にこの通知を送信します。 そのため、このクエリはのみプラットフォームに適用される、基になるハードウェアは、アイドル状態、OS によって要求から別のプラットフォームを入力する必要があります自律的に。 返される値は、診断のために使用し、プラットフォームのアイドル状態の保存場所の OS のビュー大きく異なる場合、プラットフォームが実際に実現を特定します。 

カウントは、要素のインデックスがプラットフォームのアイドル状態のインデックスに対応する場所、状態配列内の要素の数を指定します。 PEP は各要素と一致する状態の実際の保存場所と遷移の数を入力します。 


このクエリによってキャプチャされた値を累計は、その期間、PEP (またはプロセッサ ドライバー) 実際に実行プラットフォーム アイドル状態の遷移のみに対応する必要がありますに注意してください。 これにより、OS の計算される保存場所と実際の保存場所間の比較が意味のあることが保証されます。
 

PEP_NOTIFY_PPM_QUERY_PLATFORM_STATE_RESIDENCIES 通知の場合、IRQL で AcceptProcessorNotification ルーチンを呼び出すことができます。
 
## <a name="pepnotifyppmqueryvetoreasons"></a>PEP_NOTIFY_PPM_QUERY_VETO_REASONS 
ターゲットのプロセッサに、PEP のデバイス ハンドルを含む処理 A PEPHANDLE 構造体。 通知では、特定のプロセッサを使用しない場合に、NULL がこれになります。

通知 PEP_NOTIFY_PPM_QUERY_VETO_REASONS 値。

データ。 PEP_PPM_QUERY_VETO_REASONS 構造へのポインター。
ProcessorIdleVeto と PlatformIdleVeto コールバックで、PEP を使用する一意の拒否理由の数を照会するために使用します。 

Windows 電源管理フレームワーク (PoFx) は、ProcessorIdleVeto と PlatformIdleVeto コールバックで、PEP を使用する一意の拒否理由の数を照会するプロセッサの初期化でこの通知を送信します。 この通知はオプションであり、PEP を無視できます。 

受け入れられると、PEP は、プロセッサ、プラットフォーム、またはアイドル状態の調整を拒否するには、1 ~ VetoReasonCount、包括的で拒否の理由を使用して許可されます。 PEP は拒否理由 VetoReasonCount よりも大きい値を使用できません。 OS は、構造体を追跡拒否を事前に割り当てて、PEP_NOTIFY_PPM_ENUMERATE_BOOT_VETOES を併用すると、すべてのプロセッサ、プラットフォーム、および調整の状態がコールバックを拒否することの保証は成功します。

この通知は、PEP では許容されません、PEP は、法的な拒否の理由で ProcessorIdleVeto と PlatformIdleVeto コールバックを使用できます。 OS では、割り当てエラーまたはその他の問題のためのコールバックが失敗しないようにすることは限りません。

AcceptProcessorNotification ルーチンに常に IRQL でと呼ばれる PEP_NOTIFY_PPM_QUERY_VETO_REASONS 通知、PASSIVE_LEVEL を = です。

PASSIVE_LEVEL
 
## <a name="pepnotifyppmqueryvetoreason"></a>PEP_NOTIFY_PPM_QUERY_VETO_REASON 
ターゲットのプロセッサに、PEP のデバイス ハンドルを含む処理 A PEPHANDLE 構造体。 通知では、特定のプロセッサを使用しない場合に、NULL がこれになります。

通知 PEP_NOTIFY_PPM_QUERY_VETO_REASON 値。

データ。 PEP_PPM_QUERY_VETO_REASON 構造へのポインター。
特定の拒否の理由については、クエリに PEP に送信されます。

Windows の電源管理フレームワーク (PoFx) では、特定の拒否理由に関する情報を照会するプロセッサの初期化の時点でこの通知を送信します。 この通知は、名前の内容を埋めるために拒否の理由、名前に必要な割り当てサイズを取得する NULLName バッファーが 1 回および非 NULLName バッファーが 1 回の 2 回送信されます。 名前は、この拒否の理由を表す条件を示す、人間が判読できる文字列にする必要があります。 WPA およびカーネル デバッガーなどのデバッグ ツールがアイドル状態が入力されなかった理由を診断するときに名前が表示されます。 

AcceptProcessorNotification ルーチンに常に IRQL でと呼ばれる PEP_NOTIFY_PPM_QUERY_VETO_REASON 通知、PASSIVE_LEVEL を = です。

PASSIVE_LEVEL
 
## <a name="pepnotifyppmenumeratebootvetoes"></a>PEP_NOTIFY_PPM_ENUMERATE_BOOT_VETOES 
ターゲットのプロセッサに、PEP のデバイス ハンドルを含む処理 A PEPHANDLE 構造体。 通知では、特定のプロセッサを使用しない場合に、NULL がこれになります。

通知 PEP_NOTIFY_PPM_ENUMERATE_BOOT_VETOES 値。

データが NULL ポインターの値。
PEP に OS が ProcessorIdleVeto または PlatformIdleVeto への呼び出しを受け入れる準備ができていることを通知します。 

Windows の電源管理フレームワーク (PoFx) では、OS が ProcessorIdleVeto または PlatformIdleVeto への呼び出しを受け入れる準備ができていることを示すこの通知がプロセッサの初期化後アイドル状態の最初のエントリの前に送信します。 この通知のコンテキストで任意の起動時に vetoes を列挙できるは、PEP と OS では、プロセッサ、プラットフォーム、またはアイドル状態の調整を選択する最初の試行する前に有効にならないことが保証されます。 この通知に関連付けられているデータのパラメーターがありません。 

AcceptProcessorNotification ルーチンに常に IRQL でと呼ばれる PEP_NOTIFY_PPM_ENUMERATE_BOOT_VETOES 通知、PASSIVE_LEVEL を = です。

PASSIVE_LEVEL
 
## <a name="pepnotifyppmparkmask"></a>PEP_NOTIFY_PPM_PARK_MASK 
ターゲットのプロセッサに、PEP のデバイス ハンドルを含む処理 A PEPHANDLE 構造体。 通知では、特定のプロセッサを使用しない場合に、NULL がこれになります。

通知 PEP_NOTIFY_PPM_PARK_MASK 値。

データ。 PEP_PPM_PARK_MASK 構造へのポインター。
現在のコア パーキング マスクの PEP に通知します。

Windows 電源管理フレームワーク (PoFx) は、現在のコア パーキング マスクの PEP を通知するために、実行時にこの通知を送信します。

IRQL で PEP_NOTIFY_PPM_PARK_MASK 通知の場合、AcceptProcessorNotification ルーチンと呼ばれる = DISPATCH_LEVEL とすべてのプロセッサ上の実行中に送信することがあります。

DISPATCH_LEVEL
 
## <a name="pepnotifyppmparkselectionv2"></a>PEP_NOTIFY_PPM_PARK_SELECTION_V2 
ターゲットのプロセッサに、PEP のデバイス ハンドルを含む処理 A PEPHANDLE 構造体。 通知では、特定のプロセッサを使用しない場合に、NULL がこれになります。

通知 PEP_NOTIFY_PPM_PARK_SELECTION_V2 値。

データ。 PEP_PPM_PARK_SELECTION_V2 構造へのポインター。
コアが駐車またはからの割り込みを進めるための推奨セットを選択することを OS でなどは、PEP を通知します。 この通知を承認されない場合、OS がフォールバック PEP_NOTIFY_PPM_PARK_SELECTION 通知を送信します。

パフォーマンス チェックのアルゴリズムを実行するときに、OS が通知を送信 PEP_NOTIFY_PPM_PARK_SELECTION_V2 複数回: 各パーク ドメイン環境および 0 の core 効率クラスごとに何度か割り込みステアリングの 0 個以上回です。 パフォーマンス チェックの OS に一貫性のある応答を提供するために、PEP を支援するために、OS は、通知を求めるメッセージが表示されるパフォーマンス チェックの評価の割り込み時間ベースのタイムスタンプを指定します。 すべてパーク選択通知が 1 つのパフォーマンスの結果は、同じタイムスタンプ評価を確認します。 残りのフィールド (Count、AdditionalUnparkedProcessors、EvaluationType、およびプロセッサ) では、同じパフォーマンス チェックの評価中に送信される通知が異なる可能性があります、PEP はことはできませんがあることと同じ前提としています。 ことに注意してください。 

AcceptProcessorNotification ルーチンに常に IRQL でと呼ばれる、PEP_NOTIFY_PPM_PARK_SELECTION 通知 DISPATCH_LEVEL を = です。

DISPATCH_LEVEL
 
## <a name="pepnotifyppmperfcheckcomplete"></a>PEP_NOTIFY_PPM_PERF_CHECK_COMPLETE 
ターゲットのプロセッサに、PEP のデバイス ハンドルを含む処理 A PEPHANDLE 構造体。 通知では、特定のプロセッサを使用しない場合に、NULL がこれになります。

通知 PEP_NOTIFY_PPM_PERF_CHECK_COMPLETE 値。

データ。 PEP_PPM_PERF_CHECK_COMPLETE 構造へのポインター。
定期的なパフォーマンス チェックの評価が完了したことを PEP に通知します。

Windows の電源管理フレームワーク (PoFx) では、評価が完了したあたり定期的な確認 PEP に通知する実行時にこの通知を送信します。

IRQL で PEP_NOTIFY_PPM_PERF_CHECK_COMPLETE 通知の場合、AcceptProcessorNotification ルーチンと呼ばれる = DISPATCH_LEVEL とすべてのプロセッサ上の実行中に送信することがあります。

DISPATCH_LEVEL
 
## <a name="pepnotifyppmquerycoordinateddependency"></a>PEP_NOTIFY_PPM_QUERY_COORDINATED_DEPENDENCY 
ターゲットのプロセッサに、PEP のデバイス ハンドルを含む処理 A PEPHANDLE 構造体。 通知では、特定のプロセッサを使用しない場合に、NULL がこれになります。

通知 PEP_NOTIFY_PPM_QUERY_COORDINATED_DEPENDENCY 値。

データ。 PEP_PPM_QUERY_COORDINATED_DEPENDENCY 構造へのポインター。
各調整のアイドル状態の依存関係のクエリに PEP に送信されます。

Windows の電源管理フレームワーク (PoFx) では、各連携のとれたアイドル状態の依存関係の PEP を照会するプロセッサの初期化の時点でこの通知を送信します。 OS には、依存関係の配列の MaximumDependencySize 要素が割り当てられます。 DependencySizeUsed で使用されていた、配列の要素の数は、PEP を入力する必要があります。

依存関係が表現されていることをプロセッサの場合は、PEP を対象となるプロセッサ POHANDLE TargetProcessor フィールドで塗りつぶします。 ExpectedState フィールドは、ターゲットのプロセッサのプロセッサのアイドル状態のインデックスを参照します。 

依存関係が表現されていることが他の調整のアイドル状態にある場合は、PEP は、TargetProcessor の場合は NULL に設定します。 ExpectedState フィールドは、連携のとれたアイドル状態のインデックスを参照します。 

各依存関係では、OS が、依存関係を満たすために使用できるオプションのメニューが一覧表示します。 アイドル状態になる OS は最小のインデックスに最も大きいインデックスから各条件をチェックして、依存関係を満たすしようとします。 依存関係の条件が満たされた場合、OS は満たされる依存関係を考慮します。 どの条件が満たされる場合、依存関係が満たされていないと、調整のアイドル状態を入力しない可能性があります。

AcceptProcessorNotification ルーチンに常に IRQL でと呼ばれる PEP_NOTIFY_PPM_QUERY_COORDINATED_DEPENDENCY 通知、PASSIVE_LEVEL を = です。

PASSIVE_LEVEL
 
## <a name="pepnotifyppmquerycoordinatedstatename"></a>PEP_NOTIFY_PPM_QUERY_COORDINATED_STATE_NAME 
ターゲットのプロセッサに、PEP のデバイス ハンドルを含む処理 A PEPHANDLE 構造体。 通知では、特定のプロセッサを使用しない場合に、NULL がこれになります。

通知 PEP_NOTIFY_PPM_QUERY_COORDINATED_STATE_NAME 値。

データ。 PEP_PPM_QUERY_STATE_NAME 構造へのポインター。
アイドル状態の特定またはプラットフォームの調整については、クエリに PEP に送信されます。

Windows 電源管理フレームワーク (PoFx) は、アイドル状態の特定またはプラットフォームの調整については、PEP を照会するプロセッサの初期化でこの通知を送信します。 この通知は、名前の内容を埋めるために、状態、名前に必要な割り当てサイズを取得する NULL 名バッファーが 1 回および NULL 以外の名前のバッファーが 1 回ごとに 2 回送信されます。 名前は、連携のとれたアイドル状態の名前を示す、人間が判読できる文字列である必要があります。 アイドル状態の調整は、複数クラスター システムでは、異なるクラスター上の同等の状態の名前可能性がある同じを除く、一意の名前が必要です。 WPA およびカーネル デバッガーなどのツールをデバッグすると、この調整/プラットフォームのアイドル状態を参照する診断名が表示されます。

AcceptProcessorNotification ルーチンに常に IRQL でと呼ばれる PEP_NOTIFY_PPM_QUERY_COORDINATED_STATE_NAME 通知、PASSIVE_LEVEL を = です。

PASSIVE_LEVEL
 
## <a name="pepnotifyppmquerycoordinatedstates"></a>PEP_NOTIFY_PPM_QUERY_COORDINATED_STATES 
ターゲットのプロセッサに、PEP のデバイス ハンドルを含む処理 A PEPHANDLE 構造体。 通知では、特定のプロセッサを使用しない場合に、NULL がこれになります。

通知 PEP_NOTIFY_PPM_QUERY_COORDINATED_STATES 値。

データ。 PEP_PPM_QUERY_COORDINATED_STATES 構造へのポインター。
すべて連携のとれたアイドル状態のプロパティにクエリ プロセッサの初期化に使用します。

Windows の電源管理フレームワーク (PoFx) では、アイドル状態の調整されたすべてのプロパティを照会するプロセッサの初期化に PEP にこの通知を送信します。 PEP に PEP_NOTIFY_PPM_QUERY_PLATFORM_STATE 通知が送信されるが、直前に、この通知が送信されます。 受け入れられない場合、PEP は、アイドル状態の連携のとれたインターフェイスを使用して、PEP_NOTIFY_PPM_QUERY_PLATFORM_STATE 通知を受信しませんが。 できない場合は、プラットフォームのアイドル状態のインターフェイスを使用して、PEP を受け入れられると、し、OS がフォールバックして連携のとれたアイドル状態のクエリに PEP_NOTIFY_PPM_QUERY_PLATFORM_STATE 通知を使用しています。 

OS は、PEP のすべてのプロセッサが登録された後までには、この通知の送信を待機します。 

PEP は、連携のとれたアイドル状態に関する情報の状態を構造体に格納します。

調整のアイドル状態の順序は、次の規則に従う必要があります。 

2 つの調整と同じ機能単位は、最も明るいものから順に表示されるはずの別の電源状態を表す状態 (ほとんどの電力消費/最低切り替えコスト) 最下位に (少なくとも電源消費/ほとんど切り替えコスト)。 調整のアイドル状態のみ下限のインデックスを持つその他の連携のとれたアイドル状態に依存する可能性があります。 2 つ不整合のある連携したアイドル状態の状態 (つまり、2 つ連携のとれたアイドル状態のプロセッサの分離されたセットに依存する) 必要な順序がありません。

AcceptProcessorNotification ルーチンに常に IRQL でと呼ばれる PEP_NOTIFY_PPM_QUERY_COORDINATED_STATES 通知、PASSIVE_LEVEL を = です。

PASSIVE_LEVEL
 
## <a name="pepnotifyppmqueryprocessorstatename"></a>PEP_NOTIFY_PPM_QUERY_PROCESSOR_STATE_NAME 
ターゲットのプロセッサに、PEP のデバイス ハンドルを含む処理 A PEPHANDLE 構造体。 通知では、特定のプロセッサを使用しない場合に、NULL がこれになります。

通知 PEP_NOTIFY_PPM_QUERY_PROCESSOR_STATE_NAME 値。

データ。 PEP_PPM_QUERY_STATE_NAME 構造へのポインター。
特定のプロセッサのアイドル状態については、クエリに PEP に送信されます。

Windows 電源管理フレームワーク (PoFx) は、特定のプロセッサのアイドル状態については、PEP を照会するプロセッサの初期化でこの通知を送信します。 この通知は、名前の内容を埋めるために、状態、名前に必要な割り当てサイズを取得する NULL 名バッファーが 1 回および NULL 以外の名前のバッファーが 1 回ごとに 2 回送信されます。 名前は、連携のとれたアイドル状態の名前を示す、人間が判読できる文字列である必要があります。 アイドル状態の調整は、複数クラスター システムでは、異なるクラスター上の同等の状態の名前可能性がある同じを除く、一意の名前が必要です。 WPA およびカーネル デバッガーなどのツールをデバッグすると、この調整/プラットフォームのアイドル状態を参照する診断名が表示されます。

AcceptProcessorNotification ルーチンに常に IRQL でと呼ばれる PEP_NOTIFY_PPM_QUERY_PROCESSOR_STATE_NAME 通知、PASSIVE_LEVEL を = です。

PASSIVE_LEVEL
 
## <a name="pepnotifyppmentersystemstate"></a>PEP_NOTIFY_PPM_ENTER_SYSTEM_STATE 
ターゲットのプロセッサに、PEP のデバイス ハンドルを含む処理 A PEPHANDLE 構造体。 通知では、特定のプロセッサを使用しない場合に、NULL がこれになります。

通知 PEP_NOTIFY_PPM_ENTER_SYSTEM_STATE 値。

データ。 PEP_PPM_ENTER_SYSTEM_STATE 構造へのポインター。
PEP_NOTIFY_PPM_ENTER_SYSTEM_STATE は、システムは、システム電源の状態に、PEP に通知する、省略可能な通知です。 システムのすべてのパッシブ レベル作業をプロセッサをシステムの電源状態の移行が完了した後、この通知はすべてのプロセッサに同時に送信します。  

この通知は、ディスパッチにあるすべてのプロセッサを搭載した、DISPATCH_LEVEL で送信されます。 この通知は常に、ターゲット プロセッサで実行されます。 

注、PEP をこの通知からのすべての作業キューに登録する必要があります。 プロセッサは処理しません作業項目、Dpc などがこの通知の送信後。 
 

DISPATCH_LEVEL
 
## <a name="pepnotifyppmperfsetstate"></a>PEP_NOTIFY_PPM_PERF_SET_STATE 
ターゲットのプロセッサに、PEP のデバイス ハンドルを含む処理 A PEPHANDLE 構造体。 通知では、特定のプロセッサを使用しない場合に、NULL がこれになります。

通知 PEP_NOTIFY_PPM_PERF_SET_STATE 値。

データ。 PEP_PPM_PERF_SET_STATE 構造へのポインター。
実行時に、プロセッサの現在の操作のパフォーマンス状態を設定するために使用します。 PEP に自律的なハードウェア ブースティング減らすことなくパフォーマンスのセットの要求のパフォーマンスがの対応がある場合はの自律的なハードウェアの最小パフォーマンスの状態や最大のパフォーマンスの状態に基づいて要求を制限して、目的のターゲットパフォーマンスの状態。 それ以外の場合、必要なパフォーマンスの状態を正確に実行します。  

この通知は、DISPATCH_LEVEL で送信されます。 スケジューラは、使用中のパフォーマンス状態が出力された場合、PEP は、この通知を処理するときにセクション 3.3.6 での制限に従う必要があります。 すべてのプロセッサ上の実行中に送信されます。 

DISPATCH_LEVEL
 
## <a name="pepnotifyppmquerydiscreteperfstates"></a>PEP_NOTIFY_PPM_QUERY_DISCRETE_PERF_STATES 
ターゲットのプロセッサに、PEP のデバイス ハンドルを含む処理 A PEPHANDLE 構造体。 通知では、特定のプロセッサを使用しない場合に、NULL がこれになります。

通知 PEP_NOTIFY_PPM_QUERY_DISCRETE_PERF_STATES 値。

データ。 PEP_PPM_QUERY_DISCRETE_PERF_STATES 構造へのポインター。
PEP_NOTIFY_PPM_QUERY_CAPABILITIES 通知には、個別のパフォーマンス状態のサポートが示されている場合、PEP をサポートする個別のパフォーマンス状態の一覧についてはクエリ プロセッサの初期化に使用します。  

各パフォーマンス状態のマッピングを個別のパフォーマンス値で最も低速なから最も高速なパフォーマンス状態の一覧を注文する必要があります。 パフォーマンス状態の一覧にする必要がありますも PEP_NOTIFY_PPM_QUERY_PERF_CAPABILITIES 通知で示されている各パフォーマンス値と一致するエントリが含まれます。  この通知は PASSIVE_LEVEL で送信されます。 すべてのプロセッサ上の実行中に送信されます。 

PASSIVE_LEVEL
 
## <a name="pepnotifyppmquerydomaininfo"></a>PEP_NOTIFY_PPM_QUERY_DOMAIN_INFO 
ターゲットのプロセッサに、PEP のデバイス ハンドルを含む処理 A PEPHANDLE 構造体。 通知では、特定のプロセッサを使用しない場合に、NULL がこれになります。

通知 PEP_NOTIFY_PPM_QUERY_DOMAIN_INFO 値。

データ。 PEP_PPM_QUERY_DOMAIN_INFO 構造へのポインター。
パフォーマンスのドメインに関する情報をクエリする省略可能な通知します。  この通知は PASSIVE_LEVEL で送信されます。 すべてのプロセッサ上の実行中に送信されます。

PASSIVE_LEVEL

  
## <a name="pepnotifyppmresumefromsystemstate"></a>PEP_NOTIFY_PPM_RESUME_FROM_SYSTEM_STATE 
ターゲットのプロセッサに、PEP のデバイス ハンドルを含む処理 A PEPHANDLE 構造体。 通知では、特定のプロセッサを使用しない場合に、NULL がこれになります。

通知 PEP_NOTIFY_PPM_RESUME_FROM_SYSTEM_STATE 値。

データ。 PEP_PPM_RESUME_FROM_SYSTEM_STATE 構造へのポインター。
システムが電源の状態から再開だけ PEP に通知する省略可能な通知します。 パッシブの作業を再開するプロセッサを解放する前に、この通知はすべてのプロセッサに同時に送信します。  この通知は、ディスパッチにあるすべてのプロセッサを搭載した、DISPATCH_LEVEL で送信されます。 この通知は常に、ターゲット プロセッサで実行されます。 

DISPATCH_LEVEL
 

