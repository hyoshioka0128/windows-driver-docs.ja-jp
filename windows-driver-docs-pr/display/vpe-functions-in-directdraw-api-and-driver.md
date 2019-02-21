---
title: DirectDraw API とドライバーの VPE 関数
description: DirectDraw API とドライバーの VPE 関数
ms.assetid: 7e899f20-4082-4438-b7f2-198d1a4ad344
keywords:
- DirectX VPE サポート WDK DirectDraw、関数
- 描画 VPEs WDK DirectDraw、関数
- DirectDraw VPEs WDK Windows 2000 の表示、関数
- ビデオ ポート WDK DirectDraw、関数の拡張機能
- VPEs WDK DirectDraw、関数
- WDK のビデオ ポートの拡張機能の関数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0963f17d65818f236dcb1ad3708ccad39e1946d4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553164"
---
# <a name="vpe-functions-in-directdraw-api-and-driver"></a>DirectDraw API とドライバーの VPE 関数


## <span id="ddk_vpe_functions_in_directdraw_api_and_driver_gg"></span><span id="DDK_VPE_FUNCTIONS_IN_DIRECTDRAW_API_AND_DRIVER_GG"></span>


DirectX の最新のリリースでのビデオ ポート拡張機能は、DirectDraw API への低レベルの拡張機能です。 VPE でビデオ ポートを MPEG または NTSC デコーダーとハードウェアの間の接続をネゴシエートするクライアント - 通常、DirectShow--にできます。 VPE では、クライアントはのトリミングおよびスケーリングなど、ビデオ ストリームの効果を制御することもできます。

VPE はアプリケーションで広範な使用するために設計された高レベルの API ではありません。 アプリケーションでは、VPE の無料のサポートを提供する、DirectShow を使用する必要があります。 次の図は、VPE とカーネル モードのアーキテクチャの単純なビューを示しています。 詳細については、次を参照してください。[カーネル モードのビデオ トランスポート](kernel-mode-video-transport.md)します。

![図に示すのビデオ ポートとカーネル モードの拡張機能アーキテクチャ](images/ddfig10.png)

上記の図は、DirectDraw アーキテクチャの他のコンポーネントとの関連 VPE を示しています。 DirectShow VPE を使用してデータと V 同期および H 同期情報を転送する方法についての情報を提供すると、接続をネゴシエートします。 この情報は、APIC 接続 (ITU 656)、外部データの明細行の追加の pin または Brooktree と Philips によって実装されるなどの独自のデータ ストリームを指定できます。

接続のネゴシエーション、VGA ハードウェアでは、どのような接続はサポートされることを示し、MPEG または NTSC デコーダーは、その設定を指定します。 DirectShow では、2 つの最適な接続をネゴシエートします。 接続は、二重のクロックとアクティブなビデオなどの他のパラメーターを記述するフラグをグローバル一意識別子 (GUID)、として記述されます。

 

 





