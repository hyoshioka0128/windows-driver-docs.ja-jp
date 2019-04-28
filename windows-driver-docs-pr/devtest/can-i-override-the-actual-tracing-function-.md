---
title: 実際のトレース機能をオーバーライドできます。
description: 実際のトレース機能をオーバーライドできます。
ms.assetid: 215e6fb6-a1f4-4188-a3aa-9688ce17d04b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b0ea70b656d77ed08456cc59556b184210071968
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364724"
---
# <a name="can-i-override-the-actual-tracing-function"></a>実際のトレース関数をオーバーライドできますか?


[はい]。 カスタム WPP を定義することでこれを行う\_TRACE マクロ。 インクルードする前に、このマクロのバージョンを定義する必要があります、[トレース メッセージのヘッダー (.tmh) ファイル](trace-message-header-file.md)のソース ファイルで、[トレース プロバイダー](trace-provider.md)、カーネル モード ドライバーまたはユーザー モード アプリケーションなどです。

カスタム WPP を定義する方法の例については\_マクロのトレースを参照してください[は保持できます直前のエラー コード TraceMessage が呼び出される前にしますか?](can-i-preserve-the-last-error-code-before-tracemessage-is-called-.md)します。

 

 





