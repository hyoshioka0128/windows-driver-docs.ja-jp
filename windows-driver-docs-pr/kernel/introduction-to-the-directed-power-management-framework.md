---
title: 指示電源管理フレームワークの概要
description: Power Framework、または PoFx、バージョン 3 には、電源管理フレームワークの指示または DFx、について説明します。
ms.assetid: 58550c57-3439-4212-b0c6-6a2fbfd38414
ms.date: 03/27/2019
ms.custom: 19H1
ms.openlocfilehash: 5bd11c3b5728e9e6515c687fa902e2236e37608b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341433"
---
# <a name="introduction-to-the-directed-power-management-framework"></a>指示電源管理フレームワークの概要

Windows 10、バージョンが 1903、実行時の電源管理フレームワークのバージョン 3 以降 ([PoFx](https://docs.microsoft.com/windows-hardware/drivers/kernel/overview-of-the-power-management-framework)) 省略可能な指示を提供します Directed PoFx (チェンジ DFx) 電源モデル。

DFx では、オペレーティング システムは、システムがアイドル状態に移行することにより、システムは、低電力をより確実に入力する場合に、適切な低電力アイドル状態を入力するデバイス スタックを指示します。

目的は、システムの電源効率をフォーム ファクターの Windows デバイスの電力消費量を削減することです。

DFx D 状態管理のみをサポートします。  DFx は、F 状態制約を使用して、デバイスのサブツリーをスキップします。

## <a name="requirements-for-wdf-non-miniport-drivers"></a>WDF (非ミニポート) ドライバーの要件

指定する WDF ドライバー **SystemManagedIdleTimeout**または**SystemManagedIdleTimeoutWithHint**で、 [WDF_DEVICE_POWER_POLICY_IDLE_SETTINGS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/ns-wdfdevice-_wdf_device_power_policy_idle_settings)構造体を無効にできます次のレジストリを追加することで DFx にキー INF の[AddReg ディレクティブ セクション](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)内、 [DDInstall.HW セクション](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-hw-section):

```
HKR,"WDF","WdfDirectedPowerTransitionEnable",0x00010001,1
```

要求元のシステムで管理されるアイドル タイムアウトには、ドライバーの代わりに PoFx を登録する WDF が発生するため、ドライバーがこのシナリオで PoFx を登録する必要はありません。

ドライバーが指定されている場合**DriverManagedIdleTimeout**、アイドル タイムアウトのシステムで管理されるへの切り替えを検討してください。  実現できない場合は、DFx を有効にする WDM 後述のガイドラインを使用します。

WDF ドライバーでは、実行時の電源管理を使用していない、サポートを追加し、システムで管理されるアイドル タイムアウトを使用します。  これを行うには、提供、 [WDF_DEVICE_POWER_POLICY_IDLE_SETTINGS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/ns-wdfdevice-_wdf_device_power_policy_idle_settings)への入力として構造体[ **WdfDeviceAssignS0IdleSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings)します。

## <a name="requirements-for-wdm-non-miniport-drivers"></a>(非ミニポート) WDM ドライバーの要件

ドライバーは WDF によって提供される、システムで管理されるアイドル サポートを使用していない場合 (、ドライバーはドライバー管理を使用して WDF ドライバー、アイドル状態または WDM ドライバー)、PoFx に自身を登録すると DFx サポートを受けるもします。  このシナリオでは、ドライバーは、実装することによって PoFx と登録します。

- [PO_FX_DIRECTED_POWER_DOWN_CALLBACK コールバック関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_directed_power_down_callback)
- [PO_FX_DIRECTED_POWER_UP_CALLBACK コールバック関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_directed_power_up_callback)


これらのコールバックへのポインターを提供する[PO_FX_DEVICE_V3](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-po_fx_device_v3)構造体への入力が、 [ **PoFxRegisterDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxregisterdevice)関数。

DFx サポートを受けるのみ、デバイスを提供できますのみ、 `PO_FX_DIRECTED_POWER*` PoFx を登録するときにコールバックします。  PoFx コールバックの残りの部分を実装する必要はありません。

## <a name="example"></a>例

次の例は、上記で説明した、自己登録オプションを示しています。

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

ドライバーが指定されている場合`PO_FX_VERSION_V1`以前は、注意`PO_FX_DEVICE_V3`構造体の使用`PO_FX_COMPONENT_V2`コンポーネントの配列構造にします。

## <a name="requirements-for-miniport-drivers"></a>ミニポート ドライバーの要件

ポート/ミニポート ドライバー モデルに従うデバイス クラス、システム指定のポートのドライバーは通常の電源ポリシーの所有権を処理します。  ほとんどのミニポートを DFx サポートを処理するためにポートに対応するドライバーが期待どおりに DFx を有効にするコードを変更を要求する必要はありません。

## <a name="testing"></a>Testing (テスト)

Microsoft 提供の DFx の使用できる 3 つのテスト: で単一デバイス テスト、 [Windows Driver Kit](https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk)ユーザー指定のデバイス、デバイス レベル HLK テスト、およびのすべてのデバイスをテスト用システム レベル HLK テストのテストのためのもので、システム。

単一デバイス テストはの一部、 [PwrTest](https://docs.microsoft.com/windows-hardware/drivers/devtest/pwrtest) WDK に付属するツール。  アクセスを使用して、ツールを実行、`/directedfx`スイッチします。  詳細については、次を参照してください。 [PwrTest DirectedFx シナリオ](../devtest/pwrtest-directedfx-scenario.md)します。

HLK テストについては、次のページを参照してください。

- [有向 FX 単一デバイス テスト](https://docs.microsoft.com/windows-hardware/test/hlk/testref/34cfdfa6-7826-443c-9717-bc28c3166092)
- [有向 FX システムの検証テスト](https://docs.microsoft.com/windows-hardware/test/hlk/testref/def16163-9118-4d4a-b559-37873befa12e)

## <a name="dfx-and-s-state-transitions"></a>DFx および S 状態遷移

- DFx 遷移のターゲット D 状態をランタイム D3 のと一致する必要があります (RTD3) S3 または S4 遷移のターゲット D 状態とは異なるれる可能性があります。  デバイスが、RTD3 用 D2 の入力が S3 または s4 D3 を入力のシナリオを検討してください。  この場合、DFx のターゲット D 状態は、D2 場合があります。
- 同様に、DFx の arm にスリープを解除の動作を場合は一致 S3 または S4 遷移で使用されている RTD3 と異なる場合があります。  たとえば、デバイスを使用して RTD3 の D2/ウェイク武装を入力して可能性がありますが S3 または s4 D3/いいえ-ウェイク-武装を入力します。  このシナリオでは、D2/ウェイク武装も DFx 遷移入力する必要があります。

## <a name="dfx-and-runtime-d3-rtd3"></a>DFx とランタイム D3 (RTD3)

- RTD3 でのデバイスでは、アイドル状態になったときに省電力 D 状態が通常入力します。  新しい作業が到着すると、デバイスはすぐに D0 を解除します。  DFx でデバイスがそのターゲット D 状態 (およびそのキューで新しい作業の保留) 内に存続する続行する必要があります PoFx にリダイレクト電源バックアップまでです。

## <a name="see-also"></a>関連項目

- [モダン スタンバイのためのハードウェアの準備](https://docs.microsoft.com/windows-hardware/design/device-experiences/prepare-hardware-for-modern-standby)
- [PwrTest](https://docs.microsoft.com/windows-hardware/drivers/devtest/pwrtest)
- [PO_FX_DEVICE_V3 構造体](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-po_fx_device_v3)
- [PO_FX_DIRECTED_POWER_DOWN_CALLBACK コールバック関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_directed_power_down_callback)
- [PO_FX_DIRECTED_POWER_UP_CALLBACK コールバック関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_directed_power_up_callback)
- [PoFxCompleteDirectedPowerDown](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxcompletedirectedpowerdown)関数
- [PwrTest DirectedFx シナリオ](../devtest/pwrtest-directedfx-scenario.md)
- [有向 FX 単一デバイス テスト](https://docs.microsoft.com/windows-hardware/test/hlk/testref/34cfdfa6-7826-443c-9717-bc28c3166092)
- [有向 FX システムの検証テスト](https://docs.microsoft.com/windows-hardware/test/hlk/testref/def16163-9118-4d4a-b559-37873befa12e)
