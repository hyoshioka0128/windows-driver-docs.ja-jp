---
title: トレース メッセージ ヘッダー ファイル
description: トレース メッセージ ヘッダー ファイル
ms.assetid: 835162c0-6596-42ae-bc6d-824dd6c3f69f
keywords:
- トレースメッセージヘッダーファイル WDK
- TMH ファイル WDK
- ファイル WDK ソフトウェアのトレース
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 80b432ed8b5dc5f26fd9c57e1a44c42b3ff23966
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769648"
---
# <a name="trace-message-header-file"></a>トレース メッセージ ヘッダー ファイル


*トレースメッセージヘッダー* (tmh) ファイルは、WPP が生成するトレースコードによって使用される関数と変数の宣言が含まれているテキストファイルです。 ヘッダーファイルには、トレースメッセージの書式設定命令を[トレースプロバイダー](trace-provider.md)の PDB ファイル (カーネルモードドライバーやユーザーモードアプリケーションなど) に追加するマクロも含まれています。

Wpp マクロを含む[トレースプロバイダー](trace-provider.md)をコンパイルすると、wpp によって自動的に tmh ファイルが生成されます。 TMH ファイルにはソースファイルと同じ名前が付けられていますが、ファイル名拡張子は tmh です。 WPP は、ソースファイルと同じディレクトリにファイルを保存します。

WPP マクロをソースコードに追加する場合は、WPP によって生成される TMH ファイル用の** \# include**ディレクティブも追加する必要があります。 Include ステートメントの形式は次のとおりです。

```
#include SourceFileName.tmh
```

この include ステートメントは、 [wpp \_ 制御 \_ guid](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556186(v=vs.85))マクロの定義の後、かつ、wpp マクロを呼び出す前に記述する必要があります。

詳細については、「[トレースプロデューサーに WPP マクロを追加する](adding-wpp-macros-to-a-trace-provider.md)」および「 [tracedrv](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/tracing/tracedriver)(ソフトウェアトレース用に設計されたサンプルドライバー)」を参照してください。 TraceDrv サンプルは、GitHub の[Windows ドライバーサンプル](https://github.com/Microsoft/Windows-driver-samples)リポジトリで入手できます。

 

 





