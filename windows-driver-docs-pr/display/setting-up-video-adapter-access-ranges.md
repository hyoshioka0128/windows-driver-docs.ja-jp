---
title: ビデオ アダプター アクセス範囲の設定
description: ビデオ アダプター アクセス範囲の設定
ms.assetid: 250c5611-c6f5-49b5-94bc-93a1b43312e6
keywords:
- ビデオ アダプターへのアクセスの範囲は WDK ビデオのミニポート
- 範囲は、WDK のビデオのミニポート
- 範囲の論理アドレス WDK のビデオのミニポート
- アダプターへのアクセスの範囲は WDK ビデオのミニポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f01a2dbbd733a69ba0ac5f19d39216acece5929f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339698"
---
# <a name="setting-up-video-adapter-access-ranges"></a>ビデオ アダプター アクセス範囲の設定


## <span id="ddk_setting_up_video_adapter_access_ranges_gg"></span><span id="DDK_SETTING_UP_VIDEO_ADAPTER_ACCESS_RANGES_GG"></span>


配列の[**ビデオ\_アクセス\_範囲**](https://msdn.microsoft.com/library/windows/hardware/ff570498)-型の要素には、メモリやビデオ アダプターがデコード I/O ポートの 1 つまたは複数の範囲がについて説明します。 この配列内の各アクセス範囲要素には、物理アドレスのバスの相対値が含まれています。

ミニポート ドライバーの[ *HwVidFindAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff567332)ルーチンは、すべての PCI メモリとポートまたはアダプターが応答するポートの範囲を要求する必要があります。 アダプターに応じて、 **AdapterInterfaceType**値[**ビデオ\_ポート\_CONFIG\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff570531)、 *HwVidFindAdapter* 、次のいくつかを呼び出すことができます **ビデオ ポート * * * Xxx* bus 相対の必要な構成データを取得する関数。

[**VideoPortGetAccessRanges**](https://msdn.microsoft.com/library/windows/hardware/ff570302)

[**VideoPortGetBusData**](https://msdn.microsoft.com/library/windows/hardware/ff570306)

[**VideoPortGetDeviceData**](https://msdn.microsoft.com/library/windows/hardware/ff570311)

[**VideoPortGetRegistryParameters**](https://msdn.microsoft.com/library/windows/hardware/ff570316)

[**VideoPortVerifyAccessRanges**](https://msdn.microsoft.com/library/windows/hardware/ff570377)

場合*HwVidFindAdapter*呼び出して bus 相対アクセス範囲情報を取得できません**VideoPortGetBusData**または**VideoPortGetAccessRanges**、または、レジストリから**VideoPortGetDeviceData**または**VideoPortGetRegistryParameters**、ミニポート ドライバーは一連のアクセスの範囲のバス相対の既定値が必要です。

すべて*HwVidFindAdapter*関数はカーネル モード アドレス空間内の範囲にそれぞれのクレームのバスの相対物理アドレス範囲をマップする必要があります**VideoPortGetDeviceBase**論理アドレスの範囲特に、バスの複数のマシン。

論理アドレス範囲にマップされたアドレスを使用して、ドライバーを呼び出すことができます、**VideoPortRead * * * Xxx*と **VideoPortWrite * * * Xxx*読み取りまたは書き込みをアダプターにする関数。 これらのカーネル モード アドレスも渡すことができますを[ **VideoPortCompareMemory**](https://msdn.microsoft.com/library/windows/hardware/ff570285)、 [ **VideoPortMoveMemory**](https://msdn.microsoft.com/library/windows/hardware/ff570332)、 [**VideoPortZeroDeviceMemory**](https://msdn.microsoft.com/library/windows/hardware/ff570492)、や[ **VideoPortZeroMemory**](https://msdn.microsoft.com/library/windows/hardware/ff570493)します。 I/O の領域にマップされた範囲は、ミニポート ドライバーの呼び出し、**VideoPortReadPort * * * Xxx*と **VideoPortWritePort * * * Xxx*関数。 メモリ内の対応付けられた範囲、ミニポート ドライバーの呼び出し、**VideoPortReadRegister * * * Xxx*と **VideoPortWriteRegister * * * Xxx*関数。

[ *HwVidFindAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff567332)関数*常にする必要があります*呼び出す[ **VideoPortVerifyAccessRanges** ](https://msdn.microsoft.com/library/windows/hardware/ff570377)または[ **VideoPortGetAccessRanges** ](https://msdn.microsoft.com/library/windows/hardware/ff570302)正常*する前に*呼び出し[ **VideoPortGetDeviceBase**](https://msdn.microsoft.com/library/windows/hardware/ff570310).

-   すべての成功した呼び出しに**VideoPortVerifyAccessRanges**または**VideoPortGetAccessRanges**ミニポート ドライバーのバスに固有のビデオ メモリの要求およびアドレスまたは I/O ポートの登録設定のレジストリのアダプターです。 ただし、注意をすることが重要、後続の呼び出しに**VideoPortVerifyAccessRanges**または**VideoPortGetAccessRanges**により、消去するドライバーの以前に要求したリソースと最後に呼び出された関数に渡された範囲に置き換えられます。 そのため、ドライバーがこれらの関数に個別の呼び出しによって範囲を要求する場合は既にものも含め、すべての範囲の配列に渡す必要があります。

-   *HwVidFindAdapter*アダプターのアクセスの範囲の小さなセットを要求、このセットを使用して、アダプターが、ミニポート ドライバーがサポートしているかどうかを判断およびを別の呼び出しでサポートされているアダプターのアクセスの範囲の完全なセットをクレーム**VideoPortGetAccessRanges**または**VideoPortVerifyAccessRanges**します。 ここでも、これらに呼び出しが成功した**ビデオ ポート.AccessRanges**ルーチンは特定のアダプターのレジストリで、呼び出し元の前の要求が上書きされます。

-   要求の他の種類、割り込みベクトルなどのハードウェア リソースのミニポート ドライバーは、ビデオの適切な値を設定する必要があります\_ポート\_CONFIG\_情報と呼び出し**VideoPortVerifyAccessRanges**、呼び出すことが必要がありますまたは**VideoPortGetAccessRanges**します。

-   呼び出す**VideoPortGetAccessRanges**または**VideoPortVerifyAccessRanges**正常に確実にミニポート ドライバーはレジスタの使用を試みませんまたはデバイスのメモリ アドレスによって既に使用されて別ドライバー。

-   レジストリ内のアダプターのバス相対ハードウェア リソースを要求すると、アダプターのドライバーから同じアクセス範囲 (およびその他のハードウェア リソース) を使用しようとしました。 後で読み込むことができないようにします。 後からロード ドライバーが、ビデオ アダプターの初期化状態を変更できなくなります。

レガシ リソースにデコードするハードウェアのミニポート ドライバーがこれらのリソースを要求する必要があります、 **DriverEntry**ルーチン、実装されている場合、またはその*HwVidLegacyResources*ルーチン。 レガシ リソースはそれらのリソースがデバイスの PCI 構成領域に表示されませんが、デバイスによってデコードされます。 参照してください[と主張してレガシ リソース](claiming-legacy-resources.md)詳細についてはします。

後、ミニポート ドライバーが読み込まれるとその[ *HwVidInitialize* ](https://msdn.microsoft.com/library/windows/hardware/ff567345)関数は、実行、ミニポート ドライバーの[ *HwVidStartIO* ](https://msdn.microsoft.com/library/windows/hardware/ff567367)関数ミニポート ドライバーは、対応する、ディスプレイ ドライバーに表示されるビデオ メモリの任意のアクセスの範囲にマップするには、呼び出されます。

 

 





