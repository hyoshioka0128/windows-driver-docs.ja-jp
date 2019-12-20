---
title: I/O を処理するためのファイル オブジェクトの作成
description: I/O を処理するためのファイル オブジェクトの作成
ms.assetid: 3cd826fc-5c67-4ab4-800a-b5aa4bd5244f
keywords:
- i/o WDK UMDF を処理するファイルオブジェクト
- i/o WDK UMDF を処理するファイルオブジェクト、作成
- I/o 要求 WDK UMDF、file オブジェクト
- ユーザーモードドライバーフレームワーク WDK、i/o を処理するファイルオブジェクト
- UMDF WDK、i/o を処理するファイルオブジェクト
- ユーザーモードドライバー WDK UMDF、i/o を処理するファイルオブジェクト
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d60970accb3c12d1cca183e03e502d5efab20a39
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210226"
---
# <a name="creating-a-file-object-to-handle-io"></a>I/O を処理するためのファイル オブジェクトの作成

[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

アプリケーションがファイルハンドルを開くと、i/o マネージャーによってファイルオブジェクトが作成されます。 さらに、フレームワークは、i/o マネージャーのファイルオブジェクトを表すフレームワークファイルオブジェクトを作成します。

ドライバーによって**Umdffileobjectpolicy**ディレクティブが**AllowNullAndUnknownFileObjects**に設定されていない限り、UMDF では、各 i/o 要求を file オブジェクトに関連付ける必要があります。 このディレクティブの詳細については、「 [INF ファイルでの WDF ディレクティブの指定](specifying-wdf-directives-in-inf-files.md)」を参照してください。

アプリケーションから独立した i/o を、アプリケーションからスタック内の次のドライバーに送信する場合 (デバイスの初期化中やデバイスイベントの通知を受け取る場合など)、ドライバーは、要求に関連付ける独自のファイルオブジェクトを作成する必要があります。

次のセクションでは、ドライバーによって作成されたファイルオブジェクトとアプリケーションで作成されたファイルオブジェクトの違い、およびドライバーによるファイルオブジェクトの作成方法と使用方法について説明します。

-   [ドライバーで作成されたファイルとアプリケーションで作成されたファイルオブジェクト](driver-created-versus-application-created-file-objects.md)
-   [ドライバーで作成されたファイルオブジェクトの作成と使用](creating-and-using-driver-created-file-objects.md)

 

 





