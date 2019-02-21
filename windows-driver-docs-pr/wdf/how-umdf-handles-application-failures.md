---
title: UMDF がアプリケーションのエラーを処理する方法
description: ユーザー モード ドライバー フレームワーク (UMDF) とオペレーティング システム、アプリケーションが失敗したときの操作について説明します。 両方の UMDF バージョン 1 と 2 に適用されます。
ms.assetid: ac59a5fe-5975-455f-9da3-318c0692bf9c
keywords:
- ユーザー モード ドライバー フレームワーク WDK、アプリケーションのエラー
- UMDF WDK、アプリケーションのエラー
- 失敗したアプリケーション WDK UMDF
- アプリケーション エラー WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 58794bae3ae80ed4a737240b5bd3f0180963f752
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557541"
---
# <a name="how-umdf-handles-application-failures"></a>UMDF がアプリケーションのエラーを処理する方法


このトピックでは、ユーザー モード ドライバー フレームワーク (UMDF) とオペレーティング システム、アプリケーションが失敗したときの操作について説明します。 両方の UMDF バージョン 1 と 2 に適用されます。

アプリケーションが失敗したときに、次のイベントが発生します。

-   リフレクターを受け取る[ **IRP\_MJ\_クリーンアップ**](https://msdn.microsoft.com/library/windows/hardware/ff550718)します。

-   クリーンアップ要求が"cancel"IPC チャネルでのホスト プロセスに送信されます。

-   ホスト プロセスと UMDF ドライバーは、保留中の I/O 要求完了します。

 

 





