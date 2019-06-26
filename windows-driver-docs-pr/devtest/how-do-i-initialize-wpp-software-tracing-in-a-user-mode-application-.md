---
title: ユーザー モード アプリケーションで WPP ソフトウェア トレースを初期化する方法
description: ユーザー モード アプリケーションで WPP ソフトウェア トレースを初期化する方法
ms.assetid: 1f1ab873-a1c3-4915-af31-ab74c1898fcb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2382b292e274fbdbc9b1d059004391a62fcd2f41
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358286"
---
# <a name="how-do-i-initialize-wpp-software-tracing-in-a-user-mode-application"></a>ユーザー モード アプリケーションで WPP ソフトウェア トレースを初期化する方法


ユーザー モード アプリケーションで WPP トレースを初期化するには呼び出すことによって、 [WPP\_INIT\_トレース](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556191(v=vs.85))WPP ソフトウェア トレースを初期化するためにマクロ。

エラーを回避するために呼び出す必要があります、 [WPP\_INIT\_トレース](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556191(v=vs.85))マクロの時点で、ソース コードは、トレースの試行までに作成されたありません。

 

 





