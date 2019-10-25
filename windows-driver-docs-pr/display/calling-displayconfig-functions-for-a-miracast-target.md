---
title: Miracast ターゲットの DisplayConfig 関数の呼び出し
ms.assetid: D408986B-B33B-4A96-B93C-2A2F301E74AF
description: Miracast ターゲットの DisplayConfig 関数の呼び出し
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 495773c6d9da6ddb1cf63314a3755719a4b16cfc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839062"
---
# <a name="calling-displayconfig-functions-for-a-miracast-target"></a>Miracast ターゲットの DisplayConfig 関数の呼び出し


新しい Miracast ターゲットに公開されている既存のアプリの互換性の問題を減らすために、 [**querydisplayconfig**](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-querydisplayconfig)関数と[**setdisplayconfig**](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-setdisplayconfig)関数の実装には、アプリで miracast ターゲットを検索する方法があります。

-   Displayconfig **\_出力\_\_テクノロジ**の値[**DISPLAYCONFIG\_VIDEO\_出力\_テクノロジ**](https://docs.microsoft.com/windows/desktop/api/wingdi/ne-wingdi-displayconfig_video_output_technology)の列挙は、VidPN ターゲットが MIRACAST デバイスであることを示します。
-   Qdc の Flags パラメーター値は、 [**Querydisplayconfig**](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-querydisplayconfig)の呼び出しの**すべての\_パス\_** 、アクティブなモニターが接続されていない Miracast ターゲットに接続するパスを返しません。
-   接続されている Miracast モニターがあるパスごとに、 [**Querydisplayconfig**](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-querydisplayconfig)は miracast シンクによって報告されたコネクタの種類を返します。 内部 Miracast シンクは**displayconfig\_出力\_\_テクノロジ**の値を[**DISPLAYCONFIG\_VIDEO\_の出力\_テクノロジ**](https://docs.microsoft.com/windows/desktop/api/wingdi/ne-wingdi-displayconfig_video_output_technology)列挙に記録します。 たとえば、Miracast シンクが、テレビが高解像度のマルチメディアインターフェイス (HDMI) ケーブルでシンクに接続されていることを報告した場合、 **Querydisplayconfig**はターゲットの種類を**DISPLAYCONFIG\_出力\_テクノロジとして報告し @no__t4_ HDMI (_s)** \_
-   [**Displayconfig\_video\_signal\_info**](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-displayconfig_video_signal_info)構造体には、 [**D3DKMDT\_VIDEO\_signal\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_video_signal_info)と同様に使用される、垂直の周波数区分線メンバー **vsyncfreqdivider**があります。**Vsyncfreqdivider**。
-   [**DisplayConfigGetDeviceInfo**](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-displayconfiggetdeviceinfo)関数は、任意のターゲットのベースコネクタの種類を提供します。 Miracast ターゲットの場合、この関数は常に displayconfig [ **\_VIDEO\_\_の出力テクノロジ**](https://docs.microsoft.com/windows/desktop/api/wingdi/ne-wingdi-displayconfig_video_output_technology)の列挙で **\_テクノロジ\_Miracast\_** の値を返します。

 

 





