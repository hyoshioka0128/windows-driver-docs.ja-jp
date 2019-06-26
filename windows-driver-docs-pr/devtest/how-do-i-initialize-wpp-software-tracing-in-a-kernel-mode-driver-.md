---
title: カーネル モード ドライバーでは、WPP ソフトウェア トレースを初期化する方法
description: カーネル モード ドライバーでは、WPP ソフトウェア トレースを初期化する方法
ms.assetid: 739428e8-14ff-4435-80e6-35b5c3366c79
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4cc6ed940ea8a467639189aacb307103e800b975
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356519"
---
# <a name="how-do-i-initialize-wpp-software-tracing-in-a-kernel-mode-driver"></a>カーネル モード ドライバーで WPP ソフトウェア トレースを初期化する方法


カーネル モード ドライバーでは、WPP トレースを初期化するには呼び出すことによって、 [WPP\_INIT\_トレース](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556191(v=vs.85))WPP ソフトウェア トレースを初期化するためにマクロ。

エラーを回避するために呼び出す必要がありますが、 [WPP\_INIT\_トレース](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556191(v=vs.85))マクロで、 [ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/storage/driverentry-of-ide-controller-minidriver)ドライバーの機能です。

 

 





