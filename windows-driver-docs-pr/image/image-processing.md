---
title: 画像処理
description: 画像処理
ms.assetid: 84e10fcc-3998-434c-922a-65b42dccbdaf
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c2e7a95b973a97bc44c3149209188e4d25216072
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335445"
---
# <a name="image-processing"></a>画像処理





特定のスキャナーのミニドライバーでいくつかミニドライバーでは、画像処理レイヤーが必要です。 このレイヤーは、静止画像デバイスから取得したデータには、アプリケーション渡される前にいくつかの操作が必要な場合にのみ必須です。

さらに処理、デバイスから取得した生データが不要、画像処理レイヤーを省略できます。

Microsoft は、任意の画像の操作が必要な場合、WIA ミニドライバーで GDI + の使用をお勧めします。

### <a name="using-gdi-in-a-wia-driver"></a>WIA ドライバーで GDI + の使用

GDI +、2 次元のイメージ操作ルーチンを提供するライブラリです。 ライブラリでは、イメージの属性の変更の回転やサイズ変更に加えてメカニズムを提供します。

WIA ミニドライバーで GDI + を使用するには、GDI + が正しく初期化されていることを確認してください。 WIA ミニドライバーが作成され、読み込まれたときに、GDI + を初期化できます。 また、WIA ドライバーが含まれることを必ず*Gdiplus.h*へのリンク、 *Gdiplus.lib*ライブラリ。

GDI + の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

 

 




