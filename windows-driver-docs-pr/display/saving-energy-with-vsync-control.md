---
title: VSync 制御による労力の低減
description: VSync 制御による労力の低減
ms.assetid: d7ee7461-0d2a-4103-9225-57ca10a75a7a
keywords:
- ドライバーモデルの表示 WDK Windows Vista, エネルギーの節約
- Windows Vista display driver model WDK、省電力
- ディスプレイドライバーモデル WDK Windows Vista、垂直コントロール
- Windows Vista display driver model WDK、垂直コントロール
ms.date: 10/14/2019
ms.localizationpriority: medium
ms.openlocfilehash: 262fb190a782b5b42606a00d47a02f7cb6951161
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829521"
---
# <a name="saving-energy-with-vsync-control"></a>VSync 制御による労力の低減

コンピューターの電源を節約するために、カーネルモードディスプレイドライバーを使用すると、垂直のモニター更新割り込みの発生回数を減らすことができます。

多くの場合、コンピューターシステムがアイドル状態のときに電力を節約するために、オペレーティングシステムで動作する新しいプロセッサとプラットフォームが使用されます。 ただし、割り込みの発生などの定期的なシステムアクティビティによって、ピーク時の電力使用率が発生し、コンピューターシステムが電力を節約する一時的なスリープ状態にならない可能性があります。

Windows Vista Service Pack 1 (SP1) および Windows Server 2008 以降では、オペレーティングシステムは、画面が新しいグラフィックスやマウスの操作から更新されていない場合に、定期的な垂直の割り込みカウントをオフにすることができます。 同期されていない割り込み間隔を制御することにより、ドライバーは大量のエネルギーを節約できます。

Windows Server 2008 以降のバージョンの Windows Driver Kit (WDK) を使用して Windows Display Driver Model (WDDM) ドライバーを再構築することで、この機能を利用できます。

## <a name="windowsvista-with-sp1-driver-changes-for-vsync-control"></a>Windows Vista with SP1 ドライバーの変更 (垂直コントロール)

ドライバーがこの機能を利用するには、Windows Vista SP1 で導入された[DXGK_VIDSCHCAPS](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidschcaps)構造の**Vsyncpowersaveaware**メンバーをサポートする必要があります。 WDDM に従う既存のドライバーは、Windows Server 2008 以降のバージョンの WDK を使用して、 **Vsyncpowersaveaware**メンバーで再コンパイルする必要があります。

この機能をサポートするドライバーがインストールされている Windows Vista SP1 以降のシステムでは、1/垂直 (垂直同期) がモニターのリフレッシュレートである10の連続した期間に GPU アクティビティが発生しない場合、垂直割り込みのカウント機能が無効になります。 垂直速度が60ヘルツ (Hz) の場合、垂直の割り込みは16ミリ秒ごとに1回発生します。 したがって、画面の更新が存在しない場合、垂直同期割り込みは160ミリ秒後にオフになります。 GPU アクティビティが再開されると、垂直の割り込みが再び有効になり、画面が更新されます。

## <a name="display-only-vsync-requirements-for-windows-8-and-later-versions"></a>Windows 8 以降のバージョンでは、表示専用の垂直同期の要件

Windows 8 以降のバージョンの Windows オペレーティングシステムでは、次のように、同期機能をサポートするための[カーネルモード表示専用ドライバー (KMDOD)](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)では省略可能です。

- **表示専用ドライバーは、垂直同期コントロールをサポートします**

  KMDOD が垂直同期コントロール機能をサポートしている場合は、 [*DxgkDdiControlInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_controlinterrupt)と[*DxgkDdiGetScanLine*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_getscanline)の両方の関数を実装する必要があります。また、 [KMDDOD_INITIALIZATION_DATA](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_kmddod_initialization_data)構造体の両方の関数への有効な関数ポインターを提供する必要があります。

  この場合、KMDOD は、垂直方向の割り込みをオペレーティングシステムに報告するために、 [*DxgkDdiInterruptRoutine*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_interrupt_routine)関数と[*DxgkDdiDpcRoutine*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_dpc_routine)関数も実装する必要があります。

  さらに、 [DISPLAYCONFIG_VIDEO_SIGNAL_INFO](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-displayconfig_video_signal_info)構造体の**ピクセル**単位の比率、 **hSyncFreq**、および**vSyncFreq**メンバーの値を**D3DKMDT_FREQUENCY_NOTSPECIFIED**することはできません。

- **表示専用ドライバーは、垂直同期コントロールをサポートしていません**

  KMDOD が垂直同期コントロール機能をサポートしていない場合は、 [*DxgkDdiControlInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_controlinterrupt)または[*DxgkDdiGetScanLine*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_getscanline)関数を実装することはできず、 [KMDDOD_INITIALIZATION_DATA](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_kmddod_initialization_data)構造体のいずれかの関数への有効な関数ポインターを提供することはできません。

  この場合、Microsoft DirectX graphics カーネルサブシステムは、現在のモードおよび最後にシミュレートされた垂直同期の時間に基づいて、垂直の割り込みの値をシミュレートし、行をスキャンします。

  さらに、 [DISPLAYCONFIG_VIDEO_SIGNAL_INFO](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-displayconfig_video_signal_info)構造体の**ピクセル**単位の比率、 **hSyncFreq**、および**vSyncFreq**メンバーの値を**D3DKMDT_FREQUENCY_NOTSPECIFIED**に設定する必要があります。

これらの条件が満たされていない場合、DirectX グラフィックスのカーネルサブシステムは KMDOD を読み込みません。

## <a name="registry-control"></a>レジストリコントロール

Windows Vista SP1 以降のバージョンの Windows オペレーティングシステムでは、既定の垂直同期アイドルタイムアウトは10個の垂直同期期間です。 必要に応じて、テスト目的で、レジストリ設定を使用してタイムアウトを制御できます。

> [!IMPORTANT]
> アプリケーションの互換性の問題を回避するには、実稼働ドライバーで既定のレジストリ設定を変更しないでください。

キーのパス:  
**RTL_REGISTRY_CONTROL \GraphicsDrivers\Scheduler**

完全なパス:  
**[HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\GraphicsDrivers\Scheduler]**

キーの値:  
**VsyncIdleTimeout**

ValueType  
**REG_DWORD**

値:  
10 = 既定値

値:  
0 = 垂直同期コントロールを無効にします (Windows Vista と同じ動作を生成します)
