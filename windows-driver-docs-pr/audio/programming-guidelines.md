---
title: HD audio DDI プログラミングガイドライン
description: HD audio DDI プログラミングガイドライン
ms.assetid: 289bdf85-9138-4920-a61f-050c51077d3e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3af7de6291f0a7a6f669bc321b508e637c442ec2
ms.sourcegitcommit: 8295a2b59212972b0f7457a748cc904b5417ad67
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71319914"
---
# <a name="hd-audio-ddi-programming-guidelines"></a>HD audio DDI プログラミングガイドライン


このセクションでは、HD オーディオ DDI バージョンを使用するためのプログラミングガイドラインを示します ( [ **\_hdaudio bus\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface)、 [**hdaudio\_bus\_interface\_V2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface_v2) 、[**Hdaudio\_businterface\_bdl 構造体) を使って、HD オーディオバスインターフェイスコントローラーに接続されているオーディオおよびモデムコーデックを制御します。\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface_bdl)

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

 

 




