---
title: U (Windows デバッガー用語集)
description: 用語集のページ-U
ms.assetid: f3866ed9-eb94-4433-8a73-3b37f7e67303
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 27e7a99269f473197137f9c6dd8ce02c0c01c17b
ms.sourcegitcommit: 48c4b6d3a504583d2f588ed892a4a281d4b58301
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/06/2019
ms.locfileid: "70387064"
---
# <a name="u"></a>U


<span id="user_mode"></span><span id="USER_MODE"></span>**ユーザーモード**  
アプリケーションとサブシステムは、*ユーザーモード*で Windows 内で実行されます。 ユーザーモードで実行されるプロセスは、独自の仮想アドレス空間内で実行されます。 システムハードウェア、使用するために割り当てられていないメモリ、システムの整合性を損なう可能性があるシステムのその他の部分など、システムの多くの部分に直接アクセスすることが制限されています。 ユーザーモードで実行されるプロセスはシステムおよびその他のユーザーモードプロセスから事実上分離されるため、これらのリソースに干渉することはできません。

ユーザーモードのプロセスは、次のカテゴリに分類できます。

-   システムプロセス

    これらは重要な機能を実行し、オペレーティングシステムに不可欠な要素です。 システムプロセスには、ログオンプロセスやセッションマネージャープロセスなどの項目が含まれます。

-   サーバープロセス

    これらは、イベントログやスケジューラなどのオペレーティングシステムサービスです。 起動時に自動的に開始するように構成することができます。

-   環境サブシステム

    これらは、アプリケーションの完全なオペレーティングシステム環境を作成するために使用されます。 Windows には、次の3つの環境が用意されています。Win32、POSIX、OS/2。

-   ユーザーアプリケーション

    次の5つの種類があります。Win32、Windows 3.1、Microsoft MS-DOS、POSIX、OS/2。

<span id="user_mode_debugging"></span><span id="USER_MODE_DEBUGGING"></span>**ユーザーモードのデバッグ**  
ターゲットがユーザーモードで実行されているデバッガーセッション。

<span id="user_mode_target"></span><span id="USER_MODE_TARGET"></span>**ユーザーモードのターゲット**  
「ターゲットアプリケーション」を参照してください。

 

 





