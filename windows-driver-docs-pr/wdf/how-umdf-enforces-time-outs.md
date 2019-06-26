---
title: UMDF でのホスト プロセスのタイムアウト
description: UMDF でのホスト プロセスのタイムアウト
ms.assetid: b8a0a4cc-9c6d-40e2-a3f1-9807dbcf15d9
keywords:
- ユーザー モード ドライバー フレームワーク WDK のタイムアウト
- UMDF WDK、タイムアウト
- ユーザー モード ドライバー WDK UMDF、タイムアウト
- タイムアウトの WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 92b6248f82c08b9d2f85b3a85d92dcd26377006f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382837"
---
# <a name="host-process-timeouts-in-umdf"></a>UMDF でのホスト プロセスのタイムアウト


Reflector は、ドライバーのホスト プロセスに重要な要求を送信するときに、ホストは内部タイマーを開始します。 既定のタイムアウト間隔は、60 秒です。 重要な要求には、プラグ アンド プレイ、能力、および I/O の取り消しが含まれます。

ユーザー モード ドライバー フレームワーク (UMDF) ドライバーは、要求の完了に向けたを定期的に操作を実行する限り、reflector は、タイムアウト期間を拡張します。 たとえば、削除要求の場合、ドライバーが定期的に削除コールバックから返される必要があります。

タイムアウト期間が経過すると、reflector は WER エラー レポートを生成、ホスト プロセスを終了し、デバイスを再起動しようとしています。 します。 詳細については、自動再起動は、次を参照してください。[デバイスの UMDF ドライバーでプールを使用して](using-device-pooling-in-umdf-drivers.md)します。

このレポートのフィールドの詳細については、次を参照してください。 [WER レポートでの UMDF メタデータにアクセスする](accessing-umdf-metadata-in-wer-reports.md)します。

タイムアウトの有効期限は、ホスト プロセスを終了する reflector の最も一般的な理由です。

使用して、タイムアウト期間を拡張することができます、 [WDF Verifier コントロール アプリケーション](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdf-verifier-control-application)します。

 

 





