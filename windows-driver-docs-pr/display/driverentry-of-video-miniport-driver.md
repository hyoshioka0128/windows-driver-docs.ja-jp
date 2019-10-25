---
title: ビデオミニポートドライバー関数の DriverEntry
description: DriverEntry は、ビデオミニポートドライバーへの最初のエントリポイントです。
ms.assetid: b927dd2c-19e1-49bc-b30b-530efe2ba13b
keywords:
- DriverEntry 関数のディスプレイデバイス
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
ms.openlocfilehash: 7c23d16c3f026ca09fea9efb2bf12cc080af26b7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839731"
---
# <a name="driverentry-of-video-miniport-driver-function"></a>ビデオミニポートドライバー関数の DriverEntry


**Driverentry**は、ビデオミニポートドライバーへの最初のエントリポイントです。

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

*Context1* \[、ミニポートドライバーが[**videoportinitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportinitialize)を呼び出す必要があるコンテキスト値へのポインター\] ます。 このコンテキスト値は、このミニポートドライバー用にシステムによって作成されたドライバーオブジェクトを識別します。

*Context2* \[、ミニポートドライバーが[**videoportinitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportinitialize)を呼び出す必要がある2番目のコンテキスト値へのポインター\] ます。 このコンテキスト値は、このミニポートドライバーのレジストリパスを識別します。

<a name="return-value"></a>戻り値
------------

**Driverentry**は、 [**videoportinitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportinitialize)によって返された値を返します。

<a name="remarks"></a>注釈
-------

各ミニポートドライバーは、読み込むために**Driverentry**という名前の関数を明示的に指定する必要があります。 **Driverentry**は、i/o システムによって直接呼び出されます。

**Driverentry**では、次の手順を実行する必要があります。

-   [**ビデオ\_HW\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_video_hw_initialization_data)構造のスタックにメモリを割り当て、 [**Videoportzero memory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportzeromemory)を呼び出して0を初期化します。

-   ビデオ\_HW\_初期化\_データメンバー (ミニポートドライバーのエントリポイントを含む) のドライバー固有の値とアダプター固有の値を入力します。 次のエントリポイントは、ミニポートドライバーによって提供されるルーチンに設定する必要があります。

    [*HwVidFindAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_find_adapter)

    [*HwVidInitialize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_initialize)

    [*HwVidStartIO*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_start_io)

    [*HwVidInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_interrupt)

    [*HwVidQueryInterface*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_query_interface)

    [*HwVidGetVideoChildDescriptor*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_get_child_descriptor)

    [*HwVidGetPowerState*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_power_get)

    [*HwVidSetPowerState*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_power_set)

-   ドライバーのハードウェアでレガシリソースがサポートされている場合、ドライバーはそれらを報告する必要があります。 ドライバーのコンパイル時にリソースリストがわかっている場合、 **Driverentry**は次のことを実行する必要があります。

    -   [**ビデオ\_HW\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_video_hw_initialization_data)構造内のすべての**リソースを要求**および**報告します**。 レガシリソースとは、デバイスの PCI 構成領域に記載されていないが、デバイスによってデコードされるリソースのことです。
    -   ミニポートドライバーで定義されている各[**ビデオ\_ACCESS\_範囲**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_video_access_range)構造に応じて、 **rangepassive**フィールドに値を入力します。

    レガシリソースリストを実行時まで特定できない場合は、ドライバーが[*HwVidLegacyResources*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_legacyresources)関数を実装して報告する必要があります。

-   [**Videoportinitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportinitialize)を呼び出し、最初の2つのパラメーターとして*Context1*と*Context2*を渡します。次に、3番目のパラメーターとして VIDEO\_HW\_初期化\_データ構造へのポインターを渡し、4番目のパラメーターとして**NULL**を指定します。引き.

**Driverentry**は、 [**videoportinitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportinitialize)によって返された値を呼び出し元に反映させる必要があります。

**Driverentry**がリソースを要求する場合は、ハードウェアがデコードし、PCI によって要求されていないリソースのみを含める必要があります。 ミニポートドライバーは、以降の呼び出しでこれらのレガシリソースを再利用して、 [**Videoportverifyaccessranges**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportverifyaccessranges); に再利用できます。ただし、ビデオポートドライバーは、以前に要求されたリソースの要求を無視するだけです。 ビデオの**HwLegacyResourceList**メンバーで以前に要求されていなかった**Videoportverifyaccessranges**のレガシアクセス範囲をミニポートドライバーが要求しようとすると、システムで電源管理とドッキングが無効になり[ **\_HW\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_video_hw_initialization_data) 、 **driverentry** (または[*HwVidLegacyResources*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_legacyresources)で実装されている場合) の間にデータ構造を初期\_化します。

Windows NT 4.0 を実行しているコンピューターもサポートする Microsoft Windows 2000 以降のドライバーでは、ハードウェア構成定数は、ビデオで定義されています *。* 次の表では、これらの定数について説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">定数</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>SIZE_OF_NT4_VIDEO_PORT_CONFIG_INFO</p></td>
<td align="left"><p>Windows NT 4.0 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_video_port_config_info" data-raw-source="[&lt;strong&gt;VIDEO_PORT_CONFIG_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_video_port_config_info)"><strong>VIDEO_PORT_CONFIG_INFO</strong></a>構造体のサイズ (バイト単位)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SIZE_OF_NT4_VIDEO_HW_INITIALIZATION_DATA</p></td>
<td align="left"><p>Windows NT 4.0 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_video_hw_initialization_data" data-raw-source="[&lt;strong&gt;VIDEO_HW_INITIALIZATION_DATA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_video_hw_initialization_data)"><strong>VIDEO_HW_INITIALIZATION_DATA</strong></a>構造体のサイズ (バイト単位)。 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportinitialize" data-raw-source="[&lt;strong&gt;VideoPortInitialize&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportinitialize)"><strong>Videoportinitialize</strong></a>が失敗した場合、ビデオミニポートドライバーは、VIDEO_HW_INITIALIZATION_DATA 構造体の<strong>Hwinitdatasize</strong>メンバーを、この構造体または Windows NT 4.0 の windows 2000 (以降) バージョンのいずれかのサイズに設定する必要があります。バージョン。 ミニポートドライバーが実行されるオペレーティングシステムのバージョンに合わせて、適切な構造サイズを選択します。 ビデオミニポートドライバーは、再び<strong>Videoportinitialize</strong>を呼び出す必要があります。 の使用例については、Windows Driver Development Kit (DDK) に含まれていたビデオミニポートドライバーのサンプルを参照してください。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SIZE_OF_W2K_VIDEO_HW_INITIALIZATION_DATA</p></td>
<td align="left"><p>Windows 2000 以降の<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_video_hw_initialization_data" data-raw-source="[&lt;strong&gt;VIDEO_HW_INITIALIZATION_DATA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_video_hw_initialization_data)"><strong>VIDEO_HW_INITIALIZATION_DATA</strong></a>構造体のサイズ (バイト単位)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SIZE_OF_WXP_VIDEO_HW_INITIALIZATION_DATA</p></td>
<td align="left"><p>Windows Vista 以降の<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_video_hw_initialization_data" data-raw-source="[&lt;strong&gt;VIDEO_HW_INITIALIZATION_DATA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_video_hw_initialization_data)"><strong>VIDEO_HW_INITIALIZATION_DATA</strong></a>構造体のサイズ (バイト単位)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SIZE_OF_WXP_VIDEO_PORT_CONFIG_INFO</p></td>
<td align="left"><p>Windows Vista <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_video_port_config_info" data-raw-source="[&lt;strong&gt;VIDEO_PORT_CONFIG_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_video_port_config_info)"><strong>VIDEO_PORT_CONFIG_INFO</strong></a>構造体のサイズ (バイト単位)。</p></td>
</tr>
</tbody>
</table>

 

**Driverentry**は、ページング可能にする必要があります。

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
<td align="left">ビデオ .h (ビデオ .h を含む)</td>
</tr>
<tr class="odd">
<td align="left"><p>Library</p></td>
<td align="left">Ntoskrnl.exe</td>
</tr>
<tr class="even">
<td align="left"><p>DLL</p></td>
<td align="left">Ntoskrnl.exe</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[*HwVidFindAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_find_adapter)

[*HwVidLegacyResources*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_legacyresources)

[**VIDEO\_HW\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_video_hw_initialization_data)

[**VideoPortInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportinitialize)

[**VideoPortVerifyAccessRanges**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportverifyaccessranges)

[**Videoportゼロメモリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportzeromemory)

 

 






