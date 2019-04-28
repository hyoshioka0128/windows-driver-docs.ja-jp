---
title: GDI サービス ルーチン
description: GDI サービス ルーチン
ms.assetid: ca4fbb84-33a8-498f-8549-c8aaf87429fd
keywords:
- GDI WDK Windows 2000 の表示、サービス ルーチン
- グラフィックス ドライバー WDK Windows 2000 の表示、サービス ルーチン
- 描画 WDK GDI やサービス ルーチン
- サービス ルーチン WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b34b364e71ce14a20b06de2f7707141c80acd4a4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374635"
---
# <a name="gdi-service-routines"></a>GDI サービス ルーチン


## <span id="ddk_gdi_service_routines_gg"></span><span id="DDK_GDI_SERVICE_ROUTINES_GG"></span>


GDI は、名前を持つフォームがある多くのサービス ルーチンをエクスポートします。 **への Eng * * * Xxx*します。 ドライバーは、動的にリンク*win32k.sys*これらのルーチンに直接アクセスします。 GDI サービス ルーチンには、サーフェスの管理、レンダリングのシミュレーション、およびパス、パレット、フォント、およびテキスト サービスが含まれます。 これらのサービスでの詳細については[GDI サポート サービス](gdi-support-services.md)します。

 

 





