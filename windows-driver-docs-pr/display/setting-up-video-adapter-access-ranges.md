---
title: ビデオ アダプター アクセス範囲の設定
description: ビデオ アダプター アクセス範囲の設定
ms.assetid: 250c5611-c6f5-49b5-94bc-93a1b43312e6
keywords:
- ビデオアダプターのアクセス範囲 WDK ビデオミニポート
- WDK の範囲 WDK ビデオミニポート
- 論理範囲アドレス WDK ビデオミニポート
- アダプターアクセス範囲 WDK ビデオミニポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cabc80f084aa33a27ad274477f6d63da4451485e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829487"
---
# <a name="setting-up-video-adapter-access-ranges"></a>ビデオ アダプター アクセス範囲の設定


## <span id="ddk_setting_up_video_adapter_access_ranges_gg"></span><span id="DDK_SETTING_UP_VIDEO_ADAPTER_ACCESS_RANGES_GG"></span>


一連の[**ビデオ\_ACCESS\_範囲**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_video_access_range)型の要素には、ビデオアダプターがデコードするメモリまたは i/o ポートの1つ以上の範囲が記述されています。 この配列内の各アクセス範囲要素には、バス相対の物理アドレス値が含まれます。

ミニポートドライバーの[*HwVidFindAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_find_adapter)ルーチンは、アダプターが応答するすべての PCI メモリ、ポート、またはポートの範囲を要求する必要があります。 *HwVidFindAdapter*は、アダプターおよび[**VIDEO\_\_PORT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_video_port_config_info)の**AdapterInterfaceType**の値に応じて、構成\_情報に応じて、次の **VideoPort * * * Xxx*関数の一部を呼び出して必要なものを取得できます。バス相対構成データ:

[**VideoPortGetAccessRanges**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportgetaccessranges)

[**VideoPortGetBusData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportgetbusdata)

[**VideoPortGetDeviceData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportgetdevicedata)

[**VideoPortGetRegistryParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportgetregistryparameters)

[**VideoPortVerifyAccessRanges**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportverifyaccessranges)

HwVidFindAdapter が**Videoportgetbusdata**または**Videoportgetbusdata**を呼び出すことによってバス相対アクセス範囲情報を取得できない場合、または**Videoportgetbusdata**または**VideoPortGetRegistryParameters**を使用してレジストリからアクセス範囲が指定されている場合、ミニポートドライバーには、アクセス範囲のバス相対既定値のセットが必要です。

すべての*HwVidFindAdapter*関数は、要求されたバス相対物理アドレス範囲を、 **Videoportgetdevicebase**論理アドレス範囲を持つカーネルモードアドレス空間の範囲 (特に複数のバスコンピューター) にマップする必要があります。

マップされた論理範囲アドレスを使用すると、ドライバーは **Videoportread * * * xxx*関数と **VideoPortWrite * * * xxx*関数を呼び出して、アダプターに対して読み取りまたは書き込みを行うことができます。 これらのカーネルモードアドレスは、 [**Videoportcomparememory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportcomparememory)、 [**VideoPortMoveMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportmovememory)、 [**VideoPortZeroDeviceMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportzerodevicememory)、または[**videoportゼロメモリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportzeromemory)に渡すこともできます。 I/o space のマップされた範囲の場合、ミニポートドライバーは **Videoportreadport * * * xxx*関数と **VideoPortWritePort * ** * * xxx 関数を呼び出します。 メモリ内のマップされた範囲の場合、ミニポートドライバーは **Videoportreadregister * * * xxx*および **VideoPortWriteRegister * * * xxx*関数を呼び出します。

HwVidFindAdapter 関数は、 [**Videoportverifyaccessranges**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportgetdevicebase)を呼び出す*前*に、常に[**videoportverifyaccessranges**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportverifyaccessranges)または[**videoportverifyaccessranges**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportgetaccessranges)を呼び出す*必要があり*ます。 [](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_find_adapter)

-   **Videoportverifyaccessranges**または**videoportverifyaccessranges**への呼び出しが成功すると、バス固有のビデオメモリに対するミニポートドライバーの要求が確立され、アダプターのアドレスまたは i/o ポートがレジストリに登録されます。 ただし、後で**Videoportverifyaccessranges**または**videoportverifyaccessranges**を呼び出すと、ドライバーの以前に要求されたリソースが消去され、最後に渡された範囲に置き換えられることに注意する必要があります。呼び出された関数。 したがって、ドライバーの要求の範囲がこれらの関数を個別に呼び出す場合は、既に要求されているものも含め、すべての範囲配列を渡す必要があります。

-   *HwVidFindAdapter*は、アダプターのアクセス範囲の小さなセットを要求し、このセットを使用して、アダプターがミニポートドライバーでサポートされているものであるかどうかを判断し、別のの呼び出し**を使用して、サポートされているアダプターのアクセス範囲の完全なセットを要求できます。VideoPortGetAccessRanges**または**Videoportgetaccessranges**。 ここでも、これらの VideoPort を正常に呼び出します。特定のアダプターの accessversionルーチンは、レジストリ内の呼び出し元の以前の要求を上書きします。

-   割り込みベクターなどの他の種類のハードウェアリソースを要求するには、ミニポートドライバーで、ビデオ\_ポート\_CONFIG\_INFO に適切な値を設定し、 **Videoportverifyaccessranges**を呼び出す必要があります。または **、VideoPortGetAccessRanges**。

-   **Videoportgetaccessranges**または**videoportgetaccessranges**を呼び出すと、ミニポートドライバーが、別のドライバーで既に使用されているレジスタまたはデバイスのメモリアドレスを使用しないようになります。

-   レジストリでアダプターのバス相対ハードウェアリソースを要求すると、後で読み込まれるドライバーが、アダプターに対して同じアクセス範囲 (およびその他のハードウェアリソース) を使用しようとすることがなくなります。 また、それ以降に読み込まれたドライバーがビデオアダプターの初期化状態を変更できないようにします。

レガシリソースをデコードするハードウェアのミニポートドライバーは、その**Driverentry**ルーチン (実装されている場合は*HwVidLegacyResources*ルーチン) でこれらのリソースを要求する必要があります。 レガシリソースとは、デバイスの PCI 構成領域に記載されていないが、デバイスによってデコードされるリソースのことです。 詳細については、「[レガシリソース](claiming-legacy-resources.md)の要求」を参照してください。

ミニポートドライバーが読み込まれ、その[*HwVidInitialize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_initialize)関数が実行されると、ミニポートドライバーの[*HwVidStartIO*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_start_io)関数が呼び出され、ミニポートドライバーが対応するディスプレイドライバーに表示するビデオメモリのアクセス範囲をマップします。

 

 





