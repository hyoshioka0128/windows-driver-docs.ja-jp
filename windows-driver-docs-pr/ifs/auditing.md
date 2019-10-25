---
title: 監査
description: 監査
ms.assetid: 0a703a27-91d6-41fc-bd46-a9486842a150
keywords:
- セキュリティ WDK ファイルシステム、監査
- WDK ファイルシステムの監査
- イベント WDK ファイルシステム
- SeAuditingFileEvents
- SeOpenObjectAuditAlarm
- イベント WDK 「イベント」も参照
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 37525f66392af208c7e7495693a2a4b841a6bd53
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841484"
---
# <a name="auditing"></a>監査


## <span id="ddk_auditing_if"></span><span id="DDK_AUDITING_IF"></span>


優れたセキュリティ設計の原則の1つは、セキュリティで保護されたシステムのようなものが存在しないことを認めることです。 システムの開発者は、すべてのセキュリティを回避することを意識する必要があります。 これは、たとえば、セキュリティサブシステムを調査してシステム内のホールを検出し、悪用することによって、アクティブに実行できます。 または、誤って重要なデータを上書きしたり削除したりすることがあります。 原因にかかわらず、このような侵害を検出できるシステムを構築することが不可欠です。

Windows 内の監査システムは、特定のセキュリティイベントを追跡するためのメカニズムを提供します。これにより、後でログを分析して、破損または侵害されたシステムの事後分析を実行できます。 Windows 深くの監査メカニズムには、ファイルシステムがシステムデータの永続的なストレージを維持する役割を果たすため、ファイルシステムが関係します。 多くのシステムでは、セキュリティの必要性が大幅に低下し、その場合は監査が無効になっています。 ファイルシステムは、両方の環境の問題に対処できるように実装する必要があります。

監査の主要なルーチンは次のとおりです。

-   [**SeAuditingFileEvents**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-seauditingfileevents)--このルーチンは、システムでファイル監査が有効になっているかどうかを判断します。これは、完全な監査チェックを実行する必要があるかどうかを判断するためのグローバルポリシーチェックです。 このルーチンは、セキュリティシステムの操作を最適化するために導入されました。

-   [**SeOpenObjectAuditAlarm**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-seopenobjectauditalarm)--このルーチンは、Windows システムでプライマリ監査操作を実行します (オブジェクトを開く試行を監査します)。 オブジェクトへのアクセスが成功したか失敗したかにかかわらず、監査対象のオブジェクトにアクセスしようとしたことに注意してください。

監査の要件はありません。 WDK 実装監査の IFS セクションにあるサンプルファイルシステム (FAT や CDFS など) はありません。 ただし、セキュリティの観点からは、管理者がシステムのセキュリティ動作を監視できるようにするため、監査が重要になります。

 

 




