---
title: プログラミング ガイド
description: プログラミング ガイド
ms.assetid: 289bdf85-9138-4920-a61f-050c51077d3e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a3a9803c7f335985abe3baa2929a17d1e9d02a4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572848"
---
# <a name="programming-guidelines"></a>プログラミング ガイド


このセクションでは、HD オーディオ DDI バージョンを使用するためのプログラミング ガイドラインを示します (で定義されている、 [ **HDAUDIO\_BUS\_インターフェイス**](https://msdn.microsoft.com/library/windows/hardware/ff536413)、 [ **HDAUDIO\_BUS\_インターフェイス\_V2** ](https://msdn.microsoft.com/library/windows/hardware/ff536418)と[ **HDAUDIO\_BUS\_インターフェイス\_BDL**](https://msdn.microsoft.com/library/windows/hardware/ff536416)構造) にコントロールのオーディオおよびモデム コーデック HD オーディオ バス インターフェイス コント ローラーに接続されています。

HD オーディオ バス ドライバーでは、その子では、カーネル モード関数ドライバー、オーディオとモデムのコーデックを HD オーディオ DDI の一方または両方のバージョンを公開します。 (UAA HD オーディオ クラス ドライバーはこれらの子のいずれかの可能性があります)。これらのドライバーでは、コント ローラーの HD オーディオ デバイスのハードウェア機能にアクセスする Ddi でルーチンを呼び出します。

このセクションの内容:

[HD オーディオ DDI バージョン間の違い](differences-between-the-hd-audio-ddi-versions.md)

[同期および非同期のコーデック コマンド](synchronous-and-asynchronous-codec-commands.md)

[実時間とリンク位置レジスタ](wall-clock-and-link-position-registers.md)

[ハードウェア リソースの管理](hardware-resource-management.md)

[2 つまたは複数のストリームの同期](synchronizing-two-or-more-streams.md)

[スリープ解除を有効にします。](wake-enable.md)

[データをコピーし、キャッシュ ポリシー](data-copying-and-caching-policy.md)

[HD オーディオ DDI のクエリを実行します。](querying-for-an-hd-audio-ddi.md)

 

 




