---
title: レガシ リソースの要求
description: レガシ リソースの要求
ms.assetid: f3e573a1-0e7a-422b-8bed-db3ba7712a2f
keywords:
- ビデオのミニポート ドライバー WDK Windows 2000 では、レガシ リソース
- レガシ リソース WDK ビデオのミニポート
- ビデオのミニポート ドライバー WDK Windows 2000 では、初期化しています
- ビデオのミニポート ドライバーの初期化
- VIDEO_HW_INITIALIZATION_DATA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f5fa4670dee6cd357783448429fe79edd46e1b5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370708"
---
# <a name="claiming-legacy-resources"></a>レガシ リソースの要求


## <span id="ddk_claiming_legacy_resources_gg"></span><span id="DDK_CLAIMING_LEGACY_RESOURCES_GG"></span>


ビデオのミニポート ドライバーが要求する必要があり、レポート内のすべてのレガシ リソースその[**ビデオ\_HW\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/ns-video-_video_hw_initialization_data)ドライバーの初期化中に構造体. レガシ リソースはそれらのリソースがデバイスの PCI 構成領域に表示されませんが、デバイスによってデコードされます。 電源管理とドッキングのこのセクションで説明した方法で報告していないレガシ リソースを検出したときに、NT ベースのオペレーティング システムが無効になります。

ミニポート ドライバーでは、このような従来のリソースをレポートには、次を行う必要があります。

- 次の 2 つのフィールドを入力デバイスは、コンパイル時に既知のレガシ リソースの一覧がある場合、 [**ビデオ\_HW\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/ns-video-_video_hw_initialization_data)作成されで初期化する構造体、 [ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/display/driverentry-of-video-miniport-driver)ルーチン。

  <table>
  <colgroup>
  <col width="50%" />
  <col width="50%" />
  </colgroup>
  <thead>
  <tr class="header">
  <th align="left">構造体のメンバー</th>
  <th align="left">定義</th>
  </tr>
  </thead>
  <tbody>
  <tr class="odd">
  <td align="left"><p><strong>HwLegacyResourceList</strong></p></td>
  <td align="left"><p>配列を指す<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/ns-video-_video_access_range" data-raw-source="[&lt;strong&gt;VIDEO_ACCESS_RANGE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/ns-video-_video_access_range)"> <strong>VIDEO_ACCESS_RANGE</strong> </a>構造体。 各構造体には、デバイスの I/O ポートまたは PCI 構成領域で一覧表示されていないビデオ アダプターのメモリの範囲について説明します。</p></td>
  </tr>
  <tr class="even">
  <td align="left"><p><strong>HwLegacyResourceCount</strong></p></td>
  <td align="left"><p>先の配列の要素の数は、 <strong>HwLegacyResourceList</strong>ポイント。</p></td>
  </tr>
  </tbody>
  </table>

     

<!-- -->

-   デバイスのレガシ リソースの一覧がコンパイル時に不明な場合は、実装、 [ *HwVidLegacyResources* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_legacyresources)関数を初期化、 **HwGetLegacyResources**ビデオのメンバー\_HW\_初期化\_データをこの関数をポイントします。 たとえば、レガシ リソースのセットが異なる 2 つのデバイスをサポートしているミニポート ドライバーの実装は*HwVidLegacyResources*実行時に従来のリソースを報告します。 ビデオ ポート ドライバーは無視されます、 **HwLegacyResourceList**と**HwLegacyResourceCount**ビデオのメンバー\_HW\_初期化\_データと、ミニポート ドライバー実装*HwVidLegacyResources*します。

-   入力、 **RangePassive**ビデオごとのフィールド\_アクセス\_適宜ミニポート ドライバーで定義されている範囲の構造体。 設定**RangePassive**ビデオに\_範囲\_パッシブ\_デコードは、リージョンは、ハードウェアでデコードされますが、画面とビデオのミニポート ドライバーは決して接触していることを示します。 設定**RangePassive**ビデオに\_範囲\_10\_ビット\_デコードは、デバイスが、リージョンのポート アドレスの 10 のビットをデコードすることを示します。

ここでも、ドライバーはハードウェア デコードが PCI によってを請求されていないリソースのみを含める必要があります。 従来、最小限のリソースは、次のようなものになりますを要求する必要があるドライバー コードします。

```cpp
//              RangeStart        RangeLength
//              |                 |      RangeInIoSpace
//              |                 |      |  RangeVisible
//        +-----+-----+           |      |  |  RangeShareable
//       low         high         |      |  |  |  RangePassive
//        v           v           v      v  v  v  v
VIDEO_ACCESS_RANGE AccessRanges[] = {
    // [0] (0x3b0-0x3bb)
    {0x000003b0, 0x00000000, 0x0000000c, 1, 1, 1, 0},
    // [1] (0x3c0-0x3df)
    {0x000003C0, 0x00000000, 0x00000010, 1, 1, 1, 0},
    // [2] (0xa0000-0xaffff)
    {0x000A0000, 0x00000000, 0x00010000, 1, 0, 0, 0},
};
 
// Within the DriverEntry routine:
VIDEO_HW_INITIALIZATION_DATA hwInitData;
hwInitData.HwLegacyResourceList = AccessRanges;
hwInitData.HwLegacyResourceCount = 3;
```

ミニポート ドライバーが「再利用」レガシ リソースを後続の呼び出し後にもう一度[ **VideoPortVerifyAccessRanges**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportverifyaccessranges)ただし、ビデオ ポート ドライバーはだけを無視する要求、このような以前。要求されたリソース。 電源管理とドッキングが無効になります、システムで、ミニポート ドライバーで従来のアクセスの範囲を要求しようとしました**VideoPortVerifyAccessRanges**をがない以前に要求されたで、 **HwLegacyResourceList。** 中に[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/display/driverentry-of-video-miniport-driver)で返されたまたは、 *LegacyResourceList*パラメーターの[ *HwVidLegacyResources*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_legacyresources)します。

 

 





