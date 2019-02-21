---
title: Miracast ターゲット DisplayConfig 関数の呼び出し
ms.assetid: D408986B-B33B-4A96-B93C-2A2F301E74AF
description: Miracast ターゲット DisplayConfig 関数の呼び出し
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 252ce447878a3d2742ee25954b90c33052f1c124
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556607"
---
# <a name="calling-displayconfig-functions-for-a-miracast-target"></a>Miracast ターゲット DisplayConfig 関数の呼び出し


新しい Miracast ターゲットに公開されている既存のアプリの互換性の問題を軽減する、 [ **QueryDisplayConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff569215)と[ **SetDisplayConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff569533)関数の実装に向け Miracast ターゲットを検出する方法があります。

-   値**DISPLAYCONFIG\_出力\_テクノロジ\_MIRACAST**で、 [ **DISPLAYCONFIG\_ビデオ\_出力\_テクノロジ**](https://msdn.microsoft.com/library/windows/hardware/ff554003)列挙型の場合、VidPN ターゲットが Miracast デバイスであることを示します。
-   Flags パラメーター値の**QDC\_すべて\_パス**への呼び出しで[ **QueryDisplayConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff569215) Miracast に接続するすべてのパスが返されませんアクティブなモニターが接続されていないターゲット。
-   Miracast モニターを接続するには、各パスに対する[ **QueryDisplayConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff569215) Miracast シンクによって報告されるコネクタの種類を返します。 内部 Miracast シンクの値をレポートする**DISPLAYCONFIG\_出力\_テクノロジ\_MIRACAST**で、 [ **DISPLAYCONFIG\_ビデオ\_出力\_テクノロジ**](https://msdn.microsoft.com/library/windows/hardware/ff554003)列挙体。 たとえば、Miracast シンクがテレビが高品位のマルチ メディア インターフェイス (HDMI) ケーブルでシンクにし、接続されていることを報告**QueryDisplayConfig**とターゲットの種類を報告**DISPLAYCONFIG\_出力\_テクノロジ\_HDMI**します。
-   [ **DISPLAYCONFIG\_ビデオ\_信号\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff554007)構造体の垂直同期頻度の区切りメンバーが**vSyncFreqDivider**と同様に使用される[ **D3DKMDT\_ビデオ\_信号\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff546625).**vSyncFreqDivider**します。
-   [ **DisplayConfigGetDeviceInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff553903)関数は、任意のターゲットのコネクタの基本型を提供します。 Miracast ターゲットでは、場合常に値を返しますの**DISPLAYCONFIG\_出力\_テクノロジ\_MIRACAST**で、 [ **DISPLAYCONFIG\_ビデオ\_出力\_テクノロジ**](https://msdn.microsoft.com/library/windows/hardware/ff554003)列挙体。

 

 





