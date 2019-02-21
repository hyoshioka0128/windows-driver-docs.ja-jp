---
Description: Support for base-driver commands (WpdServiceSampleDriver)
title: 基本ドライバー コマンド (WpdServiceSampleDriver) のサポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e97804a357b14431b945461821b1441da193c6a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530317"
---
# <a name="support-for-base-driver-commands-wpdservicesampledriver"></a>基本ドライバー コマンド (WpdServiceSampleDriver) のサポート


ドライバー モジュール (*WpdBaseDriver.cpp*) サンプルが 2 つのコマンドを処理します。WPD\_コマンド\_共通\_取得\_オブジェクト\_ID\_FROM\_持続\_UNIQUE\_ID と WPD\_コマンド\_一般的な\_保存\_クライアント\_情報。

ただし、 *WpdBaseDriver.cpp*処理、ドライバーですべてのコマンドの開始点になります。 つまり、すべてのコマンドで最初に処理、 **WpdBaseDriver::DispatchMessage**メソッド。 このメソッドは、指定されたコマンドのカテゴリを調べ、列挙型、プロパティ、機能、またはサービス コマンド ハンドラーに転送します。

次の表では、基本ドライバー モジュールでサポートされているコマンドのハンドラーと共に、基本ドライバー モジュールでサポートされている 2 つのコマンドについて説明します。

|                                                                       |                                      |                                                                                                                       |
|-----------------------------------------------------------------------|--------------------------------------|-----------------------------------------------------------------------------------------------------------------------|
| コマンド                                                               | ハンドラー                              | 説明                                                                                                           |
| WPD\_コマンド\_共通\_取得\_オブジェクト\_ID\_FROM\_持続\_UNIQUE\_ID | OnGetOjectIDsFromPersistentUniqueIDs | 指定された永続的な一意の識別子に一致するオブジェクト識別子を取得しようとするアプリケーションに発行されます。 |
| WPD\_コマンド\_共通\_保存\_クライアント\_情報                       | OnSaveClientInfo                     | アプリケーションをデバイスまたはサービスへの接続を開こうとすると発行されます。                                       |

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


****
[WpdServiceSampleDriver](the-wpdservicesampledriver-sample.md)

[WPD ドライバーのサンプル](the-wpd-driver-samples.md)

 

 





