---
title: アーカイブの CLFS サポート
description: アーカイブの CLFS サポート
ms.assetid: 5a07d7d2-4939-48f8-bd4c-855af61034fb
keywords:
- WDK カーネルの共通ログファイルシステムアーカイブ
- CLFS WDK カーネル、アーカイブ
- WDK CLFS のアーカイブ
- 非短期ログ WDK CLFS
- アーカイブテール WDK CLFS
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8310ff02d3160beaef5abfb70b47652a289305c9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837095"
---
# <a name="clfs-support-for-archiving"></a>アーカイブの CLFS サポート





共通ログファイルシステム (CLFS) では、アーカイブテールを保持することで、専用ログのアーカイブをサポートしています。 [**ClfsCreateLogFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfscreatelogfile)を呼び出して専用ログを作成する場合は、 *FFLAGSANDATTRIBUTES*パラメーターのファイル\_属性\_archive フラグを設定して、CLFS がログのアーカイブテールを保持するように指定できます。 CLFS がアーカイブテールを保持しているログは、*非短期ログ*と呼ばれます。

たとえば、データベースでトランザクションを実行していて、各トランザクションにログレコードで記述された複数の更新が含まれているとします。 特定のトランザクションがコミットされ、安定したストレージに書き込まれた後は、そのトランザクションを記述したログレコードが不要になることがあります。 つまり、システム障害が発生した場合、復旧の再開中にログレコードが必要になることはありません。 ただし、データベースを保持している安定したストレージメディアに障害が発生し、データベースが最近別のメディアに保存されていない場合、データベースの更新が失われる可能性があります。

前の段落では、データベースレコードのアーカイブについて説明していますが、他のシナリオではログレコードをアーカイブすることもできます。 どちらの場合も、アーカイブはクライアント (ソフトウェア) の責任です。 ログのアーカイブテールを設定して、実行したアーカイブを追跡することができます。 Archive tail は、アーカイブがまだ完了していない最も古いレコードのログシーケンス番号 (LSN) です。

非短期ログには、実際には2つの末尾があります。1つはベース LSN、もう1つはアーカイブテールでマークされています。 [**ClfsAdvanceLogBase**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfsadvancelogbase) (または[**ClfsWriteRestartArea**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfswriterestartarea)) と[**ClfsSetArchiveTail**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfssetarchivetail)を呼び出すことによって、2つの尾部を配置できます。 通常、ベース LSN はトランザクションのロールバックまたは再起動に必要な最も古いレコードを指し、アーカイブテールはアーカイブが実行されていない最も古いレコードを指しています。 アーカイブの末尾がベース LSN よりも小さいか、またはベース LSN よりも大きい可能性があることに注意してください。

ベース LSN とアーカイブテールは、 [**ClfsReadNextLogRecord**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfsreadnextlogrecord)を繰り返し呼び出して、前の lsn、undo-Next lsns、または user lsn によってリンクされたレコードのチェーンを読み取るときに重要です。 **ClfsReadNextLogRecord**は、lsn が archive tail と base lsn の両方より小さいレコードを読み取りません。 ただし、アーカイブテールとベース LSN の間に LSN があるレコードが読み取られます。 次のレコードチェーンの詳細については、「 [CLFS ストリームからのデータレコードの読み取り](reading-data-records-from-a-clfs-stream.md)」を参照してください。

 

 




