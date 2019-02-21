---
title: ログ ファイルの作成
description: ログ ファイルの作成
ms.assetid: dad0f9fc-1a88-4bee-800a-5a4464fff600
keywords:
- ログ ファイル WDK Driver Verifier
- Driver Verifier の WDK、ログ ファイル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5de449515a57945ab411524d55c6fbdeccf4b777
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530204"
---
# <a name="creating-log-files"></a>ログ ファイルの作成


## <span id="ddk_creating_log_files_tools"></span><span id="DDK_CREATING_LOG_FILES_TOOLS"></span>


Driver Verifier は、ログ ファイルを作成できます。 これらのファイルは、Driver Verifier のアクションとドライバーの検証中のアクションに関連する統計数の定期的な更新プログラムが含まれます。

使用して検証ユーティリティからログ ファイルが作成されます、 **/log**パラメーター。 ログ レコードの頻度を指定することもできます。 参照してください[ **Verifier のコマンド ライン**](verifier-command-line.md)詳細についてはします。

各エントリはグローバル カウンターと、個々 のカウンターだけと同様、 **verifier/query**コマンド。

これらの統計情報の詳細については、次を参照してください。[グローバル カウンターの監視](monitoring-global-counters.md)と[カウンターを個別に監視](monitoring-individual-counters.md)します。

 

 





