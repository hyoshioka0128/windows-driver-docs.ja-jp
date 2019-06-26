---
title: VSync 制御による労力の低減
description: VSync 制御による労力の低減
ms.assetid: d7ee7461-0d2a-4103-9225-57ca10a75a7a
keywords:
- ディスプレイ ドライバー モデル WDK Windows Vista、エネルギーを節約します。
- Windows Vista のディスプレイ ドライバー モデル WDK、エネルギーを節約します。
- ドライバー モデル WDK Windows Vista では、コントロールの垂直同期の表示します。
- Windows Vista ディスプレイ ドライバー モデル、WDK VSync コントロール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f713b413cd37f7b9d716d9b392b81ffe62268da
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365584"
---
# <a name="saving-energy-with-vsync-control"></a>VSync 制御による労力の低減


コンピューターで電力を節約するには、カーネル モードのディスプレイ ドライバーが発生した VSync モニターの更新の割り込みの数を減らすことができます。

新しいプロセッサとプラットフォームは、多くの場合、コンピューター システムがアイドル状態のときに、エネルギーを節約するために、オペレーティング システムで作業します。 ただし、割り込みの発生など、定期的なシステムの使用状況はピーク時の電力使用状況の原因し、コンピューター システムが電力を節約は一時的なスリープ状態を入力するを防ぐことができます。

オペレーティング システムは Windows Vista Service Pack 1 (SP1)、Windows Server 2008 以降では、定期的な VSync 割り込みがカウントに画面を新しいグラフィックスやマウスのアクティビティから更新されていないときに無効にできます。 垂直同期の割り込みの間隔を制御することで、ドライバーは、大幅なエネルギーを節約できます。

この機能を行うには、Windows Server 2008 またはそれ以降のバージョンの Windows Driver Kit (WDK) を使用して Windows Display Driver Model (WDDM) ドライバーを再構築します。

### <a name="span-iddriverchangesforvsynccontrolspanspan-iddriverchangesforvsynccontrolspanwindowsvista-with-sp1-driver-changes-for-vsync-control"></a><span id="driver_changes_for_vsync_control"></span><span id="DRIVER_CHANGES_FOR_VSYNC_CONTROL"></span>Windows Vista SP1 のドライバーを使用したのコントロールの垂直同期の変更します。

ドライバーはこの機能を活用するために、それらをサポートする必要があります、 **VSyncPowerSaveAware**内のメンバー、 [ **DXGK\_VIDSCHCAPS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_vidschcaps)が構造Windows Vista SP1 で導入されました。 WDDM に従って既存のドライバーを再コンパイルする必要があります、 **VSyncPowerSaveAware**メンバーは、Windows Server 2008 またはそれ以降のバージョンの WDK を使用します。

Windows Vista sp1 または以降のシステム、ドライバー、WDDM が続くし、この機能をサポートするには、GPU アクティビティが発生しない場合の 1/Vsync の 10 個の継続的な期間モニターのリフレッシュ レートの垂直同期が垂直同期の割り込みのカウントの機能は、オフになります。 垂直同期レートが 60 ヘルツ (Hz) の場合は、垂直同期の割り込みは 16 ミリ秒ごとに 1 回を発生します。 したがって、画面の更新プログラムがない場合、垂直同期割り込み無効になって 160 ミリ秒後にします。 GPU アクティビティが再開されると、垂直同期の割り込みが有効にもう一度画面を更新します。

### <a name="span-idwindows8display-onlyvsyncrequirementsspanspan-idwindows8display-onlyvsyncrequirementsspanspan-idwindows8display-onlyvsyncrequirementsspanwindows8-display-only-vsync-requirements"></a><span id="Windows_8_Display-Only_VSync_Requirements"></span><span id="windows_8_display-only_vsync_requirements"></span><span id="WINDOWS_8_DISPLAY-ONLY_VSYNC_REQUIREMENTS"></span>Windows 8 の表示専用の垂直同期の要件

Windows 8 以降は省略可能、[カーネル モード表示専用ドライバー (KMDOD)](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)次のように、垂直同期機能をサポートするために。

<span id="Display-only_driver_supports_VSync_control"></span><span id="display-only_driver_supports_vsync_control"></span><span id="DISPLAY-ONLY_DRIVER_SUPPORTS_VSYNC_CONTROL"></span>表示専用ドライバーは、コントロールの垂直同期をサポートしています。  
両方に実装する必要があります、KMDOD 垂直同期の制御機能をサポートする場合[ *DxgkDdiControlInterrupt* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_controlinterrupt)と[ *DxgkDdiGetScanLine* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_getscanline)関数し、でこれらの関数の両方に有効な関数ポインターを提供する必要があります、 [ **KMDDOD\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/ns-dispmprt-_kmddod_initialization_data)構造体。

この場合、KMDOD を実装する必要がありますも、 [ *DxgkDdiInterruptRoutine* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_interrupt_routine)と[ *DxgkDdiDpcRoutine* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_dpc_routine)関数にはオペレーティング システムには、垂直同期の割り込みを報告します。

さらの値、 **PixelRate**、 **hSyncFreq**、および**vSyncFreq**のメンバー、 [ **DISPLAYCONFIG\_ビデオ\_信号\_情報**](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-displayconfig_video_signal_info)構造にすることはできません**D3DKMDT\_頻度\_NOTSPECIFIED**します。

<span id="Display-only_driver_does_not_support_VSync_control"></span><span id="display-only_driver_does_not_support_vsync_control"></span><span id="DISPLAY-ONLY_DRIVER_DOES_NOT_SUPPORT_VSYNC_CONTROL"></span>表示専用ドライバーがコントロールの垂直同期をサポートしていません  
場合は、KMDOD 垂直同期の制御機能をサポートしていない必要がありますを実装していないか[ *DxgkDdiControlInterrupt* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_controlinterrupt)または[ *DxgkDdiGetScanLine* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_getscanline)関数し、でこれらの関数のいずれかに有効な関数ポインターを指定しないで、 [ **KMDDOD\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/ns-dispmprt-_kmddod_initialization_data)構造体。

ここで、Microsoft DirectX グラフィックスのカーネル サブシステムは、垂直同期の割り込みと現在のモードとシミュレートされた最後の垂直同期の時刻に基づくスキャン ラインの値をシミュレートします。

さらの値、 **PixelRate**、 **hSyncFreq**、および**vSyncFreq**のメンバー、 [ **DISPLAYCONFIG\_ビデオ\_信号\_情報**](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-displayconfig_video_signal_info)に構造体を設定する必要があります**D3DKMDT\_頻度\_NOTSPECIFIED**します。

これらの条件が満たされない場合でも、DirectX グラフィックスのカーネル サブシステムでは、KMDOD は読み込まれません。

### <a name="span-idregistrycontrolspanspan-idregistrycontrolspan-registry-control"></a><span id="registry_control"></span><span id="REGISTRY_CONTROL"></span> レジストリの制御

Windows Vista SP1 と以降のバージョンの Windows オペレーティング システムでは、既定の垂直同期のアイドル タイムアウトは 10 個の垂直同期の期間です。 必要に応じて、テスト目的は、タイムアウト値をレジストリ設定を使用して制御できます。

**重要な**  アプリケーション互換性の問題を回避するためには変わりません運用ドライバーの既定のレジストリ設定します。

 

<span id="Key_Path_"></span><span id="key_path_"></span><span id="KEY_PATH_"></span>キーのパス:  
**RTL\_レジストリ\_コントロール\\GraphicsDrivers\\スケジューラ**

完全なパス:  
**[HKEY_LOCAL_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\GraphicsDrivers\\Scheduler]**

<span id="Key_Value_"></span><span id="key_value_"></span><span id="KEY_VALUE_"></span>キーの値:  
**VsyncIdleTimeout**

<span id="ValueType_"></span><span id="valuetype_"></span><span id="VALUETYPE_"></span>ValueType:  
**REG\_DWORD**

<span id="Value_"></span><span id="value_"></span><span id="VALUE_"></span>値:  
10 = 既定値

<span id="Value_"></span><span id="value_"></span><span id="VALUE_"></span>値:  
0 = コントロールの垂直同期を無効にする (同じ動作を生成します Windows Vista と同じ)。



 

 





