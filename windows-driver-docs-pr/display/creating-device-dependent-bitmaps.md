---
title: デバイス依存ビットマップの作成
description: デバイス依存ビットマップの作成
ms.assetid: da53a8bf-5991-4abb-81f1-2d3a7cb0ff90
keywords:
- ビットマップ、GDI WDK Windows 2000 の表示
- ビットマップ グラフィックス ドライバー WDK Windows 2000 の表示
- WDK GDI、ビットマップの描画
- WDK GDI ビットマップ
- デバイスに固有のビットマップ WDK GDI
- DDB WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 42e2f6dec985d51533ef7e0bfe37698bcb4de7a0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387249"
---
# <a name="creating-device-dependent-bitmaps"></a>デバイス依存ビットマップの作成


## <span id="ddk_creating_device_dependent_bitmaps_gg"></span><span id="DDK_CREATING_DEVICE_DEPENDENT_BITMAPS_GG"></span>

ドライバーの作成し、管理、アプリケーションがビットマップの作成を要求すると、 [ *DDB* ](https://docs.microsoft.com/windows/desktop/gdi/device-dependent-bitmaps)サポートすることによって、 [ **DrvCreateDeviceBitmap** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvcreatedevicebitmap)関数。 このようなドライバーは、ビットマップを作成するときは、任意の形式で、ビットマップを格納できます。 ドライバーは、渡されたパラメーターを調べ、少なくとも数だけビット ピクセルあたりの要求にビットマップを提供します。

> [!NOTE]
> グラフィック ドライバーは、のビットマップをサポートすることでパフォーマンスを向上させることができます[*オフスクリーン メモリ*](video-present-network-terminology.md#off_screen_memory)してハードウェアを使用してビットマップを描画します。 これの例は、次を参照してください。、 **Permedia**ドライバーのサンプルを表示します。


> [!NOTE]
> Microsoft Windows Driver Kit (WDK) に 3 dlabs permedia2 チップが含まれていません (*3dlabs.htm*) と 3 dlabs Permedia3 (*Perm3.htm*) ディスプレイ ドライバーのサンプルです。 これらのサンプル ドライバーから、Windows Server 2003 SP1 ドライバー開発キット (DDK)、DDK - WDHC web サイトの Windows ドライバー開発キットのページからダウンロード可能を取得できます。

内で**DrvCreateDeviceBitmap**、ドライバーは、GDI サービスを呼び出して[ **EngCreateDeviceBitmap** ](https://msdn.microsoft.com/library/windows/hardware/ff564204) GDI のデバイスのビットマップのハンドルを作成します。

ドライバーがサポートしている場合**DrvCreateDeviceBitmap**、DDB を作成します。、、その書式を定義し、ハンドルを返します。 ドライバーは、ビットマップが格納されている場所とどのような形式を制御します。 ドライバーは、そのデバイスの画面に最も密接に一致する色の書式をサポートする必要があります。

ビットマップの内容は作成後は未定義です。 ドライバーを返す場合**NULL**GDI がこれらのタスクを実行する代わりに、; の作成し、ビットマップを管理しません。

ドライバーは、ビットマップを作成する場合にできる必要がありますも実装することでそれらを削除する、 [ **DrvDeleteDeviceBitmap** ](https://msdn.microsoft.com/library/windows/hardware/ff556187)関数。

 

 





