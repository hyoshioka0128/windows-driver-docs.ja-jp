---
title: ユーザー モード アプリケーションで WPP ソフトウェア トレースを初期化する方法
description: ユーザー モード アプリケーションで WPP ソフトウェア トレースを初期化する方法
ms.assetid: 1f1ab873-a1c3-4915-af31-ab74c1898fcb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b31b7e087c76a0f1919e6238ad60c95f0ba5fbb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329714"
---
# <a name="how-do-i-initialize-wpp-software-tracing-in-a-user-mode-application"></a>ユーザー モード アプリケーションで WPP ソフトウェア トレースを初期化する方法


ユーザー モード アプリケーションで WPP トレースを初期化するには呼び出すことによって、 [WPP\_INIT\_トレース](https://msdn.microsoft.com/library/windows/hardware/ff556191)WPP ソフトウェア トレースを初期化するためにマクロ。

エラーを回避するために呼び出す必要があります、 [WPP\_INIT\_トレース](https://msdn.microsoft.com/library/windows/hardware/ff556191)マクロの時点で、ソース コードは、トレースの試行までに作成されたありません。

 

 





