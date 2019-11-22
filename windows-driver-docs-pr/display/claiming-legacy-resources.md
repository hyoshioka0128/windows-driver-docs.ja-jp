---
title: レガシ リソースの要求
description: レガシ リソースの要求
ms.assetid: f3e573a1-0e7a-422b-8bed-db3ba7712a2f
keywords:
- ビデオミニポートドライバー WDK Windows 2000、レガシリソース
- レガシリソース WDK ビデオミニポート
- ビデオミニポートドライバー WDK Windows 2000、初期化
- ビデオミニポートドライバーの初期化
- VIDEO_HW_INITIALIZATION_DATA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 46f106d5ec972e4095db89b7bb1fa69fb42adc0f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839053"
---
# <a name="claiming-legacy-resources"></a>レガシ リソースの要求


## <span id="ddk_claiming_legacy_resources_gg"></span><span id="DDK_CLAIMING_LEGACY_RESOURCES_GG"></span>


ビデオミニポートドライバーは、ドライバーの初期化中に、 [**video\_HW\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_video_hw_initialization_data)構造内のすべてのレガシリソースを要求して報告する必要があります。 レガシリソースとは、デバイスの PCI 構成領域に記載されていないが、デバイスによってデコードされるリソースのことです。 NT ベースのオペレーティングシステムは、このセクションで説明されている方法で報告されていないレガシリソースが検出されたときに、電源管理とドッキングを無効にします。

ミニポートドライバーは、このようなレガシリソースを報告するために次の操作を行う必要があります。

- デバイスのレガシリソースリストがコンパイル時に認識されている場合は、 [**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/display/driverentry-of-video-miniport-driver)ルーチンで作成および初期化される[**ビデオ\_HW\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_video_hw_initialization_data)構造の次の2つのフィールドを入力します。

  <table>
  <colgroup>
  <col width="50%" />
  <col width="50%" />
  </colgroup>
  <thead>
  <tr class="header">
  <th align="left">構造体メンバー</th>
  <th align="left">定義</th>
  </tr>
  </thead>
  <tbody>
  <tr class="odd">
  <td align="left"><p><strong>HwLegacyResourceList</strong></p></td>
  <td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_video_access_range" data-raw-source="[&lt;strong&gt;VIDEO_ACCESS_RANGE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_video_access_range)"><strong>VIDEO_ACCESS_RANGE</strong></a>構造体の配列を指します。 各構造体には、PCI 構成領域に一覧表示されていないビデオアダプターのデバイス i/o ポートまたはメモリ範囲が記述されています。</p></td>
  </tr>
  <tr class="even">
  <td align="left"><p><strong>HwLegacyResourceCount</strong></p></td>
  <td align="left"><p><strong>HwLegacyResourceList</strong>が指す配列内の要素の数を指定します。</p></td>
  </tr>
  </tbody>
  </table>

     

<!-- -->

-   デバイスのレガシリソースリストがコンパイル時にわからない場合は、 [*HwVidLegacyResources*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_legacyresources)関数を実装し、VIDEO\_HW\_初期化\_データの**HwGetLegacyResources**メンバーを初期化して、これをポイントします。プロシージャ. たとえば、レガシリソースのセットが異なる2つのデバイスをサポートするミニポートドライバーは、実行時にレガシリソースを報告する*HwVidLegacyResources*を実装します。 ミニポートドライバーが*HwVidLegacyResources*を実装している場合、ビデオ\_HW\_初期化\_データの**HwLegacyResourceList**メンバーと**HwLegacyResourceCount**メンバーは、ビデオポートドライバーによって無視されます。

-   必要に応じて、ミニポートドライバーに定義されている各ビデオ\_アクセス\_範囲の構造に、 **Rangepassive**フィールドを入力します。 **Rangepassive**を VIDEO\_RANGE\_パッシブ\_デコードに設定すると、領域はハードウェアによってデコードされますが、ディスプレイおよびビデオミニポートドライバーがタッチすることはありません。 **Rangepassive**を VIDEO\_RANGE\_10\_ビット\_デコードに設定すると、デバイスがリージョンのポートアドレスの10ビットをデコードすることになります。

ここでも、ドライバーにはハードウェアがデコードするだけで、PCI によって要求されないリソースのみを含める必要があります。 最小限のレガシリソースを要求する必要があるドライバーのコードは、次のようになります。

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

ミニポートドライバーは、以降の呼び出しで従来のリソースを再利用して、 [**Videoportverifyaccessranges**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportverifyaccessranges); に再利用することができます。ただし、ビデオポートドライバーは、以前に要求されたリソースの要求を無視するだけです。 [**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/display/driverentry-of-video-miniport-driver)中に**HwLegacyResourceList**で以前に要求されていなかった、または[*HwVidLegacyResources*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_legacyresources)の*LegacyResourceList*パラメーターで返された**videoportverifyaccessranges**の従来のアクセス範囲をミニポートドライバーが要求しようとすると、システムで電源管理とドッキングが無効になります。

 

 





