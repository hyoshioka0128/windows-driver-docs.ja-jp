---
title: エラーの挿入
description: エラーの挿入
ms.assetid: d97d49bc-b216-40d6-afd1-aecff624624d
keywords:
- Windows ハードウェア アーキテクチャ WDK のエラー、エラーの挿入
- WHEA WDK、エラーの挿入
- ハードウェア エラー WDK WHEA、エラー インジェクション
- エラー WDK WHEA、エラーの挿入
- プラットフォーム固有のハードウェア エラー ドライバー プラグインを WDK WHEA、エラーの挿入
- PSHED プラグイン WDK WHEA、エラーの挿入
- WDK WHEA エラーの挿入
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 124037583f860d2f7f5ba143f7207b3659e56709
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529043"
---
# <a name="error-injection"></a>エラーの挿入


PSHED では、Windows カーネルが、テストと検証が発生するハードウェアのエラー イベントを発生オペレーティング システムへのインターフェイスを公開します。 エラーの挿入に参加しているプラグイン PSHED が実装されている場合、エラーの挿入操作を実行するよう PSHED によって呼び出されます。

エラーの挿入に参加している PSHED プラグインを実装する方法の詳細については、次を参照してください。[エラー インジェクションに参加している](participating-in-error-injection.md)します。

ユーザー モードの管理アプリケーションは呼び出すことによって、ハードウェア プラットフォームにエラーを挿入することができます、 [WHEA 管理 API](https://msdn.microsoft.com/library/windows/hardware/ff560556)します。 WHEA 管理アプリケーションを実装する方法の詳細については、次を参照してください。 [WHEA 管理アプリケーション](whea-management-applications.md)します。

 

 




