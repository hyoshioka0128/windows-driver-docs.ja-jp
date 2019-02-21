---
title: ドライバー固有のファイルのダウンロード
description: ドライバー固有のファイルのダウンロード
ms.assetid: 7ac5057a-32fb-4c3a-a5c3-3fc1217dbdc6
keywords:
- ポイント アンド プリントの WDK、ドライバー固有のファイル
- WDK プリンターのドライバー固有のファイル
- プリンターのドライバー固有のファイルのダウンロード
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e7f3d7547808e0af7b06a1b297561f796f0fcc92
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538827"
---
# <a name="downloading-driver-specific-files"></a>ドライバー固有のファイルのダウンロード





クライアント システムを呼び出すことによって、プリント サーバーへの接続を作成します**AddPrinterConnection**します。 この呼び出しの結果への呼び出しで**GetPrinterDriver**が読み取られ、サーバーで、[プリンターの INF ファイル](printer-inf-files.md)ドライバーを設定するため\_情報\_への呼び出し後に、3 つの構造**AddPrinterDriver**、ドライバーを使用した\_情報\_入力として 3 つの構造体。 **AddPrinterDriver**関数により、ドライバーで示されているすべてのファイル\_情報\_クライアントに送信する 3 つの構造体。

これらの関数とドライバー\_情報\_3 構造が、Microsoft Windows SDK ドキュメントに記載されています。

 

 




