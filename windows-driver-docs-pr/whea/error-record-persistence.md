---
title: エラー レコードの永続化
description: エラー レコードの永続化
ms.assetid: fe43f93a-59bd-4158-ad00-8fef595528cb
keywords:
- Windows ハードウェア アーキテクチャ WDK のエラー、エラー レコードの永続化
- WHEA WDK、エラー レコードの永続化
- WDK WHEA、エラー レコードの永続化エラー
- WDK WHEA を永続化エラー レコード
- WDK WHEA を記録するハードウェア エラーの保存
- WDK WHEA を記録するハードウェア エラーを格納します。
- WDK WHEA を記録するハードウェア エラーの記述
- WDK WHEA を記録するハードウェア エラーを取得します。
- WDK WHEA を記録するハードウェア エラーの読み取り
- ハードウェア エラー WDK WHEA、エラー レコードの永続化
- プラットフォーム固有のハードウェア エラー ドライバー プラグインを WDK WHEA、エラー レコードの永続化
- PSHED プラグイン WDK WHEA、エラー レコードの永続化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e9af0a18c33c832d7ca393e9d7a7fbf3bfa7c0c9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354431"
---
# <a name="error-record-persistence"></a>エラー レコードの永続化


PSHED では、保存し、システムの永続的なデータ ストレージとの間にエラー レコードを取得する Windows カーネルは、オペレーティング システムへのインターフェイスを公開します。 エラーのソース管理操作を以下に示します。

-   エラー レコードを永続的なデータ ストレージに書き込む

-   永続的なデータ ストレージからエラー レコードを読み取り

-   永続的なデータ ストレージからエラー レコードをクリアします。

ハードウェアまたはファームウェア、PSHED でサポートされているエラー レコードの永続化メカニズムと互換性があるハードウェア プラットフォームに実装していない場合、プラットフォーム ベンダーはエラー レコードの永続化に参加している PSHED プラグインを実装する必要があります。 この PSHED プラグイン インターフェイス ハードウェア プラットフォームによって実装されているエラー レコードの永続化メカニズムを使用します。

エラー レコードの永続化に参加している PSHED プラグインを実装する方法の詳細については、次を参照してください。[エラー レコードの永続化に参加している](participating-in-error-record-persistence.md)します。

エラー レコードの永続化の詳細については、次を参照してください。[エラー レコードの永続化メカニズム](error-record-persistence-mechanism.md)します。

 

 




