---
title: 複数ヘッド ビデオ メモリのレポート
description: 複数ヘッド ビデオ メモリのレポート
ms.assetid: 664b60f5-9e19-4dfc-8bd7-73ceccf6cbea
keywords:
- 複数ヘッド ハードウェア WDK DirectX 9.0 では、メモリ レポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e544560c0e354dd074956ef1c8d905bc5b102306
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573255"
---
# <a name="reporting-multiple-head-video-memory"></a>複数ヘッド ビデオ メモリのレポート


## <span id="ddk_reporting_multiple_head_video_memory_gg"></span><span id="DDK_REPORTING_MULTIPLE_HEAD_VIDEO_MEMORY_GG"></span>


ドライバーへの呼び出しに応答する必要があります複数ヘッド モードでは、master head [ *DdGetAvailDriverMemory* ](https://msdn.microsoft.com/library/windows/hardware/ff549377) master head が複数ヘッドのカードを制御するだけのヘッドであるかのように機能します。 ドライバーが返す空きメモリの量は、ビデオ メモリは、master head を降伏したが、下位の頭のビデオ メモリを含める必要があります (つまり、受信したヘッド従属*DdCreateSurface*での呼び出し、DDSCAPS2\_ADDITIONALPRIMARY ビットが設定)。

 

 





