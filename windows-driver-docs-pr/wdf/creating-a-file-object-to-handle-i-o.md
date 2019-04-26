---
title: I/O を処理するためのファイル オブジェクトの作成
description: I/O を処理するためのファイル オブジェクトの作成
ms.assetid: 3cd826fc-5c67-4ab4-800a-b5aa4bd5244f
keywords:
- WDK UMDF の I/O を処理するために、ファイル オブジェクト
- I/O WDK の UMDF を処理するために、ファイル オブジェクトを作成します。
- I/O 要求の WDK UMDF、ファイル オブジェクト
- ユーザー モード ドライバー フレームワーク WDK、I/O ハンドルへのファイル オブジェクト
- UMDF WDK、I/O ハンドルへのファイル オブジェクト
- ユーザー モード ドライバー WDK UMDF、ファイル I/O をハンドルするオブジェクト
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e69304899e9498edf06adbdac93092d7d5a4e856
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358505"
---
# <a name="creating-a-file-object-to-handle-io"></a>I/O を処理するためのファイル オブジェクトの作成

[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

アプリケーションでは、ファイル ハンドルが開いたら、I/O マネージャーは、ファイル オブジェクトを作成します。 フレームワークでは、さらに、I/O マネージャーのファイル オブジェクトを表すフレームワーク ファイル オブジェクトを作成します。

ドライバーを設定しない限り、 **UmdfFileObjectPolicy**ディレクティブを**AllowNullAndUnknownFileObjects**UMDF には、ファイル オブジェクトと関連付けるには、各 I/O 要求が必要があります。 このディレクティブの詳細については、次を参照してください。 [INF ファイルで WDF ディレクティブを指定する](specifying-wdf-directives-in-inf-files.md)します。

UMDF ドライバーは、アプリケーション スタックの次のドライバーに (たとえば、デバイスの初期化中またはデバイス イベントの通知を取得する) の独立した I/O を送信する場合、ドライバーは、要求に関連付ける独自のファイル オブジェクトを作成する必要があります。

次のセクションでは、ドライバーに作成されたファイル オブジェクトとファイルのアプリケーションで作成されたオブジェクトのドライバーの作成し、ファイル オブジェクトを使用しての違いを説明します。

-   [ドライバーが作成したアプリケーションで作成されたファイル オブジェクトとの比較](driver-created-versus-application-created-file-objects.md)
-   [作成して、ドライバーに作成されたファイル オブジェクトを使用します。](creating-and-using-driver-created-file-objects.md)

 

 





