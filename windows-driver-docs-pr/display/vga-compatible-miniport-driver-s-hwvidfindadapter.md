---
title: VGA 互換ミニポート ドライバーの HwVidFindAdapter
description: VGA 互換ミニポート ドライバーの HwVidFindAdapter
ms.assetid: 4538e95f-e84d-434c-a674-e1d1d4e9e5a0
keywords:
- ビデオのミニポート ドライバー WDK Windows 2000 では、VGA、HwVidFindAdapter
- WDK の VGA ビデオのミニポート HwVidFindAdapter
- HwVidFindAdapter
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e335dba6a14096500e6502bf5c4f26d29f88e799
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387419"
---
# <a name="vga-compatible-miniport-drivers-hwvidfindadapter"></a>VGA 互換ミニポート ドライバーの HwVidFindAdapter


## <span id="ddk_vga_compatible_miniport_driver_s_hwvidfindadapter_gg"></span><span id="DDK_VGA_COMPATIBLE_MINIPORT_DRIVER_S_HWVIDFINDADAPTER_GG"></span>


VGA と互換性のあるミニポート ドライバーの[ *HwVidFindAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff567332)関数 (またはレジストリ*HwVid..コールバック*) で、次のように設定する必要があります、 [**ビデオ\_ポート\_CONFIG\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff570531)バッファー。

-   **NumEmulatorAccessEntries**、内のエントリの数を示す、 **EmulatorAccessEntries**配列

-   **EmulatorAccessEntries**の指定した数値を格納する静的配列をポイントして、 [**エミュレーター\_アクセス\_エントリ**](https://msdn.microsoft.com/library/windows/hardware/ff564131)-を記述する要素を入力します。範囲の I/O ポート フック V86 エミュレーターからと、既定では、転送、 *SvgaHwIoPortXxx*関数

    各エントリには、次のように開始 I/O アドレス範囲の長さをミニポート ドライバーには、I/O ポートを使用して文字列データの入力または出力がサポートしているし、ミニポート ドライバーによって提供されるかどうか (UCHAR、USHORT、または ULONG) をするのにはアクセスのサイズがトラップ*SvgaHwIoPortXxx*関数を実際に検証し、場合によっては、データを転送します。 各*SvgaHwIoPortXxx*読み取りハンドルの機能 (**IN**または**INSD/REP INSB/INSW**) または書き込みを行う (**アウト**または**REP OUTSB/OUTSW/OUTSD**) UCHAR、USHORT、または ULONG サイズのデータの転送。

-   **EmulatorAccessEntriesContext**、ミニポート ドライバーのデバイス拡張機能を内の領域などのストレージへのポインター、ミニポート ドライバーの*SvgaHwIoPortXxx*関数を一連のアプリケーションが発行したバッチ処理できます検証が必要な手順

-   **VdmPhysicalVideoMemoryAddress**と**VdmPhysicalVideoMemoryLength**、さまざまなビデオ メモリにマップする必要がありますを記述する、 *VDM*アドレス空間から BIOS INT10 呼び出しをサポートするには全画面表示 MS-DOS アプリケーション

    ミニポート ドライバーを呼び出すことができます、 [ **VideoPortInt10** ](https://msdn.microsoft.com/library/windows/hardware/ff570321)このようなアプリケーションをサポートできるアダプターのミニポート ドライバーのビデオ モードが変更されたときに機能します。

-   **HardwareStateSize**、IOCTL への応答に、アダプターのハードウェアの状態を格納するために必要なバイトの最小数を記述する\_ビデオ\_保存\_ハードウェア\_状態要求

    ユーザー、全画面表示の MS-DOS アプリケーション ウィンドウで実行すると、ミニポート ドライバーは、ビデオ アダプターのディスプレイ ドライバー獲得コントロールの前に、アダプターの状態を保存する必要があります。 VGA と互換性のあるミニポート ドライバーもする必要がありますサポート相互 IOCTL\_ビデオ\_復元\_ハードウェア\_ユーザーは、全画面表示に選択したアプリケーションを切り替える場合があるために、状態を要求モード。

VGA と互換性のあるミニポート ドライバーのエミュレーターへのアクセス エントリでは、アダプターのアクセスの範囲の配列のサブセットを指定します。 エミュレーターのアクセス エントリを指定でき、通常は、割り当てられたアクセスの範囲の配列内のすべての I/O ポートによって設定されます、 [ *HwVidFindAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff567332)関数。 アクセス権の範囲への呼び出しで渡します[ **VideoPortSetTrappedEmulatorPorts**](https://msdn.microsoft.com/library/windows/hardware/ff570366)現在 IOPM を定義、および全画面表示の MS-DOS アプリケーションで直接アクセスできる I/O ポートを確認します。ミニポート ドライバーのエミュレーターへのアクセス エントリのサブセットを指定します。

 

 





