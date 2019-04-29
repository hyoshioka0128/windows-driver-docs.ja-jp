---
title: デバイスの電源管理リファレンス
description: ドライバーを使用して詳細な電源管理を有効にする複数の論理コンポーネントへのデバイスのハードウェアを分割 Ddi をについて説明します。
keywords:
- AcceptDeviceNotification
ms.date: 12/17/2018
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: f57e13ce1653e1dadf3b7e8901db869adf47410c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388134"
---
# <a name="device-power-management-reference"></a>デバイスの電源管理リファレンス

ドライバーは、詳細な電源管理を有効にする複数の論理コンポーネントへのデバイスのハードウェアを分割できます。 コンポーネントには、他のコンポーネントを同じデバイスの電源の状態とは無関係に管理可能な電源状態のセットがあります。 F0 状態で、コンポーネントが完全に有効です。 コンポーネントを追加、低電力状態 F1、F2 サポート可能性があります。

デバイスの電源ポリシー所有者は、通常、デバイスの関数のドライバーです。 このドライバーをコンポーネント レベルの電源管理を有効にするを使用してデバイスを登録します、[電源管理フレームワーク (PoFx)](overview-of-the-power-management-framework.md)します。 デバイスを登録することでは、ドライバーは、コンポーネントが既に使用されていると、コンポーネントがアイドル状態のときに、PoFx を通知する責任を負います。 PoFx により、コンポーネントのアクティビティ、待機時間の許容範囲、予想されるアイドル状態の期間、およびウェイク要件に関する情報に基づいて、デバイスのアイドル状態のインテリジェントな選択肢です。 コンポーネント レベルの制御の電力使用状況、によって PoFx はシステムの応答性を維持しながら電源の要件を減らすことができます。 詳細については、次を参照してください。[コンポーネント レベルの電源管理](component-level-power-management.md)します。

## <a name="device-power-management-routines"></a>デバイスの電源管理ルーチン

これらのルーチンは、電源管理フレームワーク (PoFx) デバイスの電源管理を有効にして実装されます。 デバイスの電源ポリシー所有者 (PPO) である、ドライバーによっては、これらのルーチンが呼び出されます。 通常、デバイスの機能のドライバーは、このデバイスの PPO です。

|トピック|説明|
|----|----|
|[**PoFxActivateComponent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxactivatecomponent)|**PoFxActivateComponent**ルーチンは、指定したコンポーネントのアクティブ化の参照カウントをインクリメントします。|
|[PoFxCompleteDevicePowerNotRequired](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxcompletedevicepowernotrequired)|**PoFxCompleteDevicePowerNotRequired**ルーチンは、呼び出し元のドライバーがドライバーへの呼び出しに応答を完了したことを電源管理フレームワーク (PoFx) に通知[ *DevicePowerNotRequiredCallback* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_device_power_not_required_callback)コールバック ルーチン。|
|[**PoFxCompleteIdleCondition**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxcompleteidlecondition)|**PoFxCompleteIdleCondition**ルーチンは、指定したコンポーネントによってアイドル状態を保留中の変更が完了したことを電源管理フレームワーク (PoFx) に通知します。|
|[**PoFxCompleteIdleState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxcompleteidlestate)|PoFxCompleteIdleState ルーチンでは、指定したコンポーネントの [fx] 状態に保留中の変更が完了したこと、電源管理フレームワーク (PoFx) を通知します。|
|[**PoFxIdleComponent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxidlecomponent)|**PoFxIdleComponent**日常的な指定したコンポーネントのアクティブ化の参照カウントをデクリメントします。|
|[**PoFxIssueComponentPerfStateChange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxissuecomponentperfstatechange)|**PoFxIssueComponentPerfStateChange**ルーチンは、特定のパフォーマンスの状態で、デバイスのコンポーネントを配置する要求を送信します。|
|[**PoFxIssueComponentPerfStateChangeMultiple**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxissuecomponentperfstatechangemultiple)|**PoFxIssueComponentPerfStateChangeMultiple**ルーチンは、デバイス コンポーネントの複数のパフォーマンスの状態でパフォーマンスの状態を変更する要求を同時に設定を送信します。|
|[**PoFxNotifySurprisePowerOn**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxnotifysurprisepoweron)|**PoFxNotifySurprisePowerOn**ルーチンが他のデバイスに電力が供給の副作用として、デバイスがオンにされた電源管理フレームワーク (PoFx) を通知します。|
|[**PoFxPowerControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxpowercontrol)|**PoFxPowerControl**ルーチンは、電源管理フレームワーク (PoFx) に電源制御要求を送信します。|
|[**PoFxQueryCurrentComponentPerfState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxpowercontrol)|**PoFxQueryCurrentComponentPerfState**ルーチンは、コンポーネントのパフォーマンス状態のセット内のアクティブなパフォーマンスの状態を取得します。|
|[**PoFxRegisterComponentPerfStates**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxregistercomponentperfstates)|**PoFxRegisterComponentPerfStates**ルーチン、電源管理フレームワーク (PoFx) によってパフォーマンスの状態管理のデバイスのコンポーネントを登録します。|
|[**PoFxRegisterDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxregisterdevice)|**PoFxRegisterDevice**ルーチンが、電源管理フレームワーク (PoFx) をデバイスを登録します。|
|[**PoFxReportDevicePoweredOn**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxreportdevicepoweredon)|**PoFxReportDevicePoweredOn**ルーチンは、デバイスが、D0 (完全にオン) の電源状態への要求された移行を完了したこと、電源管理フレームワーク (PoFx) に通知します。|
|[**PoFxSetComponentLatency**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxsetcomponentlatency)|**PoFxSetComponentLatency**ルーチンがアイドル状態から指定したコンポーネントのアクティブな条件への移行で許容できる最大待機時間を指定します。|
|[**PoFxSetComponentResidency**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxsetcomponentresidency)|**PoFxSetComponentResidency**ルーチンは、コンポーネントがアイドル状態が入力した後、アイドル状態に可能性がどのくらいの時間の推定所要時間を設定します。|
|[**PoFxSetComponentWake**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxsetcomponentwake)|**PoFxSetComponentWake**ルーチンでは、ドライバーがアイドル状態が入力されるたびをウェイクするための指定したコンポーネントを準備するかどうかを示します。|
|[**PoFxSetDeviceIdleTimeout**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxsetdeviceidletimeout)|**PoFxSetDeviceIdleTimeout**ルーチンから、デバイスの最後のコンポーネントが、電源管理フレームワーク (PoFx) が、ドライバーを呼び出すときにアイドル状態に入ったときの最小時間間隔を指定する[ *DevicePowerNotRequiredCallback* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_device_power_not_required_callback)コールバック ルーチン。|
|[**PoFxStartDevicePowerManagement**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxstartdevicepowermanagement)|**PoFxStartDevicePowerManagement**ルーチンは、電源管理フレームワーク (PoFx) を使用したデバイスの登録が完了して、デバイスの電源管理を開始します。|
|[**PoFxUnregisterDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxunregisterdevice)|**PoFxUnregisterDevice**ルーチンは、電源管理フレームワーク (PoFx) から、デバイスの登録を削除します。|

## <a name="device-power-management-callbacks"></a>デバイスの電源管理のコールバック

これらのコールバック ルーチンは、デバイスの電源管理を有効にする電源管理フレームワーク (PoFx) によって要求されます。 デバイスの電源ポリシー所有者になっているドライバーでは、これらのコールバック ルーチンを実装します。 PoFx では、クエリを実行して、デバイスで、コンポーネントの電源の状態を構成するこれらのルーチンを呼び出します。

|トピック|説明|
|----|----|
|[ComponentActiveConditionCallback](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_component_active_condition_callback)|*ComponentActiveConditionCallback*コールバック ルーチンは、指定したコンポーネントがアイドル状態からアクティブな状態への移行を完了したことをドライバーに通知します。|
|[ComponentIdleConditionCallback](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_component_idle_condition_callback)|*ComponentIdleConditionCallback*コールバック ルーチンは、指定したコンポーネントがアクティブな状態からアイドル状態への移行を完了したことをドライバーに通知します。|
|[ComponentIdleStateCallback](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_component_idle_state_callback)|*ComponentIdleStateCallback*コールバック ルーチンが指定したコンポーネントの電源状態の [fx] に変更が保留中のドライバーに通知します。|
|[ComponentPerfStateCallback](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_component_perf_state_callback)|*ComponentPerfStateCallback*コールバック ルーチンは、コンポーネントのパフォーマンスの状態を変更するには、その要求が完了したことをドライバーに通知します。|
|[DevicePowerNotRequiredCallback](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_device_power_not_required_callback)|*DevicePowerNotRequiredCallback*コールバック ルーチンは、D0 電源の状態を維持するために、デバイスが必要ないことをデバイス ドライバーに通知します。|
|[DevicePowerRequiredCallback](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_device_power_required_callback)|*DevicePowerRequiredCallback*コールバック ルーチンがデバイス ドライバをデバイスが入力する必要があり、D0 の電源状態のままに通知します。|
|[PowerControlCallback](https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_power_control_callback)|*PowerControlCallback*コールバック ルーチンは、電源管理フレームワーク (PoFx) から要求される電源管理操作を実行します。|

## <a name="device-power-management-structures"></a>デバイスの電源管理の構造体

電源管理フレームワーク (PoFx) デバイスの電源管理をサポートするためにこれらの構造を定義します。

|トピック|説明|
|----|----|
|[PO_FX_COMPONENT_V1](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_po_fx_component_v1)   [PO_FX_COMPONENT_V2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_po_fx_component_v2)|**PO_FX_COMPONENT**構造体には、デバイス内のコンポーネントの電源状態の属性がについて説明します。|
|[PO_FX_COMPONENT_IDLE_STATE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_po_fx_component_idle_state)|**PO_FX_COMPONENT_IDLE_STATE**構造体は、デバイス コンポーネントの [fx] 電源状態の属性を指定します。|
|[PO_FX_COMPONENT_PERF_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_po_fx_component_perf_info)|**PO_FX_COMPONENT_PERF_INFO**構造体には、デバイス内の 1 つのコンポーネントのパフォーマンス状態のすべてのセットがについて説明します。|
|[PO_FX_COMPONENT_PERF_SET](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_po_fx_component_perf_set)|**PO_FX_COMPONENT_PERF_SET**構造体は、一連のデバイス内の 1 つのコンポーネントのパフォーマンス状態を表します。|
|[PO_FX_DEVICE_V1](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_po_fx_device_v1)   [PO_FX_DEVICE_V2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_po_fx_device_v2)   [PO_FX_DEVICE_V3](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_po_fx_device_v3)|**PO_FX_DEVICE**構造体が、電源管理フレームワーク (PoFx) にデバイスの電源の属性について説明します。|
|[PO_FX_PERF_STATE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_po_fx_perf_state)|**PO_FX_PERF_STATE**構造体は、デバイス内の 1 つのコンポーネントのパフォーマンス状態を表します。|
|[PO_FX_PERF_STATE_CHANGE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_po_fx_perf_state_change)|**PO_FX_PERF_STATE_CHANGE**構造には、呼び出すことによって要求されているパフォーマンスの状態の変更に関する情報が含まれる、 [PoFxIssueComponentPerfStateChange](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxissuecomponentperfstatechange)または[PoFxIssueComponentPerfStateChangeMultiple](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxissuecomponentperfstatechangemultiple)ルーチン。

## <a name="device-power-management-enumerations"></a>デバイスの電源管理の列挙型

電源管理フレームワーク (PoFx) は、デバイスの電源管理をサポートするためにこれらの列挙体を定義します。

|トピック|説明|
|----|----|
|[PO_FX_PERF_STATE_TYPE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ne-wdm-_po_fx_perf_state_type)|**PO_FX_PERF_STATE_TYPE**列挙には、パフォーマンスの状態の種類を記述する値が含まれています、 [PO_FX_COMPONENT_PERF_SET](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_po_fx_component_perf_set)します。|
|[PO_FX_PERF_STATE_UNIT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ne-wdm-_po_fx_perf_state_unit)|**PO_FX_PERF_STATE_UNIT**列挙にはでパフォーマンスの状態によって制御されるユニットの種類を記述する値が含まれています、 [PO_FX_COMPONENT_PERF_SET](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_po_fx_component_perf_set)します。

## <a name="device-power-management-constants"></a>デバイスの電源管理の定数

### <a name="pofxflagxxx-flag-bits"></a>PO_FX_FLAG_XXX フラグのビット

**PO_FX_FLAG_XXX**定数は、コンポーネントの状態を変更する要求が同期的または非同期的に実行されたかどうかを示すフラグ ビットです。

```c++
#define PO_FX_FLAG_BLOCKING   0x1
#define PO_FX_FLAG_ASYNC_ONLY 0x2
```

#### <a name="pofxflagxxx-constants"></a>PO_FX_FLAG_XXX 定数

|定数|説明|
|----|----|
|PO_FX_FLAG_BLOCKING|条件の変更を同期させます。 このフラグが設定されている場合、条件の変更を要求するルーチンは制御を返しません呼び出し元のドライバー コンポーネントのハードウェアが、新しい条件への移行を完了するまでです。 このフラグは、IRQL で呼び出し元が実行されている場合にのみ使用できます < DISPATCH_LEVEL します。|
|PO_FX_FLAG_ASYNC_ONLY|条件の変更を完全に非同期に確認します。 このフラグが設定されている場合、呼び出し元のドライバーのコールバック ルーチンは、条件の変更を要求するルーチンが呼び出されるスレッド以外のスレッドから呼び出されます。 したがって、条件の変更を常に要求するルーチンは、コールバックが完了するを待つことがなく非同期的に返します。|

#### <a name="pofxflagxxx-remarks"></a>PO_FX_FLAG_XXX 解説

次のルーチンをフラグ パラメーターを設定することができます、 **PO_FX_FLAG_XXX**定数。

- [PoFxActivateComponent](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxactivatecomponent)
- [PoFxIdleComponent](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxidlecomponent)
- [PoFxIssueComponentPerfStateChange](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxissuecomponentperfstatechange)
- [PoFxIssueComponentPerfStateChangeMultiple](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxissuecomponentperfstatechangemultiple)

**PO_FX_FLAG_BLOCKING**と**PO_FX_FLAG_ASYNC_ONLY**フラグのビットは相互に排他的です。 呼び出し元が両方のフラグのビットは、フラグ パラメーターでは、1 つまたはその他のフラグのビットを設定できます。

#### <a name="pofxflagxxx-requirements"></a>PO_FX_FLAG_XXX 要件

|バージョン|Header|
|----|----|
|Windows 8 以降でサポートされています。|Wdm.h|

### <a name="pofxflagperfxxx-flag-bits"></a>PO_FX_FLAG_PERF_XXX フラグのビット

**PO_FX_FLAG_PERF_XXX**定数は、電源管理フレームワーク (PoFx) が、デバイスのコンポーネントのパフォーマンス状態を管理する方法を定義するフラグ ビットです。

```c++
#define PO_FX_FLAG_PERF_PEP_OPTIONAL   0x1
#define PO_FX_FLAG_PERF_QUERY_ON_F0 0x2
#define PO_FX_FLAG_PERF_QUERY_ON_ALL_IDLE_STATES 0x4
```

|定数|Value|説明|
|----|----|----|
|**PO_FX_FLAG_PERF_PEP_OPTIONAL**|1 (0x1)|ドライバーが、プラットフォーム拡張機能からプラグイン (PEP) の支援なしのパフォーマンス状態を変更できますか、ドライバーはパフォーマンス状態 PoFx でログ目的でのみ登録ことを示します。 このフラグが設定されている場合、 [PoFxRegisterComponentPerfStates](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxregistercomponentperfstates)呼び出しは引き続き、PEP は、コンポーネントのパフォーマンス状態をサポートしていない場合に成功しました。|
|**PO_FX_FLAG_PERF_QUERY_ON_F0**|2 (0x2)|一部のデバイスでは、PEP はパフォーマンスの状態が特定のパフォーマンスの状態にコンポーネントの設定の場所に必要があります (と呼ばれる、*名目上のパフォーマンスの状態*) コンポーネントがアイドル状態とします。 ドライバーは、コンポーネントには、標準のパフォーマンスの状態、ケース PoFx のコンポーネントが F0 に移行するときに、現在のパフォーマンスの状態を判断する、PEP のクエリが含まれている場合、このフラグを設定します。|
|**PO_FX_FLAG_PERF_QUERY_ON_ALL_IDLE_STATES**|4 (0x4)|一部のデバイスでは、PEP はパフォーマンスの状態が特定のパフォーマンスの状態にコンポーネントの設定の場所に必要があります (と呼ばれる、*名目上のパフォーマンスの状態*)、コンポーネント間アイドル状態に遷移するときにします。 ドライバーは、このコンポーネントには、標準のパフォーマンスの状態、PoFx ケースが、コンポーネントのアイドル状態が遷移するときに現在のパフォーマンス状態を確認する、PEP をクエリが含まれている場合、このフラグを設定します。|

#### <a name="pofxflagperfxxx-remarks"></a>PO_FX_FLAG_PERF_XXX 解説

フラグ パラメーターを[PoFxRegisterComponentPerfStates](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxregistercomponentperfstates)ルーチンに設定することができます、 **PO_FX_FLAG_PERF_XXX**定数。

#### <a name="pofxflagperfxxx-requirements"></a>PO_FX_FLAG_PERF_XXX 要件

|必要条件|バージョン|
|----|----|
|Windows 10 以降でサポートされています。|Wdm.h|
