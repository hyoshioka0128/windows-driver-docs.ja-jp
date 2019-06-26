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
ms.openlocfilehash: 59889d83cffa1a22aee9653c8d1fe3eaa039a2b4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383354"
---
# <a name="clfs-support-for-archiving"></a>アーカイブの CLFS サポート





Common Log File System (CLFS) は、専用のログをアーカイブ末尾を保持することでアーカイブをサポートします。 呼び出すと[ **ClfsCreateLogFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-clfscreatelogfile)専用のログを作成するには、ファイルを設定することができます\_属性\_のアーカイブ フラグ、 *fFlagsAndAttributes*CLFS がログのアーカイブ末尾を維持する必要がありますを指定するパラメーター。 CLFS は、アーカイブ末尾を保持するログと呼ばれる、*短期間ではないログ*します。

データベースでトランザクションを実行して、各トランザクションがログ レコードによって記述される更新プログラムをいくつかあるとします。 特定のトランザクションがコミットし、安定したストレージに書き込まれた後、は、そのトランザクションをかどうかを記述するログ レコードを必要はありません。 ログの中にレコードは必要ありませんは、システム障害が発生した場合の回復を再起動します。 ただし、データベースを保持する安定したストレージ メディアが失敗して、データベース アーカイブされていない最近のメディアで、データベースの更新は失われる可能性があります。

前の段落には、アーカイブ データベースのレコードがについて説明しますが、他のシナリオでログ レコードをアーカイブする場合があります。 いずれの場合も、アーカイブと、クライアント (ソフトウェア) の役割です。 追跡できますアーカイブ ログのアーカイブ末尾を設定して行いました。 アーカイブ末尾のアーカイブがまだ完了していない、最も古いレコードのログ シーケンス番号 (LSN) では。

実際には、2 つの尾部短期間ではないログ: ベース LSN とアーカイブ末尾でマークされた 1 つで 1 つをマークします。 2 つの末尾が離れを配置するには、必要に応じて呼び出すことによって[ **ClfsAdvanceLogBase** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-clfsadvancelogbase) (または[ **ClfsWriteRestartArea**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-clfswriterestartarea))、および[ **ClfsSetArchiveTail**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-clfssetarchivetail)します。 通常、基本の LSN は、トランザクション ロールバックのために必要になりますもまたは回復、および対象のアーカイブが実行されていない最も古いレコードをアーカイブ末尾のポイントを再起動する最も古いレコードを指します。 アーカイブ末尾には、ベースの LSN よりも小さくすることがありますまたはベースの LSN よりも大きいことが考えられますことに注意してください。

ベースの LSN とアーカイブ末尾が重要なを呼び出すと[ **ClfsReadNextLogRecord** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-clfsreadnextlogrecord)繰り返しを前の Lsn によってリンクされているレコードのチェーンを読み取るには、元に戻す next Lsn、またはユーザーの Lsn。 **ClfsReadNextLogRecord**はアーカイブ末尾とベースの LSN よりも小さい LSN を持つレコードを読み取れません。 ただし、アーカイブ末尾とベースの LSN 間の LSN がレコードを読み取ります。 次のレコードのチェーンの詳細については、次を参照してください。 [CLFS Stream からのデータ レコードの読み取り](reading-data-records-from-a-clfs-stream.md)します。

 

 




