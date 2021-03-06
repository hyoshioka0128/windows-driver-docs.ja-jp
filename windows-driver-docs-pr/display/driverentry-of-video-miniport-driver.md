---
title: ビデオ ミニポート ドライバーの DriverEntry 関数
description: DriverEntry は、ビデオのミニポート ドライバーへの初期のエントリ ポイントです。
ms.assetid: b927dd2c-19e1-49bc-b30b-530efe2ba13b
keywords:
- DriverEntry 関数ディスプレイ デバイス
topic_type:
- apiref
api_name:
- DriverEntry
api_location:
- NtosKrnl.exe
api_type:
- DllExport
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: e1ea2aa1be31527e253ff2a17e3455f15a271878
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384267"
---
# <a name="driverentry-of-video-miniport-driver-function"></a>ビデオ ミニポート ドライバーの DriverEntry 関数


**DriverEntry**ビデオのミニポート ドライバーへの最初のエントリ ポイントです。

<a name="syntax"></a>構文
------

```cpp
ULONG DriverEntry(
  _In_ PVOID Context1,
  _In_ PVOID Context2
);
```

<a name="parameters"></a>パラメーター
----------

*Context1* \[で\]ミニポート ドライバーを呼び出す必要がありますが、コンテキスト値へのポインター [ **VideoPortInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportinitialize)します。 このコンテキストの値は、このミニポート ドライバーにシステムによって作成されたドライバー オブジェクトを識別します。

*Context2* \[で\]ミニポート ドライバーを呼び出す必要がありますが、2 番目のコンテキスト値へのポインター [ **VideoPortInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportinitialize)します。 このコンテキストの値は、このミニポート ドライバーのレジストリ パスを識別します。

<a name="return-value"></a>戻り値
------------

**DriverEntry**によって返される値を返します[ **VideoPortInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportinitialize)します。

<a name="remarks"></a>注釈
-------

各ミニポート ドライバーが明示的にという名前の関数をいる必要があります**DriverEntry**読み込まれるためです。 **DriverEntry** I/O システムで直接呼び出されます。

**DriverEntry**次の手順を実行する必要があります。

-   スタックのメモリを割り当て、 [**ビデオ\_HW\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/ns-video-_video_hw_initialization_data)構造、および呼び出し[ **VideoPortZeroMemory** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportzeromemory)が 0 に初期化します。

-   ビデオの特定のドライバーとアダプター固有の値を入力\_HW\_初期化\_ミニポート ドライバーのエントリ ポイントを含む、データ メンバー。 ミニポート ドライバー指定のルーチンには、次のエントリ ポイントを設定する必要があります。

    [*HwVidFindAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_find_adapter)

    [*HwVidInitialize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_initialize)

    [*HwVidStartIO*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_start_io)

    [*HwVidInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_interrupt)

    [*HwVidQueryInterface*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_query_interface)

    [*HwVidGetVideoChildDescriptor*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_get_child_descriptor)

    [*HwVidGetPowerState*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_power_get)

    [*HwVidSetPowerState*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_power_set)

-   ドライバーのハードウェアでは、レガシ リソースをサポートする場合、ドライバーは、それらを報告する必要があります。 **DriverEntry**ドライバーのコンパイル時にリソースの一覧がわかっている場合は、次を行う必要があります。

    -   要求し、このようなすべてのリソースでのレポート、 **HwLegacyResourceList**と**HwLegacyResourceCount**のメンバー、 [**ビデオ\_HW\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/ns-video-_video_hw_initialization_data)構造体。 レガシ リソースはそれらのリソースがデバイスの PCI 構成領域に表示されませんが、デバイスによってデコードされます。
    -   入力、 **RangePassive**フィールドごとに[**ビデオ\_アクセス\_範囲**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/ns-video-_video_access_range)ミニポート ドライバーで定義された構造体。

    代わりに、ドライバーを実装する必要がありますレガシ リソースの一覧は、実行時まで決定できない場合、 [ *HwVidLegacyResources* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_legacyresources)にまとめて報告する関数。

-   呼び出す[ **VideoPortInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportinitialize)を渡して、 *Context1*と*Context2* ビデオへのポインター、最初の2つのパラメーターとして\_HW\_初期化\_3 番目のパラメーターとしてのデータ構造と**NULL** 4 番目のパラメーターとして。

**DriverEntry**によって返される値を反映する必要があります[ **VideoPortInitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportinitialize)呼び出し元に戻します。

場合**DriverEntry**リソースの要求は、ハードウェア デコードが PCI によってを請求されていないリソースだけを含める必要があります。 ミニポート ドライバーが「再利用」これらのレガシ リソースを後続の呼び出し後にもう一度[ **VideoPortVerifyAccessRanges**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportverifyaccessranges)ただし、ビデオ ポート ドライバーは、このような要求を無視だけです。以前に要求されたリソース。 電源管理とドッキングが無効になります、システムで、ミニポート ドライバーで従来のアクセスの範囲を要求しようとしました**VideoPortVerifyAccessRanges**をがない以前に要求されたで、 **HwLegacyResourceList。** のメンバー、 [**ビデオ\_HW\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/ns-video-_video_hw_initialization_data)中に構造体**DriverEntry**(または[ *HwVidLegacyResources*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_legacyresources)、実装されている場合)。

Microsoft Windows 2000 と Windows NT 4.0 を実行しているコンピューターをサポートするドライバーを後で、ハードウェア構成の定数が定義されている*video.h*します。 これらの定数は、次の表で説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">定数</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>SIZE_OF_NT4_VIDEO_PORT_CONFIG_INFO</p></td>
<td align="left"><p>サイズ (バイト単位)、Windows NT 4.0 の<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/ns-video-_video_port_config_info" data-raw-source="[&lt;strong&gt;VIDEO_PORT_CONFIG_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/ns-video-_video_port_config_info)"> <strong>VIDEO_PORT_CONFIG_INFO</strong> </a>構造体。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SIZE_OF_NT4_VIDEO_HW_INITIALIZATION_DATA</p></td>
<td align="left"><p>サイズ (バイト単位)、Windows NT 4.0 の<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/ns-video-_video_hw_initialization_data" data-raw-source="[&lt;strong&gt;VIDEO_HW_INITIALIZATION_DATA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/ns-video-_video_hw_initialization_data)"> <strong>VIDEO_HW_INITIALIZATION_DATA</strong> </a>構造体。 場合<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportinitialize" data-raw-source="[&lt;strong&gt;VideoPortInitialize&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportinitialize)"> <strong>VideoPortInitialize</strong> </a>失敗した場合、ビデオのミニポート ドライバーを設定する必要があります、 <strong>HwInitDataSize</strong>のサイズに VIDEO_HW_INITIALIZATION_DATA 構造体のメンバーこの構造体の Windows 2000 (以降) のバージョンまたは Windows NT 4.0 バージョンのいずれか。 ミニポート ドライバーを実行するオペレーティング システムのバージョンと一致する適切な構造体のサイズを選択します。 ビデオのミニポート ドライバーに呼び出す必要がありますし、 <strong>VideoPortInitialize</strong>もう一度です。 使用例は、Windows ドライバー開発キット (DDK) が含まれていたビデオのミニポート ドライバーのサンプルを参照してください。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SIZE_OF_W2K_VIDEO_HW_INITIALIZATION_DATA</p></td>
<td align="left"><p>サイズ (バイト)、Windows 2000 以降の<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/ns-video-_video_hw_initialization_data" data-raw-source="[&lt;strong&gt;VIDEO_HW_INITIALIZATION_DATA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/ns-video-_video_hw_initialization_data)"> <strong>VIDEO_HW_INITIALIZATION_DATA</strong> </a>構造体。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SIZE_OF_WXP_VIDEO_HW_INITIALIZATION_DATA</p></td>
<td align="left"><p>サイズ (バイト)、Windows Vista 以降<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/ns-video-_video_hw_initialization_data" data-raw-source="[&lt;strong&gt;VIDEO_HW_INITIALIZATION_DATA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/ns-video-_video_hw_initialization_data)"> <strong>VIDEO_HW_INITIALIZATION_DATA</strong> </a>構造体。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SIZE_OF_WXP_VIDEO_PORT_CONFIG_INFO</p></td>
<td align="left"><p>Windows Vista のバイト単位のサイズ、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/ns-video-_video_port_config_info" data-raw-source="[&lt;strong&gt;VIDEO_PORT_CONFIG_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/ns-video-_video_port_config_info)"> <strong>VIDEO_PORT_CONFIG_INFO</strong> </a>構造体。</p></td>
</tr>
</tbody>
</table>

 

**DriverEntry**ページング可能な行う必要があります。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>対象プラットフォーム</p></td>
<td align="left">Desktop</td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Video.h (Video.h を含む)</td>
</tr>
<tr class="odd">
<td align="left"><p>Library</p></td>
<td align="left">NtosKrnl.lib</td>
</tr>
<tr class="even">
<td align="left"><p>DLL</p></td>
<td align="left">NtosKrnl.exe</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[*HwVidFindAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_find_adapter)

[*HwVidLegacyResources*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_legacyresources)

[**ビデオ\_HW\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/ns-video-_video_hw_initialization_data)

[**VideoPortInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportinitialize)

[**VideoPortVerifyAccessRanges**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportverifyaccessranges)

[**VideoPortZeroMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportzeromemory)

 

 






