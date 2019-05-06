---
title: 最適化の条件付きトレースする前に、WPP マクロを生成することを確認します。
description: トレースする前に、WPP マクロを生成する条件付きチェックを最適化できます。
ms.assetid: 0d0ad0de-561f-4480-be91-2304242fee91
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f4c50510ed28c00d9f32c5abe80e6aace29c2ddc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549050"
---
# <a name="can-i-optimize-the-conditional-checks-that-the-wpp-macros-produce-before-the-tracing"></a>トレースする前に、WPP マクロを生成する条件付きチェックを最適化できますか。


WPP の条件付きチェックを削除する\_INIT\_WPP マクロを使用することを呼び出さないようにをトレースします。 この場合にのみを行うことができます WPP\_INIT\_のソース コード内でトレースするあらゆる試みが行われる前に、トレースが呼び出されます、[トレース プロバイダー](trace-provider.md)、カーネル モード ドライバーまたはユーザー モード アプリケーションなどです。

**重要な**  トレースがオブジェクトのコンストラクターまたはマクロで行われた場合に、このチェックを削除しないでください。 それ以外の場合、トレース プロバイダーでアクセス違反が発生する可能性があります。

 

インクルードする前に、[トレース メッセージのヘッダー (.tmh) ファイル](trace-message-header-file.md)WPP の条件付きチェックを無効にするのには、次の定義を追加、ソース コードで\_INIT\_トレースします。

```
#define WPP_CHECK_INIT
```

 

 





