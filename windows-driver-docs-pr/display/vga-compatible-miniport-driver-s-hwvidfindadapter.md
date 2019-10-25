---
title: VGA 互換ミニポート ドライバーの HwVidFindAdapter
description: VGA 互換ミニポート ドライバーの HwVidFindAdapter
ms.assetid: 4538e95f-e84d-434c-a674-e1d1d4e9e5a0
keywords:
- ビデオミニポートドライバー WDK Windows 2000、VGA、HwVidFindAdapter
- VGA WDK ビデオミニポート、HwVidFindAdapter
- HwVidFindAdapter
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 91ea087d4bb9e30b68a5e0f7bf599a56ba7b94f1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829200"
---
# <a name="vga-compatible-miniport-drivers-hwvidfindadapter"></a>VGA 互換ミニポート ドライバーの HwVidFindAdapter


## <span id="ddk_vga_compatible_miniport_driver_s_hwvidfindadapter_gg"></span><span id="DDK_VGA_COMPATIBLE_MINIPORT_DRIVER_S_HWVIDFINDADAPTER_GG"></span>


VGA 互換のミニポートドライバーの[*HwVidFindAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_find_adapter)関数 (またはレジストリ*HwVidCallback*) は、[**ビデオ\_ポート\_CONFIG\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_video_port_config_info)バッファーに次の設定を行う必要があります。

-   **NumEmulatorAccessEntries**、 **EmulatorAccessEntries**配列内のエントリの数を示します。

-   **EmulatorAccessEntries**は、指定された数のエミュレーターを含む静的配列を指し、\_エントリ型の要素に[**アクセス\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/miniport/ns-miniport-_emulator_access_entry)ます。それぞれが、V86 EMULATOR からフックされた i/o ポートの範囲を記述し、既定では*に転送されます。Svガス Hwioportxxx*関数

    各エントリには、開始 i/o アドレス、範囲長、トラップされるアクセスのサイズ (UCHAR、USHORT、または ULONG)、ミニポートドライバーで i/o ポートを使用した文字列データの入力または出力がサポートされているかどうか、およびミニポートドライバーが提供する*Svガス Hwioportxxx が含まれます。* データを実際に検証し、転送する可能性がある関数。 各*Svガス Hwioportxxx*関数は、uchar 型、USHORT 型、または ULONG 型のデータの転送 (**IN**または**rep**) の転送、または書き込み (**OUT**または**rep outsb/outsb/outsb**) 転送を処理します。

-   **EmulatorAccessEntriesContext**は、ミニポートドライバーのデバイス拡張機能の領域などのストレージへのポインターであり、ミニポートドライバーの*Svガス Hwioportxxx*関数は、アプリケーションによって発行された、検査

-   **VdmPhysicalVideoMemoryAddress**と**VdmPhysicalVideoMemoryLength**。全画面の MS-DOS アプリケーションからの BIOS INT10 呼び出しをサポートするために、 *VDM*アドレス空間にマップする必要があるビデオメモリの範囲を記述します。

    ミニポートドライバーは[**VideoPortInt10**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportint10)関数を呼び出すことができます。このようなアプリケーションでは、ビデオモードが、ミニポートドライバーのアダプターがサポートできるものに変更されます。

-   ハードウェア\_状態要求\_保存\_、IOCTL\_ビデオに応答してアダプターのハードウェア状態を格納するために必要な最小バイト**数を示します。**

    ユーザーが全画面表示の MS-DOS アプリケーションをウィンドウで実行するように切り替えると、ミニポートドライバーは、ディスプレイドライバーがビデオアダプターの制御を取り戻す前に、アダプターの状態を保存する必要があります。 また、VGA と互換性のあるミニポートドライバーでは、ユーザーがウィンドウアプリケーションを全画面表示モードに切り替える可能性があるため、\_VIDEO\_RESTORE\_ハードウェア\_状態要求をサポートする必要があることに注意してください。

VGA 互換のミニポートドライバーのエミュレーターアクセスエントリは、アダプターのアクセス範囲配列のサブセットを指定します。 エミュレーターアクセスエントリはにすることができ、通常は、 [*HwVidFindAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_find_adapter)関数によって設定された、マップされたアクセス範囲配列内のすべての i/o ポートです。 アクセス範囲は、現在の IOPM を定義し、全画面の MS-DOS アプリケーションから直接アクセスできる i/o ポートを特定し、ミニポートドライバーのエミュレーターのサブセットを指定することによって、 [**VideoPortSetTrappedEmulatorPorts**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportsettrappedemulatorports)の呼び出しに渡されます。アクセスエントリ。

 

 





