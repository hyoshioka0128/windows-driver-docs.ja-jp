---
title: デバイスの電源管理リファレンス
description: ドライバーがデバイスハードウェアを複数の論理コンポーネントに分割して詳細な電源管理を可能にする DDIs について説明します。
keywords:
- AcceptDeviceNotification
ms.date: 12/17/2018
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 9ddd586e4d302b1994ae118582e429d4a5fda90a
ms.sourcegitcommit: ba3199328ea5d80119eafc399dc989e11e7ae1d6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "74860568"
---
# <a name="device-power-management-reference"></a>デバイスの電源管理リファレンス

ドライバーは、デバイスのハードウェアを複数の論理コンポーネントに分割して、きめ細かく電源管理を行うことができます。 コンポーネントには、同じデバイス内の他のコンポーネントの電力状態とは別に管理できる一連の電源状態があります。 F0 状態では、コンポーネントは完全にオンになっています。 コンポーネントは、追加の低電力状態の F1、F2 などをサポートする場合があります。

デバイスの電源ポリシー所有者は、通常、デバイスの関数ドライバーです。 コンポーネントレベルの電源管理を有効にするために、このドライバーはデバイスを[電源管理フレームワーク (PoFx)](overview-of-the-power-management-framework.md)に登録します。 デバイスを登録することにより、ドライバーは、コンポーネントがアクティブに使用されているときと、コンポーネントがアイドル状態になったときに、PoFx に通知する役割を担います。 PoFx を使用すると、コンポーネントのアクティビティ、待機時間の許容範囲、予想されるアイドル期間、およびウェイクの要件に関する情報に基づいて、デバイスのインテリジェントなアイドル状態を選択できます。 コンポーネントレベルで電力使用量を制御することで、PoFx はシステムの応答性を維持しながら電力要件を減らすことができます。 詳細については、「[コンポーネントレベルの電源管理](component-level-power-management.md)」を参照してください。

## <a name="device-power-management-routines"></a>デバイスの電源管理ルーチン

これらのルーチンは、デバイスの電源管理を有効にするために、電源管理フレームワーク (PoFx) によって実装されています。 これらのルーチンは、デバイスの電源ポリシー所有者 (PPO) であるドライバーによって呼び出されます。 通常、デバイスの関数ドライバーは、このデバイスの PPO です。

|トピック|説明|
|----|----|
|[**PoFxActivateComponent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxactivatecomponent)|**PoFxActivateComponent**ルーチンは、指定されたコンポーネントのアクティブ化参照カウントをインクリメントします。|
|[PoFxCompleteDevicePowerNotRequired](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxcompletedevicepowernotrequired)|**PoFxCompleteDevicePowerNotRequired**ルーチンは、呼び出し元のドライバーがドライバーの[*Devicepowernotrequiredcallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_device_power_not_required_callback)コールバックルーチンへの呼び出しへの応答を完了したことを、電源管理フレームワーク (pofx) に通知します。|
|[**PoFxCompleteIdleCondition**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxcompleteidlecondition)|**PoFxCompleteIdleCondition**ルーチンは、指定されたコンポーネントがアイドル状態に対する保留中の変更を完了したことを、電源管理フレームワーク (pofx) に通知します。|
|[**PoFxCompleteIdleState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxcompleteidlestate)|PoFxCompleteIdleState ルーチンは、指定されたコンポーネントが Fx 状態に対する保留中の変更を完了したことを、電源管理フレームワーク (PoFx) に通知します。|
|[**PoFxIdleComponent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxidlecomponent)|**PoFxIdleComponent**ルーチンは、指定されたコンポーネントのアクティブ化参照カウントをデクリメントします。|
|[**PoFxIssueComponentPerfStateChange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxissuecomponentperfstatechange)|**PoFxIssueComponentPerfStateChange**ルーチンは、特定のパフォーマンス状態にデバイスコンポーネントを配置する要求を送信します。|
|[**PoFxIssueComponentPerfStateChangeMultiple**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxissuecomponentperfstatechangemultiple)|**PoFxIssueComponentPerfStateChangeMultiple**ルーチンは、デバイスコンポーネントの複数のパフォーマンス状態セットのパフォーマンス状態を同時に変更する要求を送信します。|
|[**PoFxNotifySurprisePowerOn**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxnotifysurprisepoweron)|**PoFxNotifySurprisePowerOn**ルーチンは、他のデバイスに電力を供給する副作用としてデバイスがオンになったことを、電源管理フレームワーク (pofx) に通知します。|
|[**PoFxPowerControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxpowercontrol)|**Pofxpowercontrol**ルーチンは、電源管理フレームワーク (pofx) に電源管理要求を送信します。|
|[**PoFxQueryCurrentComponentPerfState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxpowercontrol)|**Pofxquerycurrentcomponentperfstate**ルーチンは、コンポーネントのパフォーマンス状態セット内のアクティブなパフォーマンス状態を取得します。|
|[**PoFxRegisterComponentPerfStates**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxregistercomponentperfstates)|**Pofxregistercomponentperfstates**ルーチンは、電源管理フレームワーク (pofx) によるパフォーマンス状態管理のためにデバイスコンポーネントを登録します。|
|[**PoFxRegisterDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxregisterdevice)|**Pofxregisterdevice**ルーチンは、デバイスを電源管理フレームワーク (pofx) に登録します。|
|[**PoFxReportDevicePoweredOn**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxreportdevicepoweredon)|**Pofxreportdevicepoweredon**ルーチンは、デバイスが D0 (フルオン) の電源状態への要求された移行を完了したことを、電源管理フレームワーク (pofx) に通知します。|
|[**PoFxSetComponentLatency**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxsetcomponentlatency)|**Pofxsetcomponentlatency**ルーチンは、指定されたコンポーネントのアイドル状態からアクティブ条件への移行で許容できる最大待機時間を指定します。|
|[**PoFxSetComponentResidency**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxsetcomponentresidency)|**Pofxsetcomponentresidency**ルーチンは、コンポーネントがアイドル状態になった後に、コンポーネントがアイドル状態のままになる可能性のある推定時間を設定します。|
|[**PoFxSetComponentWake**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxsetcomponentwake)|**Pofxsetcomponentwake**ルーチンは、コンポーネントがアイドル状態になるたびに、ドライバーが指定されたコンポーネントをスリープ解除するかどうかを示します。|
|[**PoFxSetDeviceIdleTimeout**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxsetdeviceidletimeout)|**PoFxSetDeviceIdleTimeout**ルーチンは、電源管理フレームワーク (pofx) がドライバーの[*Devicepowernotrequiredcallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_device_power_not_required_callback)コールバックルーチンを呼び出すときに、デバイスの最後のコンポーネントがアイドル状態になるまでの最短時間間隔を指定します。|
|[**PoFxStartDevicePowerManagement**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxstartdevicepowermanagement)|**Pofxstartdevicepowermanagement**ルーチンは、電源管理フレームワーク (pofx) によるデバイスの登録を完了し、デバイスの電源管理を開始します。|
|[**PoFxUnregisterDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxunregisterdevice)|**Pofxunregisterdevice**ルーチンは、電源管理フレームワーク (pofx) からデバイスの登録を削除します。|

## <a name="device-power-management-callbacks"></a>デバイスの電源管理コールバック

これらのコールバックルーチンは、デバイスの電源管理を有効にするために、電源管理フレームワーク (PoFx) によって要求されます。 デバイスの電源ポリシー所有者であるドライバーは、これらのコールバックルーチンを実装します。 PoFx は、これらのルーチンを呼び出して、デバイス内のコンポーネントの電源状態を照会および構成します。

|トピック|説明|
|----|----|
|[ComponentActiveConditionCallback](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_component_active_condition_callback)|*ComponentActiveConditionCallback* callback ルーチンは、指定されたコンポーネントがアイドル状態からアクティブな状態への遷移を完了したことをドライバーに通知します。|
|[ComponentIdleConditionCallback](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_component_idle_condition_callback)|*ComponentIdleConditionCallback* callback ルーチンは、指定されたコンポーネントがアクティブな状態からアイドル状態への遷移を完了したことをドライバーに通知します。|
|[ComponentIdleStateCallback](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_component_idle_state_callback)|*ComponentIdleStateCallback*コールバックルーチンは、指定されたコンポーネントの Fx 電源状態に対する保留中の変更をドライバーに通知します。|
|[ComponentPerfStateCallback](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_component_perf_state_callback)|*ComponentPerfStateCallback*コールバックルーチンは、コンポーネントのパフォーマンス状態の変更要求が完了したことをドライバーに通知します。|
|[DevicePowerNotRequiredCallback](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_device_power_not_required_callback)|*Devicepowernotrequiredcallback*コールバックルーチンは、デバイスが D0 電源状態のままである必要がないことをデバイスドライバーに通知します。|
|[DevicePowerRequiredCallback](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_device_power_required_callback)|*Devicepowerrequiredcallback*コールバックルーチンは、デバイスを入力して D0 の電源状態を維持する必要があることをデバイスドライバーに通知します。|
|[PowerControlCallback](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_power_control_callback)|*Powercontrolcallback*コールバックルーチンは、電源管理フレームワーク (pofx) によって要求された電源管理操作を実行します。|

## <a name="device-power-management-structures"></a>デバイスの電源管理構造

電源管理フレームワーク (PoFx) は、デバイスの電源管理をサポートするためにこれらの構造を定義します。

|トピック|説明|
|----|----|
|[PO_FX_COMPONENT_V1](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_po_fx_component_v1)   [PO_FX_COMPONENT_V2](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_po_fx_component_v2)|**PO_FX_COMPONENT**構造体は、デバイス内のコンポーネントの電源状態属性を記述します。|
|[PO_FX_COMPONENT_IDLE_STATE](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_po_fx_component_idle_state)|**PO_FX_COMPONENT_IDLE_STATE**構造体は、デバイス内のコンポーネントの FX 電源状態の属性を指定します。|
|[PO_FX_COMPONENT_PERF_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_po_fx_component_perf_info)|**PO_FX_COMPONENT_PERF_INFO**構造体は、デバイス内の1つのコンポーネントについて、すべてのパフォーマンス状態のセットを記述します。|
|[PO_FX_COMPONENT_PERF_SET](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_po_fx_component_perf_set)|**PO_FX_COMPONENT_PERF_SET**構造体は、デバイス内の1つのコンポーネントに対するパフォーマンス状態のセットを表します。|
|[PO_FX_DEVICE_V1](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_po_fx_device_v1)   [PO_FX_DEVICE_V2](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_po_fx_device_v2)   [PO_FX_DEVICE_V3](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-po_fx_device_v3)|**PO_FX_DEVICE**構造は、電源管理フレームワーク (pofx) に対するデバイスの電源属性を記述します。|
|[PO_FX_PERF_STATE](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_po_fx_perf_state)|**PO_FX_PERF_STATE**構造体は、デバイス内の1つのコンポーネントのパフォーマンス状態を表します。|
|[PO_FX_PERF_STATE_CHANGE](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_po_fx_perf_state_change)|**PO_FX_PERF_STATE_CHANGE**構造体には、 [PoFxIssueComponentPerfStateChange](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxissuecomponentperfstatechange)または[PoFxIssueComponentPerfStateChangeMultiple](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxissuecomponentperfstatechangemultiple)ルーチンを呼び出すことによって要求されているパフォーマンス状態への変更に関する情報が含まれています。

## <a name="device-power-management-enumerations"></a>デバイスの電源管理の列挙

電源管理フレームワーク (PoFx) は、デバイスの電源管理をサポートするために、これらの列挙を定義します。

|トピック|説明|
|----|----|
|[PO_FX_PERF_STATE_TYPE](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_po_fx_perf_state_type)|**PO_FX_PERF_STATE_TYPE**列挙には、 [PO_FX_COMPONENT_PERF_SET](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_po_fx_component_perf_set)のパフォーマンス状態の種類を示す値が含まれます。|
|[PO_FX_PERF_STATE_UNIT](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_po_fx_perf_state_unit)|**PO_FX_PERF_STATE_UNIT**列挙には、 [PO_FX_COMPONENT_PERF_SET](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_po_fx_component_perf_set)のパフォーマンス状態によって制御される単位の種類を示す値が含まれます。

## <a name="device-power-management-constants"></a>デバイスの電源管理定数

### <a name="po_fx_flag_xxx-flag-bits"></a>PO_FX_FLAG_XXX フラグビット

**PO_FX_FLAG_XXX**定数は、コンポーネントの条件を変更する要求が同期または非同期で実行されるかどうかを示すフラグビットです。

```c++
#define PO_FX_FLAG_BLOCKING   0x1
#define PO_FX_FLAG_ASYNC_ONLY 0x2
```

#### <a name="po_fx_flag_xxx-constants"></a>PO_FX_FLAG_XXX 定数

|定数|説明|
|----|----|
|PO_FX_FLAG_BLOCKING|条件を同期的に変更します。 このフラグが設定されている場合、条件の変更を要求するルーチンは、コンポーネントハードウェアが新しい条件への移行を完了するまで、呼び出し元ドライバーに制御を返しません。 このフラグは、呼び出し元が IRQL < DISPATCH_LEVEL で実行されている場合にのみ使用できます。|
|PO_FX_FLAG_ASYNC_ONLY|条件を完全に非同期に変更します。 このフラグが設定されている場合、呼び出し元ドライバーのコールバックルーチンは、条件の変更を要求するルーチンが呼び出されたスレッド以外のスレッドから呼び出されます。 このため、条件の変更を要求するルーチンは、コールバックの完了を待たずに、常に非同期に戻ります。|

#### <a name="po_fx_flag_xxx-remarks"></a>PO_FX_FLAG_XXX 解説

次のルーチンに対する Flags パラメーターは、 **PO_FX_FLAG_XXX**定数に設定できます。

- [PoFxActivateComponent](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxactivatecomponent)
- [PoFxIdleComponent](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxidlecomponent)
- [PoFxIssueComponentPerfStateChange](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxissuecomponentperfstatechange)
- [PoFxIssueComponentPerfStateChangeMultiple](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxissuecomponentperfstatechangemultiple)

**PO_FX_FLAG_BLOCKING**と**PO_FX_FLAG_ASYNC_ONLY**のフラグビットは相互に排他的です。 呼び出し元は、Flags パラメーターに1つまたは他のフラグビットを設定できますが、両方を設定することはできません。

#### <a name="po_fx_flag_xxx-requirements"></a>PO_FX_FLAG_XXX の要件

|バージョン|Header|
|----|----|
|Windows 8 以降でサポートされています。|Wdm.h|

### <a name="po_fx_flag_perf_xxx-flag-bits"></a>PO_FX_FLAG_PERF_XXX フラグビット

**PO_FX_FLAG_PERF_XXX**定数は、電源管理フレームワーク (pofx) がデバイスコンポーネントのパフォーマンス状態をどのように管理するかを定義するフラグビットです。

```c++
#define PO_FX_FLAG_PERF_PEP_OPTIONAL   0x1
#define PO_FX_FLAG_PERF_QUERY_ON_F0 0x2
#define PO_FX_FLAG_PERF_QUERY_ON_ALL_IDLE_STATES 0x4
```

|定数|Value|説明|
|----|----|----|
|**PO_FX_FLAG_PERF_PEP_OPTIONAL**|1 (0x1)|ドライバーがプラットフォーム拡張機能プラグイン (PEP) の支援なしにパフォーマンス状態を変更できること、またはドライバーがログ記録のために PoFx にパフォーマンス状態を登録していることを示します。 このフラグが設定されている場合は、PEP がコンポーネントのパフォーマンスの状態をサポートしていない場合でも、 [Pofxregistercomponentperfstates](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxregistercomponentperfstates)の呼び出しは成功します。|
|**PO_FX_FLAG_PERF_QUERY_ON_F0**|2 (0x2)|一部のデバイスでは、PEP はコンポーネントをアイドル状態するときに、コンポーネントのパフォーマンス状態を特定のパフォーマンス状態 (*公称パフォーマンス状態*と呼びます) に設定する必要がある場合があります。 [ドライバー] コンポーネントに公称パフォーマンス状態が含まれている場合、このフラグを設定します。この場合、コンポーネントが F0 に移行するときに、PoFx によって PEP にクエリが実行され、現在のパフォーマンス状態が判断されます。|
|**PO_FX_FLAG_PERF_QUERY_ON_ALL_IDLE_STATES**|4 (0x4)|一部のデバイスでは、PEP はコンポーネントをアイドル状態の間で遷移させるときに、コンポーネントのパフォーマンス状態を特定のパフォーマンス状態 (*公称パフォーマンス状態*と呼びます) に設定する必要がある場合があります。 [ドライバー] このフラグは、このコンポーネントに公称パフォーマンス状態が含まれている場合に設定されます。この場合、PoFx は、コンポーネントがアイドル状態に移行するときに、現在のパフォーマンスの状態を判断するために PEP に対してクエリを実行します。|

#### <a name="po_fx_flag_perf_xxx-remarks"></a>PO_FX_FLAG_PERF_XXX 解説

[Pofxregistercomponentperfstates](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxregistercomponentperfstates)ルーチンの Flags パラメーターは、 **PO_FX_FLAG_PERF_XXX**定数に設定できます。

#### <a name="po_fx_flag_perf_xxx-requirements"></a>PO_FX_FLAG_PERF_XXX の要件

|要件|バージョン|
|----|----|
|Windows 10 以降でサポートされています。|Wdm.h|
