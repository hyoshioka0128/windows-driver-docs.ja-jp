---
Description: Support for base-driver commands (WpdBasicHardwareDriverSample)
title: 基本ドライバー コマンド (WpdBasicHardwareDriverSample) のサポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 709d0a97c013101eaf92bb1eb650e094bb703e11
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535770"
---
# <a name="support-for-base-driver-commands-wpdbasichardwaredriversample"></a>基本ドライバー コマンド (WpdBasicHardwareDriverSample) のサポート


サンプルについては、基本ドライバー モジュール (*WpdBaseDriver.cpp*) 1 つのコマンドを処理 (WPD\_コマンド\_共通\_取得\_オブジェクト\_ID\_\_持続\_UNIQUE\_ID)。 ただし、このモジュールは、処理サンプル ドライバーですべてのコマンドの開始点にもします。 つまり、すべてのコマンドで最初に処理、 **WpdBaseDriver::DispatchMessage**メソッド。 このメソッドは、指定されたコマンドのカテゴリを調べ、列挙型、プロパティ、または機能コマンド ハンドラーに転送します。

発生した 1 つの変更、 **WpdBaseDriver::DispatchMessage**メソッドがリソースに関連するコマンドをチェックするコードが削除されました。 関連するコマンドの処理に必要なが不要になったサンプル ドライバーがリソースをサポートしていないため、実装されている以外のコマンドを送信する任意のアプリケーション E を受信する\_NOTIMPL エラー。

次の表では、コマンドのハンドラーと共に、基本ドライバー モジュールでサポートされているコマンドについて説明します。

| コマンド                                                               | ハンドラー                              | 説明                                                                                                              |
|-----------------------------------------------------------------------|--------------------------------------|--------------------------------------------------------------------------------------------------------------------------|
| WPD\_コマンド\_共通\_取得\_オブジェクト\_ID\_FROM\_持続\_UNIQUE\_ID | OnGetOjectIDsFromPersistentUniqueIDs | アプリケーションが特定の永続的な一意の識別子と一致するオブジェクト識別子を取得しようとしたときに発行されます。 |

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


****
[WpdBasicHardwareDriverSample](the-wpdbasichardwaredriver-sample.md)

[WPD ドライバーのサンプル](the-wpd-driver-samples.md)

 

 





