---
title: KMDF ドライバーからのバグ チェック
description: KMDF ドライバーからのバグ チェック
ms.assetid: 4fde9586-3455-4692-8eeb-bbf64c0a437e
keywords:
- WDK KMDF ドライバーをデバッグするには、バグを確認します
- WDK KMDF のバグ チェック
- KMDF コードの検証
- KMDF バグは、WDK を確認します。
- WDF_VIOLATION
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7ea1a1387117ba1509030fb1fbb7fe13bd6de88e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353205"
---
# <a name="bug-checks-from-kmdf-drivers"></a>KMDF ドライバーからのバグ チェック


フレームワークはフレームワーク ベースのドライバーからのエラーのいくつかの型をチェックします。 これらのエラーが発生した場合、フレームワークを作成、WDF\_違反のバグ チェックします。

フレームワークをチェックするドライバー エラーの種類については、次を参照してください。 [ **WDF\_違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0x10d---wdf-violation)します。

ドライバーは、呼び出すことによってバグ チェックを作成できます[ **WdfVerifierKeBugCheck**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfverifier/nf-wdfverifier-wdfverifierkebugcheck)します。

 

 





