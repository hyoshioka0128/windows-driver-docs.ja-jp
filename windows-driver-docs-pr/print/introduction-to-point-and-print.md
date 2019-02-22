---
title: ポイント アンド プリントの概要
description: ポイント アンド プリントの概要
ms.assetid: 03902c64-29d7-4b59-a604-e282e4a2c7ae
keywords:
- ポイント アンド プリントの詳細について、ポイント アンド プリントの WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5dbaa132da1483597b243d48302339732ac2c5fa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549583"
---
# <a name="introduction-to-point-and-print"></a>ポイント アンド プリントの概要





*ポイント アンド プリント*は Windows 2000 以降のクライアントでユーザーのディスクまたはその他のインストール メディアを指定せず、リモート プリンターへの接続を作成する機能を表す用語です。 すべての必要なファイルと構成情報は、クライアントにプリント サーバーから自動的にダウンロードします。

ポイント アンド プリントのテクノロジは、プリント サーバーからクライアント コンピューターに送信する必要がありますファイルを指定できます 2 つのメソッドを提供します。

-   ファイルは、プリンター ドライバーを関連付けることができます。 これらのファイルは、ドライバーを使用するすべての印刷キューに関連付けられます。

-   ファイルは、個々 の印刷キューを関連付けることができます。

詳細については、次を参照してください。[サポート ポイントとプリンターのインストール中に印刷](supporting-point-and-print-during-printer-installations.md)します。

ユーザーのアプリケーションを呼び出すと、 **AddPrinterConnection**関数 (Microsoft Windows SDK のドキュメントで説明) プリンター接続を確立するには、次の操作が実行されます。

-   ドライバーに関連付けられているし、キューに関連付けられているファイルは、プリント サーバーからクライアントにダウンロードされます。

-   プリンターのキーの下で、サーバーのレジストリに保存されている、プリンターの構成パラメーターの現在の値は、クライアントにダウンロードされます。

詳細については、次を参照してください。[サポート ポイント アンド プリントの実装中にプリンター接続](supporting-point-and-print-during-printer-connections.md)します。

 

 




