---
Description: 基本ドライバーコマンドのサポート (Wpdサービス Amwadriver)
title: 基本ドライバーコマンドのサポート (Wpdサービス Amwadriver)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6b1af829fcec30fec4bf83409b24009f38dc8dca
ms.sourcegitcommit: 9102e34c3322d8697dbb6f9a1d78879147a73373
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/28/2020
ms.locfileid: "87264465"
---
# <a name="support-for-base-driver-commands-wpdservicesampledriver"></a>基本ドライバーコマンドのサポート (Wpdサービス Amwadriver)

サンプルの基本ドライバーモジュール (*Wpdbasedriver .cpp*) では、2つのコマンドが処理されます。 wpd \_ コマンド \_ では \_ \_ \_ \_ 、永続的な一意の ID からオブジェクト id を取得 \_ \_ し、 \_ wpd コマンドに共通の \_ \_ \_ クライアント情報を保存し \_ \_ ます。

ただし、 *Wpdbasedriver .cpp*は、ドライバー内のすべてのコマンド処理の開始点としても使用されます。 これは、すべてのコマンドが最初に**Wpdbasedriver::D ispatchmessage**メソッドによって処理されることを意味します。 このメソッドは、指定されたコマンドのカテゴリを調べて、列挙型、プロパティ、機能、またはサービスコマンドハンドラーに転送します。

次の表では、基本ドライバーモジュールでサポートされている2つのコマンドと、基本ドライバーモジュールでサポートされているコマンドのハンドラーについて説明します。

| command                                                               | Handler                              | 説明                                                                                                           |
|-----------------------------------------------------------------------|--------------------------------------|-----------------------------------------------------------------------------------------------------------------------|
| WPD \_ コマンド \_ 共通 \_ \_ \_ \_ の \_ 永続 \_ \_ ID からのオブジェクト ID の取得 | OnGetOjectIDsFromPersistentUniqueIDs | アプリケーションが、指定された永続的な一意の識別子と一致するオブジェクト識別子を取得しようとしたときに発行されます。 |
| WPD \_ コマンドの \_ 共通 \_ 保存 \_ クライアント \_ 情報                       | OnSaveClientInfo                     | アプリケーションがデバイスまたはサービスへの接続を開こうとしたときに発行されます。                                       |

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック

****
[Wpdサービスの Am氏ドライバー](the-wpdservicesampledriver-sample.md)

[WPD ドライバーのサンプル](the-wpd-driver-samples.md)
