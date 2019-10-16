---
title: プロセッサ電源管理 (PPM) の通知
description: PEP の AcceptProcessorNotification コールバックルーチンが受信する各プロセッサ電源管理 (PPM) 通知には、通知の種類を示す通知パラメーターと、データ構造を指すデータパラメーターが付属しています。指定された通知の種類に関する情報が格納されている。
ms.assetid: 4BA89D0F-78F0-44DF-BC9B-0F9F3256CD59
keywords:
- AcceptProcessorNotification コールバック
ms.date: 01/17/2018
ms.localizationpriority: medium
ms.openlocfilehash: b250856ff2a351929b179bdae5a7bcf4de7b4da4
ms.sourcegitcommit: 5b0d2b7a3a4efa3bc4f94a769bf41d58d3321d50
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2019
ms.locfileid: "72390721"
---
# <a name="processor-power-management-ppm-notifications"></a>プロセッサ電源管理 (PPM) の通知
PEP の[*Acceptprocessornotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/pepfx/nc-pepfx-pepcallbacknotifyppm)コールバックルーチンが受信する各プロセッサ電源管理 (PPM) 通知には、通知の種類を示す通知パラメーターと、データを指すデータパラメーターが付属しています。指定された通知の種類の情報を格納する構造体。

この呼び出しでは、通知パラメーターは、通知の種類を示す PEP_NOTIFY_PPM_XXX 定数値に設定されます。 データパラメーターが、この通知の種類に関連付けられている PEP_PPM_XXX 構造体の型を指しています。

次のプロセッサ電源管理 (PPM) 通知 Id は、AcceptProcessorNotification コールバックルーチンによって使用されます。

## <a name="pep_notify_ppm_query_capabilities"></a>PEP_NOTIFY_PPM_QUERY_CAPABILITIES 
ターゲットプロセッサの PEP のデバイスハンドルを含む PEPHANDLE 構造体を処理します。 通知が特定のプロセッサを対象としていない場合、これは NULL になります。

通知値 PEP_NOTIFY_PPM_QUERY_CAPABILITIES。

データ PEP_PPM_QUERY_CAPABILITIES 構造体へのポインター。
pep の電源管理機能に対してクエリが行われていることを PEP に通知します。

Windows の電源管理フレームワーク (PoFx) は、その電源管理機能に対して PEP が照会されたときに、この通知を送信します。 これは、プロセッサの初期化時に発生し、システム内の各プロセッサに対して送信されます。

X86/AMD64 プロセッサを搭載したプラットフォームでは、プロセッサパフォーマンス制御のために ACPI インターフェイスを使用する必要があります。

PEP_NOTIFY_PPM_QUERY_CAPABILITIES 通知を送信するために、PoFx は PEP の AcceptProcessorNotification コールバックルーチンを呼び出します。 この呼び出しでは、通知パラメーターの値は PEP_NOTIFY_PPM_QUERY_CAPABILITIES、データパラメーターは PEP_PPM_QUERY_CAPABILITIES 構造体を指します。

PEP_NOTIFY_PPM_QUERY_CAPABILITIES 通知の場合、AcceptProcessorNotification ルーチンは常に IRQL = PASSIVE_LEVEL で呼び出されます。

PASSIVE_LEVEL
 
## <a name="pep_notify_ppm_query_idle_states"></a>PEP_NOTIFY_PPM_QUERY_IDLE_STATES 
通知値 PEP_NOTIFY_PPM_QUERY_IDLE_STATES。

データ PEP_PPM_QUERY_IDLE_STATES 構造体へのポインター。
アイドル状態を PEP に通知します。

PEP_NOTIFY_PPM_QUERY_IDLE_STATES 通知を送信するために、PoFx は PEP の AcceptProcessorNotification コールバックルーチンを呼び出します。 この呼び出しでは、通知パラメーターの値は PEP_NOTIFY_PPM_QUERY_IDLE_STATES、データパラメーターは PEP_PPM_QUERY_IDLE_STATES 構造体を指します。

PEP_NOTIFY_PPM_QUERY_IDLE_STATES 通知の場合、AcceptProcessorNotification ルーチンは常に IRQL = PASSIVE_LEVEL で呼び出されます。

PASSIVE_LEVEL
 
## <a name="pep_notify_ppm_idle_select"></a>PEP_NOTIFY_PPM_IDLE_SELECT 
通知値 PEP_NOTIFY_PPM_IDLE_SELECT。

データ PEP_PPM_IDLE_SELECT 構造体へのポインター。
アイドル状態の select を PEP に通知します。

PEP_NOTIFY_PPM_IDLE_SELECT 通知を送信するために、PoFx は PEP の AcceptProcessorNotification コールバックルーチンを呼び出します。 この呼び出しでは、通知パラメーターの値は PEP_NOTIFY_PPM_IDLE_SELECT、データパラメーターは PEP_PPM_IDLE_SELECT 構造体を指します。

PEP_NOTIFY_PPM_IDLE_SELECT 通知の場合、AcceptProcessorNotification ルーチンは常に IRQL = PASSIVE_LEVEL で呼び出されます。

PASSIVE_LEVEL
 
## <a name="pep_notify_ppm_idle_cancel"></a>PEP_NOTIFY_PPM_IDLE_CANCEL 
通知値 PEP_NOTIFY_PPM_IDLE_CANCEL。

データ PEP_PPM_IDLE_CANCEL 構造体へのポインター。
キャンセル操作を PEP に通知します。

PEP_NOTIFY_PPM_IDLE_CANCEL 通知を送信するために、PoFx は PEP の AcceptProcessorNotification コールバックルーチンを呼び出します。 この呼び出しでは、通知パラメーターの値は PEP_NOTIFY_PPM_IDLE_CANCEL、データパラメーターは PEP_PPM_IDLE_CANCEL 構造体を指します。

PEP_NOTIFY_PPM_IDLE_CANCEL 通知の場合、AcceptProcessorNotification ルーチンは常に IRQL = PASSIVE_LEVEL で呼び出されます。

PASSIVE_LEVEL
 
## <a name="pep_notify_ppm_idle_execute"></a>PEP_NOTIFY_PPM_IDLE_EXECUTE 
ターゲットプロセッサの PEP のデバイスハンドルを含む PEPHANDLE 構造体を処理します。 通知が特定のプロセッサを対象としていない場合、これは NULL になります。

通知値 PEP_NOTIFY_PPM_IDLE_EXECUTE。

データ PEP_PPM_IDLE_EXECUTE または PEP_PPM_IDLE_EXECUTE_V2 構造体へのポインター。
PEP に送信され、現在のプロセッサを指定されたアイドル状態に移行します。

Windows 電源管理フレームワーク (PoFx) は、この通知を PEP に送信して、現在のプロセッサを指定されたアイドル状態に移行します。 

PEP は、以前に選択されていたアイドル状態になるようにハードウェアを準備します。これには、スリープ状態の移行によって影響を受ける可能性があるコアシステムリソースの OS の通知も含まれます。 次に、halt 命令を実行してプロセッサをアイドル状態に遷移させる必要があります。 アイドル状態から戻ると、PEP はハードウェアのセットアップを元に戻す必要があります。これには、ウェイクアップ時にアクティブになったコアシステムリソースの OS の通知も含まれます。 PEP がプロセッサ (およびプラットフォーム) のアイドル状態を実行できない場合は、エラー状態を返す必要があります。

調整されたアイドル状態のインターフェイスを使用する場合、OS は PEP_PPM_IDLE_EXECUTE_V2 構造体を使用します。これには、アイドル状態の遷移によって入力される、CoordinatedStateCount と CoordinatedState の各フィールドと、調整されたアイドル状態の一覧が含まれます。 [PlatformState] フィールドには、入力されている最も深いプラットフォームの標準の状態 () が指定されます (存在する場合)。 

調整されたアイドル状態のインターフェイスを使用しない場合、OS は PEP_PPM_IDLE_EXECUTE 構造体を使用します。 

PEP_NOTIFY_PPM_IDLE_EXECUTE 通知の場合、無効な割り込みを使用して AcceptProcessorNotification ルーチンが呼び出されます。
 
## <a name="pep_notify_ppm_idle_complete"></a>PEP_NOTIFY_PPM_IDLE_COMPLETE 
ターゲットプロセッサの PEP のデバイスハンドルを含む PEPHANDLE 構造体を処理します。 

通知値 PEP_NOTIFY_PPM_IDLE_COMPLETE。

データ PEP_PPM_IDLE_COMPLETE または PEP_PPM_IDLE_COMPLETE_V2 構造体へのポインター。
現在のプロセッサが、完了したアイドル状態の遷移からウェイクアップしていることを PEP に通知します。

Windows の電源管理フレームワーク (PoFx) は、現在のプロセッサが、完了したアイドル状態の遷移からウェイクアップするときに、この通知を送信します。 プラットフォームがプラットフォームのアイドル状態の移行を実行していた場合は、最初のプロセッサをスリープ解除するときに、終了するプラットフォームのアイドル状態が示されます。 プラットフォームのアイドル状態への移行で使用される同期の種類によっては、プラットフォームのアイドル状態から復帰する最初のプロセッサが、プラットフォームのアイドル状態になったプロセッサでない場合があります。 

プロセッサがディープアイドル状態を実行していた場合、PEP はコアコンテキストを復元するための完全な通知を受信するか、コアリソースが復元されたことを OS に通知するまで待機することはできません。 OS では、実行通知が完了すると、これらのリソースが復元されることを想定しています。 ハイパーバイザーが有効になっている場合、PEP は、プラットフォームのアイドル状態から終了し、ProcessorState フィールドが PEP_PROCESSOR_IDLE_STATE_UNKNOWN に設定されている場合にのみ、この通知を受信します。 

調整されたアイドル状態のインターフェイスを使用する場合、OS は PEP_PPM_IDLE_COMPLETE_V2 構造体を使用します。これには、アイドル状態の遷移によって終了される、CoordinatedStateCount と CoordinatedState の各フィールドと、連携しているアイドル状態の一覧が含まれています。 [PlatformState] フィールドには、終了している最も深いプラットフォームの協調的なアイドル状態 (存在する場合) が指定されます。 このプロセッサによって終了された一連の遷移アイドル状態は、緩やかな同期が使用されている場合に、それによって入力された一連のアイドル状態と異なる場合があることに注意してください。 

調整されたアイドル状態のインターフェイスを使用しない場合、OS は PEP_PPM_IDLE_COMPLETE 構造体を使用します。 

PEP_NOTIFY_PPM_IDLE_COMPLETE 通知の場合、AcceptProcessorNotification ルーチンは割り込みが無効になって呼び出され、常にターゲットプロセッサで実行されます。
 
## <a name="pep_notify_ppm_is_processor_halted"></a>PEP_NOTIFY_PPM_IS_PROCESSOR_HALTED 
ターゲットプロセッサの PEP のデバイスハンドルを含む PEPHANDLE 構造体を処理します。 通知が特定のプロセッサを対象としていない場合、これは NULL になります。

通知値 PEP_NOTIFY_PPM_IS_PROCESSOR_HALTED。

データ PEP_PPM_IS_PROCESSOR_HALTED 構造体へのポインター。
指定されたプロセッサが選択されたアイドル状態で現在停止しているかどうかを判断するために PEP に送信されます。

Windows 電源管理フレームワーク (PoFx) は、この通知を PEP に送信して、指定されたプロセッサが現在選択されているアイドル状態で停止しているかどうかを確認します。 OS は、この通知を使用して、プラットフォームのアイドル状態を調整するときに、セカンダリプロセッサがアイドル状態への移行を完全に完了したかどうかを確認します。 PEP は、ターゲットプロセッサが、プラットフォームのアイドル遷移を安全に実行できる状態になっていることを保証する必要があります (たとえば、ハードウェアレジスタを調べてコアが停止しているかどうかを確認します)。 この通知は、プロセッサがアイドル状態であることを示した後、OS が明示的に要求しない限り、そのプロセッサをウェイクアップさせることはできません。 

PEP は、IDLE_SELECT 通知と IDLE_COMPLETE 通知の間でいつでもこの通知を受け取る場合があります。 この通知は、アイドル状態の移行中に最大で1回受信することが保証されています。 

PEP_NOTIFY_PPM_IS_PROCESSOR_HALTED 通知の場合、AcceptProcessorNotification ルーチンは任意の IRQL で呼び出され、割り込みは無効になり、任意の IRQL で呼び出され、ターゲットプロセッサでは実行されません。

< = HIGH_LEVEL
 
## <a name="pep_notify_ppm_initiate_wake"></a>PEP_NOTIFY_PPM_INITIATE_WAKE 
ターゲットプロセッサの PEP のデバイスハンドルを含む PEPHANDLE 構造体を処理します。

通知値 PEP_NOTIFY_PPM_INITIATE_WAKE。

データ構造体へのポインター。
割り込み不可能なアイドル状態からのウェイクアップを開始するために、指定されたプロセッサの PEP に送信されます。

Windows 電源管理フレームワーク (PoFx) は、指定されたプロセッサの PEP にこの通知を送信して、割り込み不可能なアイドル状態からのウェイクアップを開始します。 PEP は、NeedInterruptForCompletion を使用してターゲットプロセッサの wake の状態を返す必要があります。 プロセッサがアイドル状態からのウェイクアップを終了する必要がある場合は、TRUE を返します。 この場合、PEP は、この通知の処理から戻った時点でターゲットプロセッサが中断可能であることを確認する必要があります。 ターゲットプロセッサが既に実行されている場合、またはでは、ソフトウェアによって生成された割り込みを必要とせずに (その処理中に) アイドル状態を終了する場合は、NeedInterruptForCompletion を FALSE に設定する必要があります。


PEP は同じプロセッサに対してこの通知を同時に受け取ることはありません。
 

PEP_NOTIFY_PPM_INITIATE_WAKE 通知の場合、AcceptProcessorNotification ルーチンは、割り込みが無効になっている任意の IRQL で呼び出され、ターゲットプロセッサでは実行されません。

< = HIGH_LEVEL
 
## <a name="pep_notify_ppm_query_feedback_counters"></a>PEP_NOTIFY_PPM_QUERY_FEEDBACK_COUNTERS 
ターゲットプロセッサの PEP のデバイスハンドルを含む PEPHANDLE 構造体を処理します。 通知が特定のプロセッサを対象としていない場合、これは NULL になります。

通知値 PEP_NOTIFY_PPM_QUERY_FEEDBACK_COUNTERS。

データ PEP_PPM_QUERY_FEEDBACK_COUNTERS 構造体へのポインター。
Pep に、サポートされているフィードバックカウンターの一覧を照会していることを PEP に通知します。

Windows 電源管理フレームワーク (PoFx) は、プロセッサの初期化時にこの通知を送信して、サポートされているフィードバックカウンターの一覧を PEP に照会します。

PEP_NOTIFY_PPM_QUERY_FEEDBACK_COUNTERS 通知の場合、AcceptProcessorNotification ルーチンは常に IRQL = PASSIVE_LEVEL で呼び出されます。

PASSIVE_LEVEL
 
## <a name="pep_notify_ppm_feedback_read"></a>PEP_NOTIFY_PPM_FEEDBACK_READ 
ターゲットプロセッサの PEP のデバイスハンドルを含む PEPHANDLE 構造体を処理します。 通知が特定のプロセッサを対象としていない場合、これは NULL になります。

通知値 PEP_NOTIFY_PPM_FEEDBACK_READ。

データ PEP_PPM_FEEDBACK_READ 構造体へのポインター。
は、フィードバックカウンターの現在の値を照会していることを PEP に通知します。

Windows 電源管理フレームワーク (PoFx) は、フィードバックカウンターの現在の値を照会するときに、この通知を送信します。 

この通知は、割り込みが無効になっている場合に送信されます。 カウンターの関連付けられたフィールドが設定されている場合、この通知はターゲットプロセッサで実行されます。 それ以外の場合、この通知はどのプロセッサからでも実行できます。

PEP_NOTIFY_PPM_FEEDBACK_READ 通知の場合、AcceptProcessorNotification ルーチンは IRQL = DISPATCH_LEVEL で呼び出されることがあります。

DISPATCH_LEVEL
 
## <a name="pep_notify_ppm_query_perf_capabilities"></a>PEP_NOTIFY_PPM_QUERY_PERF_CAPABILITIES 
ターゲットプロセッサの PEP のデバイスハンドルを含む PEPHANDLE 構造体を処理します。 通知が特定のプロセッサを対象としていない場合、これは NULL になります。

通知値 PEP_NOTIFY_PPM_QUERY_PERF_CAPABILITIES。

データ PEP_PPM_QUERY_PERF_CAPABILITIES 構造体へのポインター。
は、プラットフォームでサポートされているパフォーマンス範囲に対してクエリが行われていることを PEP に通知します。

Windows 電源管理フレームワーク (PoFx) は、この通知をプロセッサの初期化時に送信して、プラットフォームでサポートされているパフォーマンスの範囲を照会します。 PEP_PPM_QUERY_PERF_CAPABILITIES 構造体の DomainId および Domainid フィールドは、パフォーマンス状態ドメインをプラットフォームに表すために使用されます。 各プロセッサは、まったく1つのパフォーマンス状態ドメインのメンバーです。 オペレーティングシステムによって、パフォーマンスドメイン内のすべてのプロセッサのパフォーマンスが変化します。 

PEP_NOTIFY_PPM_QUERY_PERF_CAPABILITIES 通知の場合、AcceptProcessorNotification ルーチンは常に IRQL = PASSIVE_LEVEL で呼び出されます。

PASSIVE_LEVEL
 
## <a name="pep_notify_ppm_perf_constraints"></a>PEP_NOTIFY_PPM_PERF_CONSTRAINTS 
ターゲットプロセッサの PEP のデバイスハンドルを含む PEPHANDLE 構造体を処理します。 

通知値 PEP_NOTIFY_PPM_PERF_CONSTRAINTS。

データ PEP_PPM_PERF_CONSTRAINTS 構造体へのポインター。
は、プロセッサの現在の操作制約に対してクエリを行っていることを PEP に通知します。

Windows 電源管理フレームワーク (PoFx) は、プロセッサの現在の動作制約を検査するときに、この通知を送信します。 PEP は、制御コード GUID_PPM_PERF_CONSTRAINT_CHANGE を使用して電源管理を実行することで、プロセッサのパフォーマンス制約を再評価するための OS の要求を開始します。 InBuffer と OutBuffer は NULL である必要があります。 

PEP は、プロセッサの電源管理トランザクションを発行する前に、プロセッサの PEP_DPM_DEVICE_STARTED 通知を受信するまで待機する必要があります。 

PEP_NOTIFY_PPM_PERF_CONSTRAINTS 通知の場合、AcceptProcessorNotification ルーチンは常に IRQL = PASSIVE_LEVEL で呼び出されます。

PASSIVE_LEVEL
 
## <a name="pep_notify_ppm_perf_set"></a>PEP_NOTIFY_PPM_PERF_SET 
ターゲットプロセッサの PEP のデバイスハンドルを含む PEPHANDLE 構造体を処理します。 通知が特定のプロセッサを対象としていない場合、これは NULL になります。

通知値 PEP_NOTIFY_PPM_PERF_SET。

データ[**PEP_PPM_PERF_SET**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/pep_x/ns-pep_x-_pep_ppm_perf_set)構造体へのポインター。
プロセッサの現在の動作パフォーマンスを変更する必要があることを PEP に通知します。

Windows の電源管理フレームワーク (PoFx) は、プロセッサの現在の動作パフォーマンスを変更する場合に、この通知を送信します。 この通知は、任意のプロセッサでの実行中に送信される場合があります。

PEP_NOTIFY_PPM_PERF_SET 通知の場合、AcceptProcessorNotification ルーチンは常に IRQL = DISPATCH_LEVEL で呼び出されます。

DISPATCH_LEVEL
 
## <a name="pep_notify_ppm_park_selection"></a>PEP_NOTIFY_PPM_PARK_SELECTION 
ターゲットプロセッサの PEP のデバイスハンドルを含む PEPHANDLE 構造体を処理します。 通知が特定のプロセッサを対象としていない場合、これは NULL になります。

通知値 PEP_NOTIFY_PPM_PARK_SELECTION。

データ PEP_PPM_PARK_SELECTION 構造体へのポインター。
オペレーティングシステムが、使用するプロセッサコアの優先セットを選択したいと考えていることを PEP に通知します。

Windows 電源管理フレームワーク (PoFx) は、この通知を送信して、PEP に対して、パークするコアの優先セットを選択するように指示します。

PEP_NOTIFY_PPM_PARK_SELECTION は、次の2つの関数を実行するためにオーバーロードされています。 

PEP を使用して、(システム内のすべてのプロセッサのセットから) どのプロセッサを保留するかを選択します。また、保留を解除する必要があります。 PEP が、保留されているすべてのプロセッサのセットから割り込みを受け取る必要があり、割り込みを受信しないプロセッサを選択します。 Windows には、1つの OS で実行されている2つのを区別するための手段が用意されていません。 その結果、PEP は、特定の入力セット (AdditionalunparPepPreference Processor count と PoPreference) を使用してこの通知を受信するときに、一部の外部イベントによって PEP 優先順位が変更されない限り、一貫性のある出力 () を提供する必要があります。 

PEP_NOTIFY_PPM_PARK_SELECTION 通知の場合、AcceptProcessorNotification ルーチンは常に IRQL = DISPATCH_LEVEL で呼び出されます。

DISPATCH_LEVEL
 
## <a name="pep_notify_ppm_cst_states"></a>PEP_NOTIFY_PPM_CST_STATES 
ターゲットプロセッサの PEP のデバイスハンドルを含む PEPHANDLE 構造体を処理します。 通知が特定のプロセッサを対象としていない場合、これは NULL になります。

通知値 PEP_NOTIFY_PPM_CST_STATES。

データ PEP_PPM_CST_STATES 構造体へのポインター。
プロセッサでサポートされている ACPI 定義の C 状態のセットを示すために PEP に送信されます。 

Windows 電源管理フレームワーク (PoFx) は、この通知を PEP に送信して、プロセッサでサポートされている ACPI 定義の C 状態のセットを示します。 この通知は、最初に PEP がプロセッサに対して PEP_NOTIFY_PPM_QUERY_IDLE_STATES_V2 通知を受信する前に1回送信されます。また、_CST オブジェクトが変更されたことを示す Notify (0x81) をプロセッサが受け取るたびにも送信されます。

PEP_NOTIFY_PPM_CST_STATES 通知の場合、AcceptProcessorNotification ルーチンは常に IRQL = PASSIVE_LEVEL で呼び出されます。

PASSIVE_LEVEL
 
## <a name="pep_notify_ppm_query_platform_states"></a>PEP_NOTIFY_PPM_QUERY_PLATFORM_STATES 
ターゲットプロセッサの PEP のデバイスハンドルを含む PEPHANDLE 構造体を処理します。 通知が特定のプロセッサを対象としていない場合、これは NULL になります。

通知値 PEP_NOTIFY_PPM_QUERY_PLATFORM_STATES。

データ PEP_PPM_QUERY_PLATFORM_STATES 構造体へのポインター。
PEP がサポートするプラットフォームのアイドル状態の数を照会するために、プロセッサの初期化時に送信されます。

Windows 電源管理フレームワーク (PoFx) は、プロセッサの初期化時にこの通知を PEP に送信して、サポートされているプラットフォームのアイドル状態の数を照会します。 この通知は、起動時に1回送信されます。 0以外の数のプラットフォーム状態を返した後、PEP はプロセッサのアイドル状態の遷移中に、プラットフォームのアイドル状態の選択を開始できます。

PEP_NOTIFY_PPM_QUERY_PLATFORM_STATES 通知の場合、AcceptProcessorNotification ルーチンは常に IRQL = PASSIVE_LEVEL で呼び出されます。

PASSIVE_LEVEL
 
## <a name="pep_notify_ppm_query_lp_settings"></a>PEP_NOTIFY_PPM_QUERY_LP_SETTINGS 
通知値 PEP_NOTIFY_PPM_QUERY_LP_SETTINGS。

データ PEP_PPM_QUERY_LP_SETTINGS 構造体へのポインター。
PEP_NOTIFY_PPM_QUERY_LP_SETTINGS 通知を送信するために、PoFx は PEP の AcceptProcessorNotification コールバックルーチンを呼び出します。 この呼び出しでは、通知パラメーターの値は PEP_NOTIFY_PPM_QUERY_LP_SETTINGS、データパラメーターは PEP_PPM_QUERY_LP_SETTINGS 構造体を指します。

PEP_NOTIFY_PPM_QUERY_LP_SETTINGS 通知の場合、AcceptProcessorNotification ルーチンは常に IRQL = PASSIVE_LEVEL で呼び出されます。

PASSIVE_LEVEL
 
## <a name="pep_notify_ppm_query_idle_states_v2"></a>PEP_NOTIFY_PPM_QUERY_IDLE_STATES_V2 
ターゲットプロセッサの PEP のデバイスハンドルを含む PEPHANDLE 構造体を処理します。 通知が特定のプロセッサを対象としていない場合、これは NULL になります。

通知値 PEP_NOTIFY_PPM_QUERY_IDLE_STATES_V2。

データ PEP_PPM_QUERY_IDLE_STATES_V2 構造体へのポインター。
プロセッサの初期化時に、PEP がサポートするアイドル状態の一覧を照会するために使用されます。

Windows 電源管理フレームワーク (PoFx) は、プロセッサの初期化時にこの通知を PEP に送信して、サポートされているアイドル状態の一覧を照会します。 

Count メンバーは、アイドル状態の配列のサイズを指定します。 プロセッサドライバーは、この通知を送信する前に、PEP_NOTIFY_PPM_QUERY_CAPABILITIES でアイドル状態の数を照会します。 

PEP は、IdleStates 配列に、サポートされている各アイドル状態に関する情報を格納します。 アイドル状態は、電力消費量の減少と移行コストの増加の順に一覧表示されます。 PEP は、プロセッサごとに同じアイドル状態の一覧を報告する必要はありません。 

PEP_NOTIFY_PPM_QUERY_IDLE_STATES_V2 通知の場合、AcceptProcessorNotification ルーチンは常に IRQL = PASSIVE_LEVEL で呼び出されます。

PASSIVE_LEVEL
 
## <a name="pep_notify_ppm_query_platform_state"></a>PEP_NOTIFY_PPM_QUERY_PLATFORM_STATE 
ターゲットプロセッサの PEP のデバイスハンドルを含む PEPHANDLE 構造体を処理します。 通知が特定のプロセッサを対象としていない場合、これは NULL になります。

通知値 PEP_NOTIFY_PPM_QUERY_PLATFORM_STATE。

データ PEP_PPM_QUERY_PLATFORM_STATE 構造体へのポインター。
単一のプラットフォームアイドル状態のプロパティを照会するために PEP に送信されます。

Windows 電源管理フレームワーク (PoFx) は、プロセッサの初期化時にこの通知を送信して、単一のプラットフォームアイドル状態のプロパティを照会します。 

PEP_PPM_QUERY_PLATFORM_STATE 構造体の StateIndex パラメーターは、クエリ対象のプラットフォームのアイドル状態のインデックスを指定します。 プロセッサドライバーは、この通知を送信する前に、PEP_NOTIFY_PPM_QUERY_PLATFORM_STATES でサポートされているプラットフォームのアイドル状態の数を照会します。 その後、プロセッサドライバーは、プラットフォームのアイドル状態ごとに1つの PEP_NOTIFY_PPM_QUERY_PLATFORM_STATE 通知を送信します。 プロセッサドライバーは、すべてのプロセッサが PEP に登録されるまで、この通知の送信を待機します。 

PEP は、プラットフォームのアイドル状態に関する情報を状態構造に格納します。 [プラットフォームのアイドル状態] には、電力消費量の減少と移行コストの増加の順に表示されます。 

PEP_NOTIFY_PPM_QUERY_PLATFORM_STATE 通知の場合、AcceptProcessorNotification ルーチンは常に IRQL = PASSIVE_LEVEL で呼び出されます。

PASSIVE_LEVEL
 
## <a name="pep_notify_ppm_test_idle_state"></a>PEP_NOTIFY_PPM_TEST_IDLE_STATE 
ターゲットプロセッサの PEP のデバイスハンドルを含む PEPHANDLE 構造体を処理します。 通知が特定のプロセッサを対象としていない場合、これは NULL になります。

通知値 PEP_NOTIFY_PPM_TEST_IDLE_STATE。

データ PEP_PPM_TEST_IDLE_STATE 構造体へのポインター。
指定されたプロセッサとプラットフォームのアイドル状態を指定されたプロセッサに入力できるかどうかをテストするために使用します。

Windows 電源管理フレームワーク (PoFx) は、指定されたプロセッサとプラットフォームのアイドル状態を指定されたプロセッサに入力できるかどうかをテストするために、この通知を送信します。 アイドル状態を入力できる場合、PEP は拒否コード PEP_IDLE_VETO_NONE を入力し、アイドル状態の遷移を完了します。 何らかの理由でアイドル状態の遷移を完了できない場合、PEP はゼロでない拒否コードを入力します。 

0x80000000 から0xffffffff までの範囲の重要な拒否コードは OS 使用のために予約されているため、使用できません。
 

この通知が送信されると、OS は、選択したプロセッサまたはプラットフォームのアイドル状態に関連付けられているすべての制約が満たされていることを既に検証しています。これには、プラットフォームのアイドル遷移に関するデバイスとプロセッサの制約が含まれます。 

この通知は、OS がプロセッサまたはプラットフォームのアイドル状態を入力しようとする前に送信されます。ただし、インデックス0のプロセッサアイドル状態は常に入力可能である必要があります。 PEP_IDLE_VETO_NONE を使用してこの通知を完了しても、OS が指定されたアイドル状態になるとは限りません。 この通知は、割り込みが無効になっている状態で送信されます。 この通知は、常にターゲットプロセッサで実行されます。 

PEP_NOTIFY_PPM_TEST_IDLE_STATE 通知の場合、無効な割り込みを使用して AcceptProcessorNotification ルーチンが呼び出されます。
 
## <a name="pep_notify_ppm_idle_pre_execute"></a>PEP_NOTIFY_PPM_IDLE_PRE_EXECUTE 
ターゲットプロセッサの PEP のデバイスハンドルを含む PEPHANDLE 構造体を処理します。 通知が特定のプロセッサを対象としていない場合、これは NULL になります。

通知値 PEP_NOTIFY_PPM_IDLE_PRE_EXECUTE。

データ PEP_PPM_IDLE_EXECUTE または PEP_PPM_IDLE_EXECUTE_V2 構造体へのポインター。
指定されたアイドル状態に移行するシステムを準備するために、PEP に送信されます。

Windows 電源管理フレームワーク (PoFx) は、この通知を PEP に送信して、指定されたアイドル状態に移行するためのシステムを準備します。 この通知が正常に完了すると、OS は関連付けられた C 状態を入力してプロセッサをアイドル状態に移行します。 PEP がプロセッサ (およびプラットフォーム) のアイドル状態に入るためにシステムを準備できない場合は、エラー状態を返す必要があります。 

ハイパーバイザーが有効になっている場合、PEP は、プラットフォームのアイドル状態に入ったときと、ProcessorState フィールドが PEP_PROCESSOR_IDLE_STATE_UNKNOWN に設定されている場合にのみ、この通知を受信します。 

調整されたアイドル状態のインターフェイスを使用する場合、OS は PEP_PPM_IDLE_EXECUTE_V2 構造体を使用します。これには、アイドル状態の遷移によって入力される、CoordinatedStateCount と CoordinatedState の各フィールドと、調整されたアイドル状態の一覧が含まれます。 [PlatformState] フィールドには、入力されている最も深いプラットフォームの標準の状態 () が指定されます (存在する場合)。 

調整されたアイドル状態のインターフェイスを使用しない場合、OS は PEP_PPM_IDLE_EXECUTE 構造体を使用します。 

PEP_NOTIFY_PPM_IDLE_PRE_EXECUTE 通知の場合、AcceptProcessorNotification ルーチンは割り込みが無効になって呼び出され、常にターゲットプロセッサで実行されます。
 
## <a name="pep_notify_ppm_update_platform_state"></a>PEP_NOTIFY_PPM_UPDATE_PLATFORM_STATE 
ターゲットプロセッサの PEP のデバイスハンドルを含む PEPHANDLE 構造体を処理します。 通知が特定のプロセッサを対象としていない場合、これは NULL になります。

通知値 PEP_NOTIFY_PPM_UPDATE_PLATFORM_STATE。

データ PEP_PPM_QUERY_PLATFORM_STATE 構造体へのポインター。
プラットフォームのアイドル状態の特性を更新するためにプロセッサが通知を受信したこと (0x81) を PEP に通知します。

Windows の電源管理フレームワーク (PoFx) は、プロセッサがプラットフォームのアイドル状態の特性を更新する通知 (0x81) を受信したときに、この通知を送信します。 この通知は、プラットフォームのアイドル状態ごとに1回送信されます。 PEP が通知を受け入れない場合 (つまり、AcceptProcessorNotification コールバックから FALSE を返す場合)、最後に受け入れられた PEP_NOTIFY_PPM_QUERY_PLATFORM_STATE または PEP_NOTIFY_PPM_ から、プラットフォームのアイドル状態の前の定義が返されます。UPDATE_PLATFORM_STATE 通知は保存されます。 

この通知では、PEP_NOTIFY_PPM_QUERY_PLATFORM_STATE 通知と同じデータバッファーが使用されます。 

PEP_NOTIFY_PPM_UPDATE_PLATFORM_STATE 通知の場合、AcceptProcessorNotification ルーチンは常に IRQL = PASSIVE_LEVEL で呼び出されます。

PASSIVE_LEVEL
 
## <a name="pep_notify_ppm_query_platform_state_residencies"></a>PEP_NOTIFY_PPM_QUERY_PLATFORM_STATE_RESIDENCIES 
ターゲットプロセッサの PEP のデバイスハンドルを含む PEPHANDLE 構造体を処理します。 通知が特定のプロセッサを対象としていない場合、これは NULL になります。

通知値 PEP_NOTIFY_PPM_QUERY_PLATFORM_STATE_RESIDENCIES。

データ PEP_PPM_PLATFORM_STATE_RESIDENCIES 構造体へのポインター。
は、起動後に各プラットフォームのアイドル状態に費やされた実際の累積時間をキャプチャする必要があることを PEP に通知します。

Windows 電源管理フレームワーク (PoFx) は、この通知を PEP に送信して、起動後に各プラットフォームのアイドル状態に費やされた実際の累積時間をキャプチャします。 そのため、このクエリは、基になるハードウェアが、OS によって要求されたものとは異なるプラットフォームのアイドル状態を自律的に入力するプラットフォームにのみ適用されます。 返される値は、診断の目的で使用され、OS のプラットフォームのアイドル状態の状態の表示がプラットフォームの実際の達成と大幅に異なっているかどうかを特定します。 

Count は、States 配列内の要素の数を指定します。この要素のインデックスは、プラットフォームのアイドル状態のインデックスに対応します。 PEP は、各要素に、対応する状態の実際の常駐と遷移の数を入力します。 


このクエリによってキャプチャされた累計値は、PEP (またはプロセッサドライバー) が実際にプラットフォームのアイドル状態の移行を実行した期間にのみ対応する必要があることに注意してください。 これにより、OS の計算された常駐と実際の保存場所の比較が意味を持つようになります。
 

PEP_NOTIFY_PPM_QUERY_PLATFORM_STATE_RESIDENCIES 通知の場合、AcceptProcessorNotification ルーチンは任意の IRQL で呼び出すことができます。
 
## <a name="pep_notify_ppm_query_veto_reasons"></a>PEP_NOTIFY_PPM_QUERY_VETO_REASONS 
ターゲットプロセッサの PEP のデバイスハンドルを含む PEPHANDLE 構造体を処理します。 通知が特定のプロセッサを対象としていない場合、これは NULL になります。

通知値 PEP_NOTIFY_PPM_QUERY_VETO_REASONS。

データ PEP_PPM_QUERY_VETO_REASONS 構造体へのポインター。
ProcessorIdleVeto および PlatformIdleVeto コールバックで PEP が使用する一意の拒否理由の数を照会するために使用されます。 

Windows 電源管理フレームワーク (PoFx) は、プロセッサの初期化時にこの通知を送信して、ProcessorIdleVeto および PlatformIdleVeto コールバックで PEP が使用する一意の拒否理由の数を照会します。 この通知は省略可能であり、PEP によって無視される場合があります。 

許容される場合、PEP は、1から VetoReasonCount までの拒否理由を使用して、プロセッサ、プラットフォーム、または調整されたアイドル状態を拒否することができます。 PEP では、VetoReasonCount より大きい拒否の理由を使用することはできません。 OS は拒否追跡構造を事前に割り当て、PEP_NOTIFY_PPM_ENUMERATE_BOOT_VETOES で使用すると、すべてのプロセッサ、プラットフォーム、および調整された状態拒否コールバックが成功することを保証します。

この通知が PEP によって受け付けられない場合、PEP は ProcessorIdleVeto と PlatformIdleVeto のコールバックを有効な拒否の理由と共に使用する可能性があります。 OS は、割り当てエラーやその他の問題が原因でコールバックが失敗しないことを保証しません。

PEP_NOTIFY_PPM_QUERY_VETO_REASONS 通知の場合、AcceptProcessorNotification ルーチンは常に IRQL = PASSIVE_LEVEL で呼び出されます。

PASSIVE_LEVEL
 
## <a name="pep_notify_ppm_query_veto_reason"></a>PEP_NOTIFY_PPM_QUERY_VETO_REASON 
ターゲットプロセッサの PEP のデバイスハンドルを含む PEPHANDLE 構造体を処理します。 通知が特定のプロセッサを対象としていない場合、これは NULL になります。

通知値 PEP_NOTIFY_PPM_QUERY_VETO_REASON。

データ PEP_PPM_QUERY_VETO_REASON 構造体へのポインター。
特定の拒否理由に関する情報を照会するために PEP に送信されます。

Windows 電源管理フレームワーク (PoFx) は、プロセッサの初期化時にこの通知を送信して、特定の拒否理由に関する情報を照会します。 この通知は、拒否の理由ごとに2回送信されます。1回は名前に必要な割り当てサイズを取得するための NULLName バッファーを使用し、もう1回は名前の内容を入力するための Null 以外の名前バッファーを使用します。 名前は、この拒否理由が表す条件を示す、人間が判読できる文字列である必要があります。 WPA やカーネルデバッガーなどのデバッグツールでは、アイドル状態が入力されなかった原因を診断するときに名前が表示されます。 

PEP_NOTIFY_PPM_QUERY_VETO_REASON 通知の場合、AcceptProcessorNotification ルーチンは常に IRQL = PASSIVE_LEVEL で呼び出されます。

PASSIVE_LEVEL
 
## <a name="pep_notify_ppm_enumerate_boot_vetoes"></a>PEP_NOTIFY_PPM_ENUMERATE_BOOT_VETOES 
ターゲットプロセッサの PEP のデバイスハンドルを含む PEPHANDLE 構造体を処理します。 通知が特定のプロセッサを対象としていない場合、これは NULL になります。

通知値 PEP_NOTIFY_PPM_ENUMERATE_BOOT_VETOES。

データ NULL ポインター値。
OS が ProcessorIdleVeto または PlatformIdleVeto の呼び出しを受け入れる準備ができていることを PEP に通知します。 

Windows 電源管理フレームワーク (PoFx) は、プロセッサの初期化後に、OS が ProcessorIdleVeto または PlatformIdleVeto の呼び出しを受け入れる準備ができていることを示すために、最初のアイドルエントリの前にこの通知を送信します。 PEP は、この通知のコンテキストでブート時の vetoes を列挙する場合があります。また、OS は、プロセッサ、プラットフォーム、または動作しているアイドル状態を最初に選択する前に有効になることを保証します。 この通知には、関連付けられたデータパラメーターがありません。 

PEP_NOTIFY_PPM_ENUMERATE_BOOT_VETOES 通知の場合、AcceptProcessorNotification ルーチンは常に IRQL = PASSIVE_LEVEL で呼び出されます。

PASSIVE_LEVEL
 
## <a name="pep_notify_ppm_park_mask"></a>PEP_NOTIFY_PPM_PARK_MASK 
ターゲットプロセッサの PEP のデバイスハンドルを含む PEPHANDLE 構造体を処理します。 通知が特定のプロセッサを対象としていない場合、これは NULL になります。

通知値 PEP_NOTIFY_PPM_PARK_MASK。

データ PEP_PPM_PARK_MASK 構造体へのポインター。
現在のコアパーキングマスクを PEP に通知します。

Windows 電源管理フレームワーク (PoFx) は、実行時にこの通知を送信して、現在のコア駐車マスクを PEP に通知します。

PEP_NOTIFY_PPM_PARK_MASK 通知の場合、AcceptProcessorNotification ルーチンは IRQL = DISPATCH_LEVEL で呼び出され、任意のプロセッサで実行中に送信される可能性があります。

DISPATCH_LEVEL
 
## <a name="pep_notify_ppm_park_selection_v2"></a>PEP_NOTIFY_PPM_PARK_SELECTION_V2 
ターゲットプロセッサの PEP のデバイスハンドルを含む PEPHANDLE 構造体を処理します。 通知が特定のプロセッサを対象としていない場合、これは NULL になります。

通知値 PEP_NOTIFY_PPM_PARK_SELECTION_V2。

データ PEP_PPM_PARK_SELECTION_V2 構造体へのポインター。
は、割り込みを行うために必要なコアのセットを OS が選択したいと考えていることを PEP に通知します。 この通知が受け付けられない場合、OS はフォールバックして PEP_NOTIFY_PPM_PARK_SELECTION 通知を送信します。

パフォーマンスチェックアルゴリズムを実行すると、OS は PEP_NOTIFY_PPM_PARK_SELECTION_V2 通知を複数回送信する場合があります。各パークドメイン内のコア効率クラスごとに0回以上、割り込みステアリングの場合は0回以上です。 パフォーマンスチェックのために、オペレーティングシステムへの一貫性のある応答を提供するために、OS は、通知を求めたパフォーマンスチェックの評価の割り込み時間ベースのタイムスタンプを提供します。 1つのパフォーマンスチェック評価の結果として得られるすべてのパーク選択通知には、同じタイムスタンプが設定されます。 残りのフィールド (Count、AdditionalUnparkedProcessors、EvaluationType、および Processor) は、同じパフォーマンスチェックの評価中に送信される通知によって異なる場合があることに注意してください。 PEP は、それらが同じままであると見なすことはできません。 

PEP_NOTIFY_PPM_PARK_SELECTION 通知の場合、AcceptProcessorNotification ルーチンは常に IRQL = DISPATCH_LEVEL で呼び出されます。

DISPATCH_LEVEL
 
## <a name="pep_notify_ppm_perf_check_complete"></a>PEP_NOTIFY_PPM_PERF_CHECK_COMPLETE 
ターゲットプロセッサの PEP のデバイスハンドルを含む PEPHANDLE 構造体を処理します。 通知が特定のプロセッサを対象としていない場合、これは NULL になります。

通知値 PEP_NOTIFY_PPM_PERF_CHECK_COMPLETE。

データ PEP_PPM_PERF_CHECK_COMPLETE 構造体へのポインター。
定期的なパフォーマンスチェックの評価が完了したことを PEP に通知します。

Windows 電源管理フレームワーク (PoFx) は、実行時にこの通知を送信して、定期的なチェックの評価が完了したことを PEP に通知します。

PEP_NOTIFY_PPM_PERF_CHECK_COMPLETE 通知の場合、AcceptProcessorNotification ルーチンは IRQL = DISPATCH_LEVEL で呼び出され、任意のプロセッサで実行中に送信される可能性があります。

DISPATCH_LEVEL
 
## <a name="pep_notify_ppm_query_coordinated_dependency"></a>PEP_NOTIFY_PPM_QUERY_COORDINATED_DEPENDENCY 
ターゲットプロセッサの PEP のデバイスハンドルを含む PEPHANDLE 構造体を処理します。 通知が特定のプロセッサを対象としていない場合、これは NULL になります。

通知値 PEP_NOTIFY_PPM_QUERY_COORDINATED_DEPENDENCY。

データ PEP_PPM_QUERY_COORDINATED_DEPENDENCY 構造体へのポインター。
各調整されたアイドル状態の依存関係を照会するために PEP に送信されます。

Windows 電源管理フレームワーク (PoFx) は、プロセッサの初期化時にこの通知を送信して、各調整されたアイドル状態の依存関係を PEP に照会します。 OS は、Dependencies 配列に MaximumDependencySize 要素を割り当てます。 PEP は、DependencySizeUsed で使用された配列の要素の数を入力する必要があります。

表現されている依存関係がプロセッサ上にある場合、PEP はターゲットプロセッサの POHANDLE を使用して TargetProcessor フィールドに入力します。 ExpectedState フィールドは、ターゲットプロセッサのプロセッサアイドル状態のインデックスを参照します。 

表現されている依存関係が他の調整されたアイドル状態である場合、PEP は TargetProcessor に NULL を入力します。 次に、ExpectedState フィールドは、調整されたアイドル状態のインデックスを参照します。 

各依存関係には、OS が依存関係を満たすために使用できるオプションのメニューが表示されます。 アイドル状態になると、OS は、上位のインデックスから最小のインデックスまでの条件をチェックすることによって、依存関係を満たすことを試みます。 依存関係の条件が満たされている場合、OS は依存関係が満たされていると見なします。 条件が満たされない場合、依存関係は満たされず、調整されたアイドル状態になる可能性があります。

PEP_NOTIFY_PPM_QUERY_COORDINATED_DEPENDENCY 通知の場合、AcceptProcessorNotification ルーチンは常に IRQL = PASSIVE_LEVEL で呼び出されます。

PASSIVE_LEVEL
 
## <a name="pep_notify_ppm_query_coordinated_state_name"></a>PEP_NOTIFY_PPM_QUERY_COORDINATED_STATE_NAME 
ターゲットプロセッサの PEP のデバイスハンドルを含む PEPHANDLE 構造体を処理します。 通知が特定のプロセッサを対象としていない場合、これは NULL になります。

通知値 PEP_NOTIFY_PPM_QUERY_COORDINATED_STATE_NAME。

データ PEP_PPM_QUERY_STATE_NAME 構造体へのポインター。
特定の調整またはプラットフォームのアイドル状態に関する情報を照会するために PEP に送信されます。

Windows 電源管理フレームワーク (PoFx) は、プロセッサの初期化時にこの通知を送信して、特定の調整またはプラットフォームのアイドル状態に関する情報を PEP に照会します。 この通知は、状態ごとに2回送信されます。1回は名前に必要な割り当てサイズを取得するための NULL 名バッファーで、もう1回は名前の内容を入力するための NULL 以外の名前バッファーを使用します。 名前は、ユーザーが判読できるように、調整されたアイドル状態の名前を示す文字列にする必要があります。 連携するアイドル状態には一意の名前が必要です。ただし、マルチクラスターシステムでは、異なるクラスター上の同じ状態の名前が同じになる場合があります。 WPA やカーネルデバッガーなどのデバッグツールでは、この調整/プラットフォームアイドル状態を参照する診断に名前が表示されます。

PEP_NOTIFY_PPM_QUERY_COORDINATED_STATE_NAME 通知の場合、AcceptProcessorNotification ルーチンは常に IRQL = PASSIVE_LEVEL で呼び出されます。

PASSIVE_LEVEL
 
## <a name="pep_notify_ppm_query_coordinated_states"></a>PEP_NOTIFY_PPM_QUERY_COORDINATED_STATES 
ターゲットプロセッサの PEP のデバイスハンドルを含む PEPHANDLE 構造体を処理します。 通知が特定のプロセッサを対象としていない場合、これは NULL になります。

通知値 PEP_NOTIFY_PPM_QUERY_COORDINATED_STATES。

データ PEP_PPM_QUERY_COORDINATED_STATES 構造体へのポインター。
プロセッサの初期化時に使用して、すべての連携アイドル状態のプロパティを照会します。

Windows 電源管理フレームワーク (PoFx) は、プロセッサの初期化時にこの通知を PEP に送信して、すべての連携アイドル状態のプロパティを照会します。 この通知は、PEP が PEP_NOTIFY_PPM_QUERY_PLATFORM_STATE 通知を送信する直前に送信されます。 許容される場合、PEP は、調整されたアイドル状態のインターフェイスを使用しており、PEP_NOTIFY_PPM_QUERY_PLATFORM_STATE 通知を受信しません。 受け入れられない場合、PEP はプラットフォームのアイドル状態のインターフェイスを使用し、OS は PEP_NOTIFY_PPM_QUERY_PLATFORM_STATE 通知を使用して、調整されたアイドル状態のクエリを実行します。 

OS は、すべてのプロセッサが PEP に登録されるまで、この通知の送信を待機します。 

PEP は、状態構造体に、時間の経過に伴うアイドル状態に関する情報を格納します。

調整されたアイドル状態の順序は、次の規則に従う必要があります。 

同じ機能単位の異なる電源状態を表す2つの調整された状態は、最低 (電力消費量/最小移行コスト) から最も深い (最小電力消費量/最も多くの移行コスト) までの順序で示される必要があります。 調整されたアイドル状態は、インデックスが小さい他の調整されたアイドル状態にのみ依存します。 2つの結合されていない連携したアイドル状態 (つまり、異なるプロセッサのセットに依存する2つの連携するアイドル状態) の間には、必須の順序はありません。

PEP_NOTIFY_PPM_QUERY_COORDINATED_STATES 通知の場合、AcceptProcessorNotification ルーチンは常に IRQL = PASSIVE_LEVEL で呼び出されます。

PASSIVE_LEVEL
 
## <a name="pep_notify_ppm_query_processor_state_name"></a>PEP_NOTIFY_PPM_QUERY_PROCESSOR_STATE_NAME 
ターゲットプロセッサの PEP のデバイスハンドルを含む PEPHANDLE 構造体を処理します。 通知が特定のプロセッサを対象としていない場合、これは NULL になります。

通知値 PEP_NOTIFY_PPM_QUERY_PROCESSOR_STATE_NAME。

データ PEP_PPM_QUERY_STATE_NAME 構造体へのポインター。
特定のプロセッサアイドル状態に関する情報を照会するために PEP に送信されます。

Windows 電源管理フレームワーク (PoFx) は、プロセッサの初期化時にこの通知を送信して、PEP に特定のプロセッサアイドル状態に関する情報を照会します。 この通知は、状態ごとに2回送信されます。1回は名前に必要な割り当てサイズを取得するための NULL 名バッファーで、もう1回は名前の内容を入力するための NULL 以外の名前バッファーを使用します。 名前は、ユーザーが判読できるように、調整されたアイドル状態の名前を示す文字列にする必要があります。 連携するアイドル状態には一意の名前が必要です。ただし、マルチクラスターシステムでは、異なるクラスター上の同じ状態の名前が同じになる場合があります。 WPA やカーネルデバッガーなどのデバッグツールでは、この調整/プラットフォームアイドル状態を参照する診断に名前が表示されます。

PEP_NOTIFY_PPM_QUERY_PROCESSOR_STATE_NAME 通知の場合、AcceptProcessorNotification ルーチンは常に IRQL = PASSIVE_LEVEL で呼び出されます。

PASSIVE_LEVEL
 
## <a name="pep_notify_ppm_enter_system_state"></a>PEP_NOTIFY_PPM_ENTER_SYSTEM_STATE 
ターゲットプロセッサの PEP のデバイスハンドルを含む PEPHANDLE 構造体を処理します。 通知が特定のプロセッサを対象としていない場合、これは NULL になります。

通知値 PEP_NOTIFY_PPM_ENTER_SYSTEM_STATE。

データ PEP_PPM_ENTER_SYSTEM_STATE 構造体へのポインター。
PEP_NOTIFY_PPM_ENTER_SYSTEM_STATE は、システムがシステムの電源状態を入力しようとしていることを PEP に通知するオプションの通知です。 この通知は、システムがすべてのパッシブレベルの作業を完了した後、すべてのプロセッサに同時に送信され、システムの電源状態に移行します。  

この通知は DISPATCH_LEVEL で送信され、すべてのプロセッサがディスパッチされます。 この通知は、常にターゲットプロセッサで実行されます。 

PEP は、この通知からのすべての作業をキューに置いてはいけないことに注意してください。 この通知が送信された後、プロセッサは作業項目、Dpc などを処理しません。 
 

DISPATCH_LEVEL
 
## <a name="pep_notify_ppm_perf_set_state"></a>PEP_NOTIFY_PPM_PERF_SET_STATE 
ターゲットプロセッサの PEP のデバイスハンドルを含む PEPHANDLE 構造体を処理します。 通知が特定のプロセッサを対象としていない場合、これは NULL になります。

通知値 PEP_NOTIFY_PPM_PERF_SET_STATE。

データ PEP_PPM_PERF_SET_STATE 構造体へのポインター。
実行時にプロセッサの現在の動作パフォーマンス状態を設定するために使用されます。 PEP がパフォーマンスセット要求なしにパフォーマンスをブースト/下げることができる自律ハードウェアを使用している場合は、最小パフォーマンス状態と最大パフォーマンス状態に基づいて自律ハードウェアからの要求を制限し、必要なものをターゲットにする必要があります。パフォーマンスの状態。 それ以外の場合は、目的のパフォーマンス状態で実行する必要があります。  

この通知は、DISPATCH_LEVEL で送信されます。 Scheduler の有向パフォーマンス状態が使用されている場合、PEP は、この通知を処理するときに、セクション3.3.6 の制限に従う必要があります。 任意のプロセッサで実行中に送信される場合があります。 

DISPATCH_LEVEL
 
## <a name="pep_notify_ppm_query_discrete_perf_states"></a>PEP_NOTIFY_PPM_QUERY_DISCRETE_PERF_STATES 
ターゲットプロセッサの PEP のデバイスハンドルを含む PEPHANDLE 構造体を処理します。 通知が特定のプロセッサを対象としていない場合、これは NULL になります。

通知値 PEP_NOTIFY_PPM_QUERY_DISCRETE_PERF_STATES。

データ PEP_PPM_QUERY_DISCRETE_PERF_STATES 構造体へのポインター。
PEP_NOTIFY_PPM_QUERY_CAPABILITIES 通知が個別のパフォーマンス状態のサポートを示す場合、プロセッサの初期化時に使用され、PEP がサポートする個別のパフォーマンス状態の一覧を照会します。  

パフォーマンスの状態の一覧は、パフォーマンスの状態がそれぞれ異なるパフォーマンス値にマッピングされている場合、最速から低速に設定する必要があります。 また、[パフォーマンスの状態] 一覧には、PEP_NOTIFY_PPM_QUERY_PERF_CAPABILITIES 通知に示されている各パフォーマンス値に一致するエントリが含まれている必要があります。  この通知は、PASSIVE_LEVEL で送信されます。 任意のプロセッサで実行中に送信される場合があります。 

PASSIVE_LEVEL
 
## <a name="pep_notify_ppm_query_domain_info"></a>PEP_NOTIFY_PPM_QUERY_DOMAIN_INFO 
ターゲットプロセッサの PEP のデバイスハンドルを含む PEPHANDLE 構造体を処理します。 通知が特定のプロセッサを対象としていない場合、これは NULL になります。

通知値 PEP_NOTIFY_PPM_QUERY_DOMAIN_INFO。

データ PEP_PPM_QUERY_DOMAIN_INFO 構造体へのポインター。
パフォーマンスドメインに関する情報を照会するオプションの通知。  この通知は、PASSIVE_LEVEL で送信されます。 任意のプロセッサで実行中に送信される場合があります。

PASSIVE_LEVEL

  
## <a name="pep_notify_ppm_resume_from_system_state"></a>PEP_NOTIFY_PPM_RESUME_FROM_SYSTEM_STATE 
ターゲットプロセッサの PEP のデバイスハンドルを含む PEPHANDLE 構造体を処理します。 通知が特定のプロセッサを対象としていない場合、これは NULL になります。

通知値 PEP_NOTIFY_PPM_RESUME_FROM_SYSTEM_STATE。

データ PEP_PPM_RESUME_FROM_SYSTEM_STATE 構造体へのポインター。
システムがシステムの電源状態から再開したばかりであることを PEP に通知するオプションの通知。 この通知は、パッシブレベルの作業を再開するためにプロセッサが解放される直前に、すべてのプロセッサに同時に送信されます。  この通知は DISPATCH_LEVEL で送信され、すべてのプロセッサがディスパッチされます。 この通知は、常にターゲットプロセッサで実行されます。 

DISPATCH_LEVEL
 

