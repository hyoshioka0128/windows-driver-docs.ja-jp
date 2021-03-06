---
title: ビデオ ミニポート ドライバーのヘッダー ファイル (Windows 2000 モデル)
description: ビデオ ミニポート ドライバーのヘッダー ファイル (Windows 2000 モデル)
ms.assetid: 7ce0df41-ce1e-4d76-b7e8-6d0a3576a58d
keywords:
- ビデオのミニポート ドライバー WDK Windows 2000 では、ヘッダー ファイル
- ヘッダー ファイル WDK のビデオのミニポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bee47274052bf2578c58c7f7ccfcae265916e802
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376126"
---
# <a name="video-miniport-driver-header-files-windows-2000-model"></a>ビデオ ミニポート ドライバーのヘッダー ファイル (Windows 2000 モデル)


## <span id="ddk_video_miniport_driver_header_files_windows_2000_model__gg"></span><span id="DDK_VIDEO_MINIPORT_DRIVER_HEADER_FILES_WINDOWS_2000_MODEL__GG"></span>


Windows 2000 のディスプレイ ドライバー モデル内のビデオのミニポート ドライバーでは、次のヘッダー ファイルを含めます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ファイル名</th>
<th align="left">目次</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><em>dderror.h</em></p></td>
<td align="left"><p>ミニポート ドライバーの対応するカーネル モードにも返されますが、ビデオ ポート ドライバーに戻るミニポート ドライバーがドライバーを表示する Win32 状態定数が含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>devioctl.h</em></p></td>
<td align="left"><p>マクロと I/O 制御コードの定義に使用される定数が含まれています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>miniport.h</em></p></td>
<td align="left"><p>基本的な型、定数、およびビデオの構造が含まれています (と SCSI) のミニポート ドライバー。</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>ntddvdeo.h</em></p></td>
<td align="left"><p>システム定義の I/O 制御コード (Ioctl) を格納およびビデオ要求パケットで送信される対応する構造体 (<a href="https://docs.microsoft.com/windows-hardware/drivers/#wdkgloss-video-request-packet--vrp-" data-raw-source="&lt;em&gt;VRPs&lt;/em&gt;"><em>VRPs</em></a>) ビデオのミニポート ドライバー。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>tvout.h</em></p></td>
<td align="left"><p>含まれています、 <a href="https://docs.microsoft.com/windows/desktop/api/tvout/ns-tvout-_videoparameters" data-raw-source="[&lt;strong&gt;VIDEOPARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/tvout/ns-tvout-_videoparameters)"> <strong>VIDEOPARAMETERS</strong> </a>テレビ コネクタとコピー保護のサポートとこの構造体で使用される定数を実装するために使用される構造体。</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>video.h</em></p></td>
<td align="left"><p>含まれています、<strong>ビデオ ポート</strong><em>Xxx</em>と<em>SvgaHwIoPortXxx</em>ビデオ ポートにビデオに固有の構造体の宣言、機能など、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/ns-video-_video_request_packet" data-raw-source="[&lt;strong&gt;VIDEO_REQUEST_PACKET&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/ns-video-_video_request_packet)"> <strong>VIDEO_REQUEST_PACKET</strong></a>、および<em>HwVidXxx</em>ビデオのミニポート関数のプロトタイプ。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>videoagp.h</em></p></td>
<td align="left"><p>AGP に固有の構造体を含む<em>AgpXxx</em> 、ミニポート ドライバー関数プロトタイプと<strong>ビデオ ポート</strong><em>Xxx</em> AGP サポートを実装するために必要な宣言を関数ビデオのミニポート ドライバー。</p></td>
</tr>
</tbody>
</table>

 

これらのヘッダーは、Windows Driver Kit (WDK) に付属しています。 詳細については、関数、構造体、システム定義されている I/O 制御コード、およびこれらのヘッダー ファイル内の定数を参照してください。 [GDI 関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。

 

 





