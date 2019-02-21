---
title: レジストリで DXGI 情報の設定
description: レジストリで DXGI 情報の設定
ms.assetid: 2d116c89-02dd-4104-be75-70a00fa5e06a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 87ec69f3879b23862fba4dc2d3c4edcbdb93a0f6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532862"
---
# <a name="setting-dxgi-information-in-the-registry"></a>レジストリで DXGI 情報の設定


DXGI とリファレンス ラスタライザーは、次のレジストリ キーを使用します。

<span id="DWORD_Software_Microsoft_DXGI_DisableFullscreenWatchdog"></span><span id="dword_software_microsoft_dxgi_disablefullscreenwatchdog"></span><span id="DWORD_SOFTWARE_MICROSOFT_DXGI_DISABLEFULLSCREENWATCHDOG"></span>DWORD ソフトウェア\\Microsoft\\DXGI\\DisableFullscreenWatchdog  
1 に設定すると、ウォッチドッグ スレッドを無効にします。

<span id="DWORD_Software_Microsoft_Direct3D_ReferenceDevice_FlushOften"></span><span id="dword_software_microsoft_direct3d_referencedevice_flushoften"></span><span id="DWORD_SOFTWARE_MICROSOFT_DIRECT3D_REFERENCEDEVICE_FLUSHOFTEN"></span>DWORD ソフトウェア\\Microsoft\\Direct3D\\ReferenceDevice\\FlushOften  
多くの場合、フラッシュを 1 に設定します。

<span id="DWORD_Software_Microsoft_Direct3D_ReferenceDevice_FenceEachEntryPoint"></span><span id="dword_software_microsoft_direct3d_referencedevice_fenceeachentrypoint"></span><span id="DWORD_SOFTWARE_MICROSOFT_DIRECT3D_REFERENCEDEVICE_FENCEEACHENTRYPOINT"></span>DWORD ソフトウェア\\Microsoft\\Direct3D\\ReferenceDevice\\FenceEachEntryPoint  
Gpu DDI 関数フェンスを呼び出すたびに 1 に設定します。 Gpu を搭載したフェンス操作は、コマンドのバッチをフラッシュし、GPU がアイドル状態になるまでブロックすることです。

<span id="DWORD_Software_Microsoft_Direct3D_ReferenceDevice_Debug"></span><span id="dword_software_microsoft_direct3d_referencedevice_debug"></span><span id="DWORD_SOFTWARE_MICROSOFT_DIRECT3D_REFERENCEDEVICE_DEBUG"></span>DWORD ソフトウェア\\Microsoft\\Direct3D\\ReferenceDevice\\デバッグ  
1 に設定します。

-   多くの場合、フラッシュし、呼び出しごとに、gpu を搭載した DDI 関数フェンスを作成します。

-   リファレンス ラスタライザー (RefRast) 単一のスレッドを実行します。

<span id="DWORD_Software_Microsoft_Direct3D_ReferenceDevice_D3D10RefGdiDisplayMask"></span><span id="dword_software_microsoft_direct3d_referencedevice_d3d10refgdidisplaymask"></span><span id="DWORD_SOFTWARE_MICROSOFT_DIRECT3D_REFERENCEDEVICE_D3D10REFGDIDISPLAYMASK"></span>DWORD ソフトウェア\\Microsoft\\Direct3D\\ReferenceDevice\\D3D10RefGdiDisplayMask  
DWORD マスク内の各ビットが有効 (場合 1 に設定) または無効にします (場合は 0 に設定) モニターは、参照デバイスによって制御されます。

<span id="DWORD_Software_Microsoft_Direct3D_ReferenceDevice_SingleThreaded"></span><span id="dword_software_microsoft_direct3d_referencedevice_singlethreaded"></span><span id="DWORD_SOFTWARE_MICROSOFT_DIRECT3D_REFERENCEDEVICE_SINGLETHREADED"></span>DWORD ソフトウェア\\Microsoft\\Direct3D\\ReferenceDevice\\シングル ・ スレッド  
1 に設定し、実行中の RefRast シングル スレッドを有効にします。

<span id="DWORD_Software_Microsoft_Direct3D_ReferenceDevice_ForceHeapAlloc"></span><span id="dword_software_microsoft_direct3d_referencedevice_forceheapalloc"></span><span id="DWORD_SOFTWARE_MICROSOFT_DIRECT3D_REFERENCEDEVICE_FORCEHEAPALLOC"></span>DWORD ソフトウェア\\Microsoft\\Direct3D\\ReferenceDevice\\ForceHeapAlloc  
1 に設定し、参照デバイスが他の割り当てのメカニズムではなく、通常のプロセス ヒープを使用してリソースを作成します。

<span id="DWORD_Software_Microsoft_Direct3D_ReferenceDevice_AllowAsync"></span><span id="dword_software_microsoft_direct3d_referencedevice_allowasync"></span><span id="DWORD_SOFTWARE_MICROSOFT_DIRECT3D_REFERENCEDEVICE_ALLOWASYNC"></span>DWORD ソフトウェア\\Microsoft\\Direct3D\\ReferenceDevice\\AllowAsync  
1 に設定すると、参照デバイスの 2 番目のスレッドを非同期的に実行を許可する (未解決になる複数のコマンド バッファーが許可される)。

参照のハードウェアは通常 2 つ目のスレッドで実行されます。ただし、この 2 つ目のスレッドは、プライマリ スレッドが続行前に、すべての作業を完了します。

<span id="DWORD_Software_Microsoft_Direct3D_ReferenceDevice_SimulateInfinitelyFastHW"></span><span id="dword_software_microsoft_direct3d_referencedevice_simulateinfinitelyfasthw"></span><span id="DWORD_SOFTWARE_MICROSOFT_DIRECT3D_REFERENCEDEVICE_SIMULATEINFINITELYFASTHW"></span>DWORD ソフトウェア\\Microsoft\\Direct3D\\ReferenceDevice\\SimulateInfinitelyFastHW  
のみを参照して、デバイスが非常に速く (基本的に何も行われない) の外観を与えるいくつかの限られたコマンドの処理、参照、デバイスのシミュレートされたハードウェアを 1 に設定します。

ドライバーは、パフォーマンス ツールとしてこのキーを使用することができます。

 

 





