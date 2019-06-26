---
title: UMDF によるアプリケーション エラーの処理方法
description: ユーザー モード ドライバー フレームワーク (UMDF) とオペレーティング システム、アプリケーションが失敗したときの操作について説明します。 両方の UMDF バージョン 1 と 2 に適用されます。
ms.assetid: ac59a5fe-5975-455f-9da3-318c0692bf9c
keywords:
- ユーザー モード ドライバー フレームワーク WDK、アプリケーションのエラー
- UMDF WDK、アプリケーションのエラー
- 失敗したアプリケーション WDK UMDF
- アプリケーション エラー WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 42055756ed9c46efeb91e731a429692fe5ef945a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382830"
---
# <a name="how-umdf-handles-application-failures"></a>UMDF によるアプリケーション エラーの処理方法


このトピックでは、ユーザー モード ドライバー フレームワーク (UMDF) とオペレーティング システム、アプリケーションが失敗したときの操作について説明します。 両方の UMDF バージョン 1 と 2 に適用されます。

アプリケーションが失敗したときに、次のイベントが発生します。

-   リフレクターを受け取る[ **IRP\_MJ\_クリーンアップ**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-cleanup)します。

-   クリーンアップ要求が"cancel"IPC チャネルでのホスト プロセスに送信されます。

-   ホスト プロセスと UMDF ドライバーは、保留中の I/O 要求完了します。

 

 





