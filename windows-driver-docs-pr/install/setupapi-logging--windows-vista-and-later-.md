---
title: SetupAPI ログ記録
description: SetupAPI ログ記録
ms.assetid: 25beff4d-742a-4d46-bb91-16b3e14f2d6c
keywords:
- SetupAPI WDK、ログ記録
- WDK SetupAPI ログ記録
- SetupAPI WDK Windows Vista のログ記録
- SetupAPI SetupAPI ログについて、Windows Vista の WDK のログ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 865163660a28ae34251feb9bfd6400976d71f67e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348656"
---
# <a name="setupapi-logging"></a>SetupAPI ログ記録


Windows Vista および以降のバージョンの Windows、 [SetupAPI](setupapi.md)次のログ コンポーネントが含まれています。

-   プラグ アンド プレイ (PnP) マネージャーと SetupAPI は、インストールのイベントに関する情報をログ デバイス インストールのテキスト ログ (*SetupAPI.dev.log*) とアプリケーション インストールのテキスト ログ (*SetupAPI.app.log*). デバイス インストールのテキスト ログは、デバイスやドライバーのインストールに関する情報を格納し、アプリケーション インストールのテキスト ログは、デバイス ドライバーのインストールに関連付けられているアプリケーションのソフトウェアのインストールに関する情報を格納します。 SetupAPI テキスト ログのコンテンツに関する詳細については、次を参照してください。 [SetupAPI テキスト ログ](setupapi-text-logs.md)、ログ記録を有効にする方法については、次を参照してください。 および[SetupAPI ログのレジストリ設定](setupapi-logging-registry-settings.md)します。

-   [SetupAPI ログ関数で](https://msdn.microsoft.com/library/windows/hardware/ff550878)、SetupAPI テキスト ログにログ エントリを書き込む PnP デバイス インストールのアプリケーション、クラスのインストーラーと共同インストーラーを使用できます。 これらの関数を使用する方法については、次を参照してください。 [SetupAPI ログ記録関数を使用して](using-the-setupapi-logging-functions.md)します。

 

 





