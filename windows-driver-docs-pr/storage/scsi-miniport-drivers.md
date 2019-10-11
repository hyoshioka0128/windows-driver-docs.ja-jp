---
title: SCSI ミニポート ドライバー
description: SCSI ミニポート ドライバー
ms.assetid: d9268be8-a68d-4617-b323-349ce7c62f3f
keywords:
- SCSI ミニポートドライバー WDK 記憶域
- 記憶域ミニポートドライバー WDK、SCSI ミニポートドライバー
- ミニポートドライバー WDK 記憶域、SCSI ミニポートドライバー
- SCSI ミニポートドライバー WDK 記憶域、SCSI ミニポートドライバーについて
- HBA WDK SCSI
ms.date: 10/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: 0961a052c3b8273459992e95214f85e955c923b0
ms.sourcegitcommit: 5f4252ee4d5a72fa15cf8c68a51982c2bc6c8193
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/10/2019
ms.locfileid: "72252454"
---
# <a name="scsi-miniport-drivers"></a>SCSI ミニポート ドライバー

ここでは、次の情報について説明します。

[SCSI ミニポートドライバーでのプラグアンドプレイのサポート](supporting-plug-and-play-in-a-scsi-miniport-driver.md)

[プラグアンドプレイ SCSI ミニポートドライバーのレジストリエントリ](registry-entries-for-plug-and-play-scsi-miniport-drivers.md)

[ブートドライブを管理する SCSI ミニポートドライバーに関する制限](restrictions-on-scsi-miniport-drivers-that-manage-the-boot-drive.md)

[SCSI ミニポートドライバーでのエラー処理](error-handling-in-scsi-miniport-drivers.md)

[SCSI ミニポートドライバールーチン](scsi-miniport-driver-routines.md)

NT ベースのオペレーティングシステム用の SCSI ミニポートドライバーは、HBA 固有ですが、オペレーティングシステムに依存しません。 つまり、各ミニポートドライバーは、システムによって提供される SCSI ポートドライバー (ダイナミックリンクライブラリ (DLL)) とリンクし、ポートドライバーの **ScsiPort * * * Xxx*ルーチンだけを呼び出して、システムとその HBA と通信します。 このような SCSI ミニポートドライバーは、Microsoft Win32 アプリケーションをサポートする他の Microsoft オペレーティングシステム上で実行され、**ScsiPort * * * Xxx*ルーチンもエクスポートされます。 **ScsiPort * * * Xxx*ルーチンの詳細については、「 [SCSI ポートドライバーのサポートルーチン](scsi-port-driver-support-routines.md)」を参照してください。

**ScsiPort * * * Xxx*以外のルーチンを呼び出す SCSI ミニポートドライバーは、両方の Microsoft オペレーティングシステム環境で実行できないことに注意してください。 NT ベースのオペレーティングシステムを含む、Microsoft Windows システム間で移植性を維持するために、SCSI ミニポートドライバーはシステムが提供した **ScsiPort * * * Xxx*のみを呼び出す必要があります。

SCSI ミニポートドライバーはプラグアンドプレイドライバーの場合もあれば、リソース再配布や電源管理などのプラグアンドプレイ操作に参加していないレガシドライバーとして実行することもできます。 プラグアンドプレイとレガシミニポートドライバーの主な違いは、初期化ルーチンが呼び出され、Microsoft Windows NT 4.0 のミニポートドライバーに適用された特定の制限が適用される順序です。
