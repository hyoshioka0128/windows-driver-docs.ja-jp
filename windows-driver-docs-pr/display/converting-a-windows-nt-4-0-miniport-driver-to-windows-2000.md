---
title: Windows NT 4.0 ミニポート ドライバーから Windows 2000 への変換
description: Windows NT 4.0 ミニポート ドライバーから Windows 2000 への変換
ms.assetid: a55192c6-3de4-4433-8825-3393f2bce04a
keywords:
- ビデオミニポートドライバー WDK Windows 2000、複数の Windows バージョン、Windows NT 4.0 ドライバーの変換
- ビデオミニポートドライバーの変換 WDK Windows 2000
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 98899f89dc10d711d4030cf341a56b5f887cbdda
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839041"
---
# <a name="converting-a-windows-nt-40-miniport-driver-to-windows-2000"></a>Windows NT 4.0 ミニポート ドライバーから Windows 2000 への変換


## <span id="ddk_converting_a_windows_nt_4_0_miniport_driver_to_windows_2000_gg"></span><span id="DDK_CONVERTING_A_WINDOWS_NT_4_0_MINIPORT_DRIVER_TO_WINDOWS_2000_GG"></span>


優れた Windows NT 4.0 および以前のミニポートドライバーは、Windows 2000 以降のミニポートドライバーに簡単になることができます。 Windows 2000 以降のミニポートドライバーで必要なプラグアンドプレイサポートを提供するために必要な更新プログラムの一部を次に示します。

-   実装する必要がある新しい関数の一覧については、「[ビデオミニポートドライバー (Windows 2000 モデル) のプラグアンドプレイと電源管理](plug-and-play-and-power-management-in-video-miniport-drivers--windows-.md)」を参照してください。 これらの新しい関数を指すように、 [**VIDEO\_HW\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_video_hw_initialization_data)の新しいメンバーを必ず初期化してください。

-   [**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/display/driverentry-of-video-miniport-driver)関数で[**videoportinitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportinitialize)の呼び出しを更新します。 4番目のパラメーター (*HwContext*) は、Windows 2000 以降では**NULL**にする必要があります。

-   [*HwVidFindAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_find_adapter)関数を更新します。 列挙可能なバス上のデバイスの場合、 *HwVidFindAdapter*は次のように変更する必要があります。

    -   ほとんどのデバイス検出コードを削除します。 これは、Windows 2000 で[*HwVidFindAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_find_adapter)を呼び出すと、PnP マネージャーがデバイスを既に検出したことを意味します。
    -   [**Videoportgetaccessranges**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportgetaccessranges)を呼び出して、デバイスが応答するバス相対物理アドレスを取得します。 これらのアドレスは、PnP マネージャーによって割り当てられます。
    -   ドライバーが複数のデバイスの種類をサポートしている場合は、デバイスの種類を決定します。
    -   [*もう一度*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_find_adapter)パラメーターを無視します。 これは、システムがデバイスごとに1回だけ*HwVidFindAdapter*を呼び出すためです。

    ISA など、列挙されていないバス上のデバイスの場合、PnP はデバイスの起動を試行しますが、デバイスが実際に存在するかどうかを判断するのは[*HwVidFindAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_find_adapter)の役割です。

-   を更新**します。** デバイスとベンダー ID を含むドライバーの INF ファイルの製造セクション。 これは、PnP マネージャーがデバイスをその INF ファイルに関連付けることができるようにするために必要です。 Windows NT 4.0 および更新された Windows 2000 以降のサンプル **。製造**セクションは次のとおりです。

    ```cpp
    [ABC.Mfg]   ; Windows NT V4.0 INF
    %ABC% ABC Graphics Accelerator A = abc
    %ABC% ABC Graphics Accelerator B = abc

    [ABC.Mfg]   ; Windows 2000 and later INF
    %ABC% ABC Graphics Accelerator A = abc, PCI\VEN_ABCD&DEV_0123
    %ABC% ABC Graphics Accelerator B = abc, PCI\VEN_ABCD&DEV_4567
    ```

ドライバー開発キット (DDK) に含まれている*geninf .exe*ツールを使用して、INF を生成できます。 (DDK は Windows Driver Kit \[WDK\]の前にあります)。ただし、 *geninf*は Windows NT 4.0 用の inf を作成しないことに注意してください。 Windows NT 4.0 をサポートする場合は、 *geninf .exe*によって生成される INF ファイルを変更する必要があります。 詳細については、「[グラフィックス INF ファイルの作成](creating-graphics-inf-files.md)」を参照してください。

Windows 2000 以降のビデオポートでは、従来のドライバーとして Windows NT 4.0 ミニポートドライバーがサポートされています。 システムの実行中に、レガシミニポートドライバーのグラフィックスアダプターをシステムから削除することはできません。また、実行中のシステムに追加したときに、レガシミニポートドライバーが自動的に検出されることもありません。

 

 





