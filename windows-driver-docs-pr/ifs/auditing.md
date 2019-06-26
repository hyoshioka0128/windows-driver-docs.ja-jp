---
title: 監査
description: 監査
ms.assetid: 0a703a27-91d6-41fc-bd46-a9486842a150
keywords:
- 監査セキュリティ WDK ファイル システム
- WDK のファイル システムの監査
- WDK のファイル システムのイベント
- SeAuditingFileEvents
- SeOpenObjectAuditAlarm
- WDK を参照してくださいイベントものイベント
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: df5500e9b6944c0cc4e423ce01318200d1112e32
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385315"
---
# <a name="auditing"></a>監査


## <span id="ddk_auditing_if"></span><span id="DDK_AUDITING_IF"></span>


適切なセキュリティ設計の基本思想の 1 つは、セキュリティで保護されたシステムとしてのようなものがないことを正直に言うとです。 システムの開発者は、ユーザーがどのようなセキュリティが存在する回避ことに注意してくださいである必要があります。 でしたこれ積極的などを検索し、システム内でのセキュリティ ホールを悪用して、セキュリティ サブシステムをプローブします。 または、これは、偶発的ななどが誤って上書きまたは重要なデータを削除しています。 原因に関係なく、このような侵害を検出するシステムを構築する必要があります。

Windows での監査システムでは、ログは破損しているか、侵害されたシステムの事後分析を実行するには、後で分析できるように、特定のセキュリティ イベントを追跡するためのメカニズムを提供します。 密接に Windows の監査メカニズムには、ファイル システム、システム データの永続的な記憶域の管理を担当しているため、ファイル システムが含まれます。 多くのシステムのセキュリティ ニーズは大幅に減少、およびような場合、監査が無効です。 ファイル システムは、これら両方の環境の問題に対処することができます、このような方法で実装する必要があります。

監査のためのキーのルーチンは次のとおりです。

-   [**SeAuditingFileEvents**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-seauditingfileevents)--かどうかファイル監査が有効になって、システムでこのルーチンを決定します。 これは、完全な監査チェックを行う必要があるかどうかを判断するグローバル ポリシーを確認します。 このルーチンは、セキュリティ システムの操作を最適化するために導入されました。

-   [**SeOpenObjectAuditAlarm**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-seopenobjectauditalarm)--このルーチンは、Windows システム (監査オブジェクトを開こうとする) でプライマリ監査操作を実行します。 オブジェクトへのアクセスが成功したか失敗したかどうかではありませんが監査されるオブジェクトにアクセスしようとするにあることに注意してください。

監査の要件はありません。 サンプルのファイル システム (FAT または例では、cdfs を含む) IFS セクションでは、WDK は、監査を実装します。 ただし、セキュリティの観点から監査は、重要なシステムのセキュリティ動作を監視するための管理者が許可されています。

 

 




