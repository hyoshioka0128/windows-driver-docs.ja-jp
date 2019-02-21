---
title: Windows 2000 のビデオのミニポート ドライバー責任
description: Windows 2000 のビデオのミニポート ドライバー責任
ms.assetid: 55301260-af1b-4ef7-8f33-e0acbeb22039
keywords:
- ドライバー モデル WDK Windows 2000 では、責任を表示します。
- Windows 2000 のディスプレイ ドライバー モデル WDK、責任
- ビデオのミニポート ドライバー WDK Windows 2000 では、責任
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1bd067752ea118b5e99968f6e52819f99ac66e6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552160"
---
# <a name="windows-2000-video-miniport-driver-responsibilities"></a>Windows 2000 のビデオのミニポート ドライバー責任


## <span id="ddk_video_miniport_driver_responsibilities_gg"></span><span id="DDK_VIDEO_MINIPORT_DRIVER_RESPONSIBILITIES_GG"></span>


カーネル モード*ビデオのミニポート ドライバー* (.sys ファイル) は一般に他の NT カーネル コンポーネントとやり取りする必要がありますを操作を処理します。 たとえば、ハードウェアの初期化とメモリ マッピングなどの操作では、NT I/O サブシステムによってアクションが必要です。 ビデオのミニポート ドライバーの業務には、ハードウェア構成では、物理デバイスのメモリ マッピングなどのリソース管理が含まれます。 ビデオのミニポート ドライバーは、ビデオ ハードウェアに固有である必要があります。

ディスプレイ ドライバーが頻繁に要求されない; 操作のビデオのミニポート ドライバーを使用します。たとえば、リソースを管理する物理デバイスのメモリ マッピングを実行、出力が近接、発生するか、割り込みに応答に登録することを確認します。

**注**  ビデオのミニポート ドライバーは、すべてのリソース (メモリ リソースなど) のビデオのミニポート ドライバーと、ディスプレイ ドライバー間で共有を管理する必要があります。 システムでは、ディスプレイ ドライバーで取得したリソースがビデオのミニポート ドライバーにアクセス可能な常にすることは保証されません。

 

ビデオのミニポート ドライバーも処理されます。

-   モードでは、グラフィックス カードとの対話を設定します。

-   複数のハードウェアの種類、ディスプレイ ドライバーのハードウェアの種類の依存関係を最小限に抑えることです。

-   ビデオ ディスプレイ ドライバーのアドレス空間に登録をマッピングします。 I/O ポートは、直接アドレス指定可能です。

詳細については、ビデオのミニポート ドライバー [Windows 2000 Display Driver Model でのビデオのミニポート ドライバー](video-miniport-drivers-in-the-windows-2000-display-driver-model.md)します。

 

 





