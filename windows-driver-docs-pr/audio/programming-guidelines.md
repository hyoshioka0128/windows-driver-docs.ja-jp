---
title: HD オーディオ DDI のプログラミング ガイドライン
description: HD オーディオ DDI のプログラミング ガイドライン
ms.assetid: 289bdf85-9138-4920-a61f-050c51077d3e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4827dded98bcab494efc207e4174eaef46af9a1c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832445"
---
# <a name="hd-audio-ddi-programming-guidelines"></a>HD オーディオ DDI のプログラミング ガイドライン


このセクションでは、HD Audio DDI バージョンを使用するためのプログラミングガイドラインを示します ( [**hdaudio\_bus\_interface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface)、 [**HDAUDIO\_BUS\_INTERFACE\_V2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface_v2)および[**hdaudio\_BUS によって定義されて\_インターフェイス\_BDL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface_bdl)構造体) を、HD オーディオバスインターフェイスコントローラーに接続されているオーディオおよびモデムコーデックを制御します。

HD オーディオバスドライバーは、HD オーディオ DDI の一方または両方のバージョンをその子に公開します。これは、オーディオおよびモデムコーデックのカーネルモード関数ドライバーです。 (これらの子の1つは、UAA HD オーディオクラスドライバーである可能性があります)。これらのドライバーは、HD オーディオコントローラーデバイスのハードウェア機能にアクセスするために、DDIs のルーチンを呼び出します。

このセクションの内容:

[HD audio DDI のバージョン間の相違点](differences-between-the-hd-audio-ddi-versions.md)

[同期および非同期のコーデックコマンド](synchronous-and-asynchronous-codec-commands.md)

[ウォールクロックとリンク位置のレジスタ](wall-clock-and-link-position-registers.md)

[ハードウェアリソースの管理](hardware-resource-management.md)

[2つ以上のストリームの同期](synchronizing-two-or-more-streams.md)

[ウェイク有効化](wake-enable.md)

[データのコピーとキャッシュのポリシー](data-copying-and-caching-policy.md)

[HD audio DDI のクエリ](querying-for-an-hd-audio-ddi.md)

 

 




