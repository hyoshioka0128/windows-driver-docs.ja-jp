---
title: ドライバー管理対象テクスチャの喪失
description: ドライバー管理対象テクスチャの喪失
ms.assetid: 19f87190-bb3a-40a6-a216-8df9816e2842
keywords:
- WDK DirectDraw、失われたテクスチャの描画サーフェス
- DirectDraw サーフェスのテクスチャの紛失、WDK の Windows 2000 の表示
- サーフェスの WDK DirectDraw、テクスチャの紛失
- 中断されたテクスチャ WDK DirectDraw
- テクスチャ WDK DirectDraw、失われました。
- 失われたテクスチャ WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c259e7653857b50c585e68ce2919f2024822002
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384844"
---
# <a name="losing-driver-managed-textures"></a>ドライバー管理対象テクスチャの喪失


## <span id="ddk_losing_driver_managed_textures_gg"></span><span id="DDK_LOSING_DRIVER_MANAGED_TEXTURES_GG"></span>


ドライバー管理のテクスチャ サーフェスは、ビデオ メモリを消費するには、中断状態 (失わ) に配置する機能が必要です。 メソッドのドライバーは、このようなテクスチャ サーフェスの拡張機能で失われる必要がある場合に通知、ドライバーはドライバー管理のテクスチャ サーフェスのビデオ メモリの割り当てを制御するため、 [ *DdDestroySurface*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_destroysurface)呼び出します。

ときにドライバー管理のテクスチャ サーフェス (、DDSCAPS2 でマークされた\_TEXTUREMANAGE フラグ) が失われると、ドライバーが、特殊な受信*DdDestroySurface* DDRAWISURF で呼び出す\_で指定された無効な**dwFlags**テクスチャ サーフェス構造体のメンバー。 ドライバーは、管理対象のテクスチャのサーフェイスに関連付けられているビデオ メモリを解放する必要がありますが、その他のプライベート サーフェス情報など、画面のビデオ メモリのコピーのバックアップ (システム メモリ) のイメージを解放する必要があります。 新しいされます[ *DdCreateSurface* ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549263(v=vs.85))呼び出しが、ドライバーの観点から本当に失われないので失わドライバー管理のテクスチャ サーフェスを復元します。 ほとんどの場合、この特殊*DdDestroySurface*ビデオ メモリのコピーを削除する必要がありますが、ドライバーに通知するために呼び出しを使用します。

 

 





