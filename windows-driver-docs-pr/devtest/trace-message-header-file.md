---
title: トレース メッセージ ヘッダー ファイル
description: トレース メッセージ ヘッダー ファイル
ms.assetid: 835162c0-6596-42ae-bc6d-824dd6c3f69f
keywords:
- トレース メッセージのヘッダー ファイル WDK
- TMH ファイル WDK
- ファイルの WDK ソフトウェア トレース
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1f55b9b475ae935e1304ec78fa17f3ea8783428e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381814"
---
# <a name="trace-message-header-file"></a>トレース メッセージ ヘッダー ファイル


A*トレース メッセージのヘッダー* (TMH) ファイルは関数と WPP によって生成されるトレース コードで使用される変数の宣言を含むテキスト ファイルです。 ヘッダー ファイルには、書式の PDB ファイルにトレース メッセージを追加するマクロも含まれています、[トレース プロバイダー](trace-provider.md)、カーネル モード ドライバーまたはユーザー モード アプリケーションなどです。

WPP TMH ファイルを自動的に生成をコンパイルするとき、[トレース プロバイダー](trace-provider.md) WPP マクロが含まれています。 TMH ファイルは、.tmh ファイル名拡張子が、ソース ファイルと同じ名前を持ちます。 WPP では、ソース ファイルと同じディレクトリにファイルを保存します。

追加する必要があるソース コードを WPP マクロを追加すると、 **\#含める**WPP により生成される TMH ファイルのディレクティブ。 Include ステートメントには、フォームがあります。

```
#include SourceFileName.tmh
```

ステートメントは、これの定義の後に表示する必要があります、 [WPP\_コントロール\_GUID](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556186(v=vs.85))マクロ、WPP マクロへの呼び出しの前にします。

詳細については、次を参照してください。[トレース プロデューサーに WPP マクロを追加する](adding-wpp-macros-to-a-trace-provider.md)して[TraceDrv](https://go.microsoft.com/fwlink/p/?LinkId=617726)、ソフトウェア トレース用に設計されたサンプル ドライバー。 TraceDrv サンプルは、 [Windows ドライバー サンプル](https://go.microsoft.com/fwlink/p/?LinkId=616507)GitHub リポジトリにあります。

 

 





