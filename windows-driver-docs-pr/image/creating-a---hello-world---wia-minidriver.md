---
title: "\"Hello World\"WIA のミニドライバーを作成します。"
description: "\"Hello World\"WIA のミニドライバーを作成します。"
ms.assetid: 074da2ff-bc60-48a9-b2ff-83f070bd5351
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: caccf6323e26f54f18298efe760928a48680b337
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386324"
---
# <a name="creating-a-hello-world-wia-minidriver"></a>"Hello World"WIA のミニドライバーを作成します。





この WIA ミニドライバーは、2 つの関数をエクスポートし、次の 3 つの COM インターフェイスを実装する単純な DLL です。 次のコード例は、作業の WIA ミニドライバーにコンパイルできます。 この WIA ミニドライバーを作成する項目のツリーのルート項目のみがあるし、データを転送することはできませんが、読み込まれ、実行は、WIA ドライバーを入手するために必要な基礎を示しています。

次のファイルを使用して、"Hello World"の WIA ミニドライバーを作成します。

*hellowld.def* −、[定義ファイルの 'Hello World'](--hello-world---definition-file.md)します。

*hellowld.inf* −、[インストール ファイルの 'Hello World'](--hello-world---installation-file.md)します。

*hellowld.cpp* −、[実装ファイルの 'Hello World'](--hello-world---implementation-file.md)します。

ミニドライバーは、カスタム UI を追加する方法についてを参照してください。 ["Hello World"WIA ミニドライバー UI 拡張機能の作成](creating-a--hello-world--wia-minidriver-ui-extension.md)です。

 

 




