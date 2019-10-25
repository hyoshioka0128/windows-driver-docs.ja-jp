---
title: エラーの挿入
description: エラーの挿入
ms.assetid: d97d49bc-b216-40d6-afd1-aecff624624d
keywords:
- Windows ハードウェアエラーアーキテクチャ WDK、エラー挿入
- WHEA WDK、エラー挿入
- ハードウェアエラー WDK WHEA、エラー挿入
- エラー WDK WHEA、エラー挿入
- プラットフォーム固有のハードウェアエラードライバープラグイン WDK WHEA、エラー挿入
- PSHED プラグイン WDK WHEA、エラー挿入
- エラー挿入 WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ffca22e67acd47e47e8a13bf79fd69bf0a108bcb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844436"
---
# <a name="error-injection"></a>エラーの挿入


PSHED、テストと検証のために Windows カーネルがハードウェアエラーイベントを発生させることのできるオペレーティングシステムへのインターフェイスを公開しています。 エラー挿入に関与する実装が実装されている場合は、エラー挿入操作を実行するために、そのプラグインが PSHED よって呼び出されます。

エラー挿入に参加する PSHED プラグインを実装する方法の詳細については、「[エラー挿入への参加](participating-in-error-injection.md)」を参照してください。

ユーザーモード管理アプリケーションは、 [WHEA 管理 API](https://docs.microsoft.com/windows-hardware/drivers/ddi/_whea/)を呼び出すことによって、ハードウェアプラットフォームにエラーを挿入できます。 WHEA 管理アプリケーションを実装する方法の詳細については、「 [Whea 管理アプリケーション](whea-management-applications.md)」を参照してください。

 

 




