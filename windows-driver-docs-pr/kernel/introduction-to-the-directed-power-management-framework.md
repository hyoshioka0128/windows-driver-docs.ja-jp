---
title: 指示電源管理フレームワークの概要
description: 電源管理フレームワーク、または Power Framework の一部である DFx、バージョン3について説明します。
ms.assetid: 58550c57-3439-4212-b0c6-6a2fbfd38414
ms.date: 02/21/2020
ms.custom: 19H1
ms.openlocfilehash: 0759e31fce138294a61deddb86be642ee993054e
ms.sourcegitcommit: c9e5aa086b72ae9c1a31bf952d0711383cfd4bbd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/25/2020
ms.locfileid: "77575210"
---
# <a name="introduction-to-the-directed-power-management-framework"></a>指示電源管理フレームワークの概要

Windows 10 バージョン1903以降のランタイム電源管理フレームワーク ([Pofx](https://docs.microsoft.com/windows-hardware/drivers/kernel/overview-of-the-power-management-framework)) では、オプションの有向電源モデルであるダイレクト Pofx (DFx) が提供されています。

DFx を使用すると、オペレーティングシステムは、システムがアイドル状態に移行し、[アクティベーター](https://docs.microsoft.com/windows-hardware/design/device-experiences/activators)仲介型ソフトウェアアクティビティが存在しない場合に、適切な低電力アイドル状態を入力するようにデバイススタックに指示します。これにより、システムが低電力の電力をより確実に入力できるようになります。

この目的は、システムの電力効率を高め、Windows デバイスのエネルギー消費量をフォームファクター全体に抑えることです。

DFx は、現在、D 状態制約のみのデバイスでサポートされています。  DFx は、F 状態の制約があるデバイスのサブツリーをスキップします。

DFx は、ページングやデバッグデバイスの電源を入れません。

## <a name="requirements-for-wdf-non-miniport-drivers"></a>WDF (非ミニポート) ドライバーの要件

[WDF_DEVICE_POWER_POLICY_IDLE_SETTINGS](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_device_power_policy_idle_settings)構造体で**SystemManagedIdleTimeout**または**SystemManagedIdleTimeoutWithHint**を指定する WDF ドライバーは、 [DDINSTALL. HW セクション](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-hw-section)内の INF の[AddReg ディレクティブセクション](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)に次のレジストリキーを追加することで、DFx を選択できます。

```
HKR,"WDF","WdfDirectedPowerTransitionEnable",0x00010001,1
```

システム管理のアイドルタイムアウトを要求すると、ドライバーの代わりに WDF が PoFx に登録されるため、このシナリオではドライバーを PoFx に登録する必要がありません。

ドライバーで**DriverManagedIdleTimeout**が指定されている場合は、システム管理のアイドルタイムアウトに切り替えることを検討してください。  それが不可能な場合は、以下の WDM セクションのガイドラインを使用して、DFx を選択してください。

WDF ドライバーがランタイム電源管理を使用していない場合は、そのサポートを追加し、システム管理のアイドルタイムアウトを使用します。  これを行うには、 [**WdfDeviceAssignS0IdleSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings)への入力として[WDF_DEVICE_POWER_POLICY_IDLE_SETTINGS](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_device_power_policy_idle_settings)構造体を指定します。

## <a name="requirements-for-wdm-non-miniport-drivers"></a>WDM (ミニポート以外) ドライバーの要件

ドライバーが、WDF によって提供されるシステム管理のアイドルサポートを使用していない場合 (ドライバーは、[ドライバーで管理](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/ne-wdfdevice-_wdf_power_policy_idle_timeout_type)されているアイドル状態のドライバーまたは WDM ドライバーのいずれか)、pofx に登録することによって、DFx のサポートを受けることができます。  このシナリオでは、ドライバーは以下を実装して PoFx に登録します。

- [PO_FX_DIRECTED_POWER_DOWN_CALLBACK コールバック関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_directed_power_down_callback)
- [PO_FX_DIRECTED_POWER_UP_CALLBACK コールバック関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_directed_power_up_callback)


[**Pofxregisterdevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxregisterdevice)関数に入力される[PO_FX_DEVICE_V3](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-po_fx_device_v3)構造体で、これらのコールバックへのポインターを提供します。

DFx のサポートを受けるには、ドライバーが次のことを行う必要があります。

* PoFx の登録時に `PO_FX_DIRECTED_POWER*` コールバックを指定する
* Sx 遷移から再開するときに、 [PO_FX_DIRECTED_POWER_UP_CALLBACK](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_directed_power_up_callback)コールバック関数から[**Pofxreportdevicepoweredon**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxreportdevicepoweredon)を呼び出します。

## <a name="example"></a>例

次の例は、上記で説明した自己登録オプションを示しています。

```
PO_FX_DEVICE_V3 MyPoFxDevice;
POHANDLE MyPoFxHandle;

RtlZeroMemory(&MyPoFxDevice, sizeof(PO_FX_DEVICE_V3));
MyPoFxDevice.Version = PO_FX_VERSION_V3;

// Initialize other PoFx callbacks and other fields like
// components and their idle states.

MyPoFxDevice.DirectedPowerUpCallback = <Driver's DFx power up callback>
MyPoFxDevice.DirectedPowerDownCallback = <Driver's DFx power down callback>

Status = PoFxRegisterDevice(
  <Driver's device object>,
  (PPO_FX_DEVICE)&MyPoFxDevice,
  &MyPoFxHandle);
  if (!NT_SUCCESS(Status)) {
  return Status;
}
```

ドライバーが以前に `PO_FX_VERSION_V1` 指定されている場合、`PO_FX_DEVICE_V3` 構造体はコンポーネント配列構造に `PO_FX_COMPONENT_V2` を使用することに注意してください。

## <a name="requirements-for-miniport-drivers"></a>ミニポートドライバーの要件

ポート/ミニポートドライバーモデルに従うデバイスクラスの場合、システム指定のポートドライバーは通常、電源ポリシーの所有権を処理します。  対応するポートドライバーが DFx のサポートを処理することが想定されているため、ほとんどのミニポートでは、DFx を選択するためにコードの変更を要求する必要はありません。

## <a name="testing"></a>Testing (テスト)

Microsoft では、DFx に対して3つのテストを提供しています。ユーザー指定のデバイスをテストするための[Windows Driver Kit](https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk)の単一デバイステスト、デバイスレベルの HLK テスト、システム上のすべてのデバイスのテストを目的としたシステムレベルの HLK テストです。

単一デバイステストは、WDK に付属する[Pwrtest](https://docs.microsoft.com/windows-hardware/drivers/devtest/pwrtest)ツールの一部として利用できます。  このツールにアクセスするには、`/directedfx` スイッチを使用してツールを実行します。  詳細については、「 [Pwrtest](../devtest/pwrtest-directedfx-scenario.md)を使用したテストのシナリオ」を参照してください。

HLK テストの詳細については、次のページを参照してください。

- [有向 FX 単一デバイス テスト](https://docs.microsoft.com/windows-hardware/test/hlk/testref/34cfdfa6-7826-443c-9717-bc28c3166092)
- [有向 FX システムの検証テスト](https://docs.microsoft.com/windows-hardware/test/hlk/testref/def16163-9118-4d4a-b559-37873befa12e)

S4 からの再開後にドライバーが[Pofxreportdevicepoweredon](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxreportdevicepoweredon)を正常に呼び出すことができない可能性がある場合は、s4 からの移行後に DFx をテストすることをお勧めします。

## <a name="dfx-and-s-state-transitions"></a>DFx と S 状態遷移

- DFx 遷移のターゲット D 状態は、ランタイム D3 (RTD3) の場合と同じである必要があります。これは、S3/S4 遷移のターゲット D 状態とは異なる場合があります。  デバイスが RTD3 に D2 を入力し、S3/S4 の場合は D3 に入るシナリオを考えてみましょう。  この場合、DFx のターゲット D 状態は D2 にする必要があります。
- 同様に、DFx の arm 対応の動作は、RTD3 の場合と同じである必要があります。これは、S3/S4 遷移で使用されるものとは異なる場合があります。  たとえば、RTD3 の場合、デバイスは D2/ウェイクに入ることができますが、S3/S4 の場合は「D3/ウェイクアップ」と入力します。  このシナリオでは、DFx の移行も D2/ウェイクに入る必要があります。

## <a name="dfx-and-runtime-d3-rtd3"></a>DFx とランタイム D3 (RTD3)

- RTD3 を使用すると、デバイスは通常、アイドル状態になったときに低電力の状態になります。  新しい作業が到着すると、デバイスはすぐに D0 に復帰します。  DFx を使用すると、デバイスは引き続きターゲットの D 状態 (およびキューでの新しい作業を保留) のままにして、PoFx によって電源バックアップが行われるようにする必要があります。


## <a name="see-also"></a>参照

- [モダン スタンバイのためのハードウェアの準備](https://docs.microsoft.com/windows-hardware/design/device-experiences/prepare-hardware-for-modern-standby)
- [PwrTest](https://docs.microsoft.com/windows-hardware/drivers/devtest/pwrtest)
- [PO_FX_DEVICE_V3 構造体](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-po_fx_device_v3)
- [PO_FX_DIRECTED_POWER_DOWN_CALLBACK コールバック関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_directed_power_down_callback)
- [PO_FX_DIRECTED_POWER_UP_CALLBACK コールバック関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_directed_power_up_callback)
- [PoFxCompleteDirectedPowerDown 関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxcompletedirectedpowerdown) 
- [PwrTest DirectedFx シナリオ](../devtest/pwrtest-directedfx-scenario.md)
- [有向 FX 単一デバイス テスト](https://docs.microsoft.com/windows-hardware/test/hlk/testref/34cfdfa6-7826-443c-9717-bc28c3166092)
- [有向 FX システムの検証テスト](https://docs.microsoft.com/windows-hardware/test/hlk/testref/def16163-9118-4d4a-b559-37873befa12e)
