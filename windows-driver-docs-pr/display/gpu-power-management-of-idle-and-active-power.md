---
title: アイドル状態および現在使用されている電源の GPU 電源管理
description: GPU の電源管理インフラストラクチャにより Windows Display Driver Model (WDDM) 1.2、およびそれ以降のドライバーは、個々 のデバイスまたは一連のデバイスの電源を管理します。
ms.assetid: F8096F7E-39EA-45CB-8A1C-60A7A298AFEC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 944d08c13f17ec0853897f855e1d8cc4d9a50bc3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365027"
---
# <a name="gpu-power-management-of-idle-states-and-active-power"></a>アイドル状態および現在使用されている電源の GPU 電源管理


Windows 8 以降では、省略可能な GPU の電源管理インフラストラクチャが使用可能な Windows Display Driver Model (WDDM) 1.2 を使用して、以降のドライバーが個々 のデバイスまたは一連のデバイスの電源を管理します。 このインフラストラクチャは、Windows とのコラボレーションに F 状態と P 状態の電源管理をサポートするために標準化されたメカニズムを提供します。

|                                                                                   |                                        |
|-----------------------------------------------------------------------------------|----------------------------------------|
| WDDM の最小バージョン                                                              | 1.2                                    |
| Windows の最小バージョン                                                           | 8                                      |
| ドライバーの実装                                                             | 省略可能                               |
| [WHCK](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)要件とテスト | **Device.Graphics.RuntimePowerMgmt** |

 

## <a name="span-idgpupowermanagementdevicedriverinterfaceddispanspan-idgpupowermanagementdevicedriverinterfaceddispanspan-idgpupowermanagementdevicedriverinterfaceddispangpu-power-management-device-driver-interface-ddi"></a><span id="GPU_power_management_device_driver_interface__DDI_"></span><span id="gpu_power_management_device_driver_interface__ddi_"></span><span id="GPU_POWER_MANAGEMENT_DEVICE_DRIVER_INTERFACE__DDI_"></span>GPU の電源管理デバイス ドライバー インターフェイス (DDI)


これらの新規および更新された関数と構造体は Windows 8 以降で、ディスプレイのミニポート ドライバーの電源コンポーネントの状態を遷移して、Microsoft DirectX グラフィックスのカーネル サブシステム、電源イベントを通信するために使用できます。

-   [*DxgkCbCompleteFStateTransition*](https://msdn.microsoft.com/library/windows/hardware/jj128349)
-   [*DxgkCbPowerRuntimeControlRequest*](https://msdn.microsoft.com/library/windows/hardware/hh451323)
-   [*DxgkCbSetPowerComponentActive*](https://msdn.microsoft.com/library/windows/hardware/hh451331)
-   [*DxgkCbSetPowerComponentIdle*](https://msdn.microsoft.com/library/windows/hardware/hh451336)
-   [*DxgkCbSetPowerComponentLatency*](https://msdn.microsoft.com/library/windows/hardware/hh698278)
-   [*DxgkCbSetPowerComponentResidency*](https://msdn.microsoft.com/library/windows/hardware/hh698279)
-   [*DxgkDdiPowerRuntimeControlRequest*](https://msdn.microsoft.com/library/windows/hardware/hh451396)
-   [*DxgkDdiSetPowerComponentFState*](https://msdn.microsoft.com/library/windows/hardware/hh451422)
-   [**DXGK\_DRIVERCAPS**](https://msdn.microsoft.com/library/windows/hardware/ff561062)
-   [**DXGK\_POWER\_コンポーネント\_フラグ**](https://msdn.microsoft.com/library/windows/hardware/hh464063)
-   [**DXGK\_POWER\_コンポーネント\_マッピング**](https://msdn.microsoft.com/library/windows/hardware/hh464067)
-   [**DXGK\_POWER\_コンポーネント\_型**](https://msdn.microsoft.com/library/windows/hardware/hh464070)
-   [**DXGK\_POWER\_RUNTIME\_COMPONENT**](https://msdn.microsoft.com/library/windows/hardware/hh464073)
-   [**DXGK\_QUERYADAPTERINFOTYPE**](https://msdn.microsoft.com/library/windows/hardware/ff562010)
-   [**DXGKARG\_QUERYADAPTERINFO**](https://msdn.microsoft.com/library/windows/hardware/ff557621)
-   [**DXGK\_QUERYSEGMENTOUT3**](https://msdn.microsoft.com/library/windows/hardware/hh464082)

## <a name="span-idgpupowermanagementscenariosspanspan-idgpupowermanagementscenariosspanspan-idgpupowermanagementscenariosspangpu-power-management-scenarios"></a><span id="GPU_power_management_scenarios"></span><span id="gpu_power_management_scenarios"></span><span id="GPU_POWER_MANAGEMENT_SCENARIOS"></span>GPU の電源管理のシナリオ


Gpu とディスプレイの画面は、ラップトップ、モバイル デバイス、およびデスクトップ Pc で最も電源消費の 2 つです。

電力消費量を削減し、バッテリを長持ちさせるキーの電源管理のシナリオを次に示します。

-   モバイル フォーム ファクターのデバイスがアイドル状態に移動し、シャット ダウンは個々 のシステム コンポーネントで使用されていない場合は、電力を節約できます。
-   チップ (SoC) 上の Windows システム-コンシューマー デバイスなどに基づいてデバイスの動作し、モバイルの電話は、すぐに必要なとき、それによってエネルギーの保存を有効にします。

## <a name="span-idhardwarecertificationrequirementsspanspan-idhardwarecertificationrequirementsspanspan-idhardwarecertificationrequirementsspanhardware-certification-requirements"></a><span id="Hardware_certification_requirements"></span><span id="hardware_certification_requirements"></span><span id="HARDWARE_CERTIFICATION_REQUIREMENTS"></span>ハードウェア認定要件


この機能を実装するときにハードウェア デバイスが満たす必要のある要件については、関連するを参照してください[WHCK ドキュメント](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)で**Device.Graphics.RuntimePowerMgmt**します。

参照してください[WDDM 1.2 機能](wddm-v1-2-features.md)に Windows 8 で追加された機能の説明。

 

 





