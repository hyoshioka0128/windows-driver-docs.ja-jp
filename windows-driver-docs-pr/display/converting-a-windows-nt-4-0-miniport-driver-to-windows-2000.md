---
title: Windows NT 4.0 ミニポート ドライバーから Windows 2000 への変換
description: Windows NT 4.0 ミニポート ドライバーから Windows 2000 への変換
ms.assetid: a55192c6-3de4-4433-8825-3393f2bce04a
keywords:
- ビデオのミニポート ドライバー WDK Windows 2000、Windows NT 4.0 のドライバーを変換する、複数の Windows バージョン
- ビデオのミニポート ドライバー WDK Windows 2000 に変換します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76a5f6f5630961afe00a0c31195eb865cfb3abcb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384509"
---
# <a name="converting-a-windows-nt-40-miniport-driver-to-windows-2000"></a>Windows NT 4.0 ミニポート ドライバーから Windows 2000 への変換


## <span id="ddk_converting_a_windows_nt_4_0_miniport_driver_to_windows_2000_gg"></span><span id="DDK_CONVERTING_A_WINDOWS_NT_4_0_MINIPORT_DRIVER_TO_WINDOWS_2000_GG"></span>


適切な Windows NT 4.0 と以前のミニポート ドライバーは Windows 2000 と以降のバージョンのミニポート ドライバーに簡単になります。 Windows 2000 およびそれ以降のミニポート ドライバーで必要なプラグ アンド プレイのサポートを提供するために必要な更新プログラムの一部を次に示します。

-   参照してください[プラグ アンド プレイとビデオのミニポート ドライバー (Windows 2000 モデル) での電源管理](plug-and-play-and-power-management-in-video-miniport-drivers--windows-.md)に対して一連の新しい関数が実装する必要があります。 新しいメンバーを初期化するために必ず[**ビデオ\_HW\_初期化\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff570505)これらの新しい関数を指すようにします。

-   呼び出しを更新して[ **VideoPortInitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff570320)で、 [ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff556159)関数。 4 番目のパラメーター (*HwContext*) する必要があります**NULL** Windows 2000 以降。

-   更新プログラム、 [ *HwVidFindAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff567332)関数。 列挙可能なバスでは、上のデバイス用*HwVidFindAdapter*ように変更する必要があります。

    -   ほとんどのデバイス検出コードを削除します。 これは、ためへの呼び出し[ *HwVidFindAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff567332) Windows 2000 で PnP マネージャーで、デバイスが既に検出されたことを意味します。
    -   呼び出す[ **VideoPortGetAccessRanges** ](https://msdn.microsoft.com/library/windows/hardware/ff570302)デバイスが応答するバス相対物理アドレスを取得します。 PnP マネージャーでは、これらのアドレスが割り当てられます。
    -   ドライバーは、1 つ以上のデバイスの種類をサポートする場合は、デバイスの種類を決定します。
    -   無視する、 [*再度*](https://msdn.microsoft.com/library/windows/hardware/ff567332)パラメーター。 これは、システムが呼び出すため*HwVidFindAdapter*デバイスあたり 1 回だけです。

    PnP 静止しようと、デバイスを開始する責任が nonenumerable バス ISA などのデバイスは、 [ *HwVidFindAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff567332)をデバイスが実際に存在するかどうかを判断します。

-   更新プログラム、**します。製造**デバイスとベンダーの ID を含むように、ドライバーの INF ファイルのセクション これは、機能は、PnP マネージャーは、INF ファイルをデバイスに関連付けることができること必要です。 Windows NT 4.0 と更新された Windows 2000 以降のサンプル**します。製造**セクションに従ってください。

    ```cpp
    [ABC.Mfg]   ; Windows NT V4.0 INF
    %ABC% ABC Graphics Accelerator A = abc
    %ABC% ABC Graphics Accelerator B = abc

    [ABC.Mfg]   ; Windows 2000 and later INF
    %ABC% ABC Graphics Accelerator A = abc, PCI\VEN_ABCD&DEV_0123
    %ABC% ABC Graphics Accelerator B = abc, PCI\VEN_ABCD&DEV_4567
    ```

使用することができます、 *geninf.exe* INF を生成するドライバー開発キット (DDK) に含まれているツールです。 (前に、DDK、Windows Driver Kit \[WDK\])。留意して、ただしを*geninf.exe* Windows NT 4.0 の INF は作成されません。 によって生成される INF ファイルを変更する必要があります*geninf.exe* Windows NT 4.0 をサポートする場合。 参照してください[グラフィックス INF ファイルの作成](creating-graphics-inf-files.md)の詳細。

Windows 2000 とビデオ ポートを後では、従来のドライバーと Windows NT 4.0 のミニポート ドライバーをサポートします。 システムが実行されていることもレガシ ミニポート ドライバーは実行中のシステムに追加されたときに自動的に検出中に、システムからレガシ ミニポート ドライバーのグラフィックス アダプターを削除できません。

 

 





