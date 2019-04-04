---
title: アーカイブの CLFS サポート
description: アーカイブの CLFS サポート
ms.assetid: 5a07d7d2-4939-48f8-bd4c-855af61034fb
keywords:
- 共通のログ ファイル システムの WDK カーネルのアーカイブ
- CLFS WDK のカーネルのアーカイブ
- アーカイブの WDK CLFS
- 非一時的なログ WDK CLFS
- アーカイブ末尾 WDK CLFS
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c2772bcd6ec7a7b23fd4beb0cef59cfeb6fef3de
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550412"
---
# <a name="clfs-support-for-archiving"></a>アーカイブの CLFS サポート





Common Log File System (CLFS) は、専用のログをアーカイブ末尾を保持することでアーカイブをサポートします。 呼び出すと[ **ClfsCreateLogFile** ](https://msdn.microsoft.com/library/windows/hardware/ff540792)専用のログを作成するには、ファイルを設定することができます\_属性\_のアーカイブ フラグ、 *fFlagsAndAttributes*CLFS がログのアーカイブ末尾を維持する必要がありますを指定するパラメーター。 CLFS は、アーカイブ末尾を保持するログと呼ばれる、*短期間ではないログ*します。

データベースでトランザクションを実行して、各トランザクションがログ レコードによって記述される更新プログラムをいくつかあるとします。 特定のトランザクションがコミットし、安定したストレージに書き込まれた後、は、そのトランザクションをかどうかを記述するログ レコードを必要はありません。 ログの中にレコードは必要ありませんは、システム障害が発生した場合の回復を再起動します。 ただし、データベースを保持する安定したストレージ メディアが失敗して、データベース アーカイブされていない最近のメディアで、データベースの更新は失われる可能性があります。

前の段落には、アーカイブ データベースのレコードがについて説明しますが、他のシナリオでログ レコードをアーカイブする場合があります。 いずれの場合も、アーカイブと、クライアント (ソフトウェア) の役割です。 追跡できますアーカイブ ログのアーカイブ末尾を設定して行いました。 アーカイブ末尾のアーカイブがまだ完了していない、最も古いレコードのログ シーケンス番号 (LSN) では。

実際には、2 つの尾部短期間ではないログ: ベース LSN とアーカイブ末尾でマークされた 1 つで 1 つをマークします。 2 つの末尾が離れを配置するには、必要に応じて呼び出すことによって[ **ClfsAdvanceLogBase** ](https://msdn.microsoft.com/library/windows/hardware/ff540773) (または[ **ClfsWriteRestartArea**](https://msdn.microsoft.com/library/windows/hardware/ff541770))、および[ **ClfsSetArchiveTail**](https://msdn.microsoft.com/library/windows/hardware/ff541744)します。 通常、基本の LSN は、トランザクション ロールバックのために必要になりますもまたは回復、および対象のアーカイブが実行されていない最も古いレコードをアーカイブ末尾のポイントを再起動する最も古いレコードを指します。 アーカイブ末尾には、ベースの LSN よりも小さくすることがありますまたはベースの LSN よりも大きいことが考えられますことに注意してください。

ベースの LSN とアーカイブ末尾が重要なを呼び出すと[ **ClfsReadNextLogRecord** ](https://msdn.microsoft.com/library/windows/hardware/ff541690)繰り返しを前の Lsn によってリンクされているレコードのチェーンを読み取るには、元に戻す next Lsn、またはユーザーの Lsn。 **ClfsReadNextLogRecord**はアーカイブ末尾とベースの LSN よりも小さい LSN を持つレコードを読み取れません。 ただし、アーカイブ末尾とベースの LSN 間の LSN がレコードを読み取ります。 次のレコードのチェーンの詳細については、[CLFS Stream からのデータ レコードの読み取り](reading-data-records-from-a-clfs-stream.md)を参照してください。

 

 




