---
title: Miracast ターゲットに対する DisplayConfig 関数の呼び出し
ms.assetid: D408986B-B33B-4A96-B93C-2A2F301E74AF
description: Miracast ターゲットに対する DisplayConfig 関数の呼び出し
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e56aa2352a7f8d6a64208b8af4c5866a40d8c8e0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384605"
---
# <a name="calling-displayconfig-functions-for-a-miracast-target"></a>Miracast ターゲットに対する DisplayConfig 関数の呼び出し


新しい Miracast ターゲットに公開されている既存のアプリの互換性の問題を軽減する、 [ **QueryDisplayConfig** ](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-querydisplayconfig)と[ **SetDisplayConfig** ](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-setdisplayconfig)関数の実装に向け Miracast ターゲットを検出する方法があります。

-   値**DISPLAYCONFIG\_出力\_テクノロジ\_MIRACAST**で、 [ **DISPLAYCONFIG\_ビデオ\_出力\_テクノロジ**](https://docs.microsoft.com/windows/desktop/api/wingdi/ne-wingdi-displayconfig_video_output_technology)列挙型の場合、VidPN ターゲットが Miracast デバイスであることを示します。
-   Flags パラメーター値の**QDC\_すべて\_パス**への呼び出しで[ **QueryDisplayConfig** ](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-querydisplayconfig) Miracast に接続するすべてのパスが返されませんアクティブなモニターが接続されていないターゲット。
-   Miracast モニターを接続するには、各パスに対する[ **QueryDisplayConfig** ](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-querydisplayconfig) Miracast シンクによって報告されるコネクタの種類を返します。 内部 Miracast シンクの値をレポートする**DISPLAYCONFIG\_出力\_テクノロジ\_MIRACAST**で、 [ **DISPLAYCONFIG\_ビデオ\_出力\_テクノロジ**](https://docs.microsoft.com/windows/desktop/api/wingdi/ne-wingdi-displayconfig_video_output_technology)列挙体。 たとえば、Miracast シンクがテレビが高品位のマルチ メディア インターフェイス (HDMI) ケーブルでシンクにし、接続されていることを報告**QueryDisplayConfig**とターゲットの種類を報告**DISPLAYCONFIG\_出力\_テクノロジ\_HDMI**します。
-   [ **DISPLAYCONFIG\_ビデオ\_信号\_情報**](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-displayconfig_video_signal_info)構造体の垂直同期頻度の区切りメンバーが**vSyncFreqDivider**と同様に使用される[ **D3DKMDT\_ビデオ\_信号\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_d3dkmdt_video_signal_info).**vSyncFreqDivider**します。
-   [ **DisplayConfigGetDeviceInfo** ](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-displayconfiggetdeviceinfo)関数は、任意のターゲットのコネクタの基本型を提供します。 Miracast ターゲットでは、場合常に値を返しますの**DISPLAYCONFIG\_出力\_テクノロジ\_MIRACAST**で、 [ **DISPLAYCONFIG\_ビデオ\_出力\_テクノロジ**](https://docs.microsoft.com/windows/desktop/api/wingdi/ne-wingdi-displayconfig_video_output_technology)列挙体。

 

 





