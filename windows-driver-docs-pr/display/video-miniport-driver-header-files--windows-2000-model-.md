---
title: ビデオ ミニポート ドライバーのヘッダー ファイル (Windows 2000 モデル)
description: ビデオ ミニポート ドライバーのヘッダー ファイル (Windows 2000 モデル)
ms.assetid: 7ce0df41-ce1e-4d76-b7e8-6d0a3576a58d
keywords:
- ビデオミニポートドライバー WDK Windows 2000、ヘッダーファイル
- ヘッダーファイル WDK ビデオミニポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 16154fde1ed109735040463c5c7cef216e7a3cce
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825290"
---
# <a name="video-miniport-driver-header-files-windows-2000-model"></a>ビデオ ミニポート ドライバーのヘッダー ファイル (Windows 2000 モデル)


## <span id="ddk_video_miniport_driver_header_files_windows_2000_model__gg"></span><span id="DDK_VIDEO_MINIPORT_DRIVER_HEADER_FILES_WINDOWS_2000_MODEL__GG"></span>


Windows 2000 display driver モデルのビデオミニポートドライバーには、次のヘッダーファイルが含まれています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ファイル名</th>
<th align="left">内容</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><em>dderror. h</em></p></td>
<td align="left"><p>ミニポートドライバーがビデオポートドライバーに返す Win32 状態定数を格納します。これは、対応するカーネルモード表示ドライバーにも返されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>devioctl</em></p></td>
<td align="left"><p>I/o 制御コードを定義するために使用されるマクロと定数が含まれています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>ミニポート .h</em></p></td>
<td align="left"><p>ビデオ (および SCSI) ミニポートドライバーの基本型、定数、および構造体が含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>ntddvdeo</em></p></td>
<td align="left"><p>ビデオミニポートドライバーにビデオ要求パケット (<a href="https://docs.microsoft.com/windows-hardware/drivers/#wdkgloss-video-request-packet--vrp-" data-raw-source="&lt;em&gt;VRPs&lt;/em&gt;"><em>Vrps</em></a>) で送信されるシステム定義の i/o 制御コード (ioctl) とそれに対応する構造体を含みます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>tvout</em></p></td>
<td align="left"><p>テレビコネクタおよびコピー防止サポートと、この構造体で使用される定数を実装するために使用される<a href="https://docs.microsoft.com/windows/desktop/api/tvout/ns-tvout-_videoparameters" data-raw-source="[&lt;strong&gt;VIDEOPARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/tvout/ns-tvout-_videoparameters)"><strong>VIDEOPARAMETERS</strong></a>構造体が含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>ビデオ. h</em></p></td>
<td align="left"><p><strong>VideoPort</strong><em>Xxx</em>および<em>Svガス hwioportxxx</em>ビデオポート関数の宣言、ビデオ固有の構造 ( <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_video_request_packet" data-raw-source="[&lt;strong&gt;VIDEO_REQUEST_PACKET&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_video_request_packet)"><strong>VIDEO_REQUEST_PACKET</strong></a>など)、および<em>HwVidXxx</em>ビデオミニポート関数プロトタイプが含まれています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>videoagp</em></p></td>
<td align="left"><p>ビデオミニポートドライバーで AGP サポートを実装するために必要な、AGP 固有の構造体、 <em>Agpxxx</em>ミニポートドライバー関数プロトタイプ、および<strong>VideoPort</strong><em>Xxx</em>関数の宣言が含まれています。</p></td>
</tr>
</tbody>
</table>

 

これらのヘッダーには、Windows Driver Kit (WDK) が付属しています。 これらのヘッダーファイルの関数、構造体、システム定義 i/o 制御コード、および定数の詳細については、「 [GDI 関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」を参照してください。

 

 





