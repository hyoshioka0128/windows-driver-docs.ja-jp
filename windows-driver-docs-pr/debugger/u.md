---
title: U (Windows デバッガーの用語集)
description: 用語集ページ - U
Robots: noindex, nofollow
ms.assetid: f3866ed9-eb94-4433-8a73-3b37f7e67303
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 41e8dd3ccb60e1af399873e003559c104440d7fc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560664"
---
# <a name="u"></a>U


<span id="user_mode"></span><span id="USER_MODE"></span>**ユーザー モード**  
内での Windows アプリケーションやサブシステムを実行*ユーザー モード*します。 ユーザー モードで実行されるプロセスは、独自の仮想アドレス空間内で行います。 システム ハードウェア、使用、およびシステムの整合性を損なう可能性があるシステムの他の部分が割り当てられていないメモリを含む、システムの多くの部分に直接アクセスが禁止されます。 ユーザー モードで実行されているプロセスにシステムやその他のユーザー モード プロセスから効果的に分離するため、これらのリソース使用でき、干渉ことはできません。

ユーザー モード プロセスは、次のカテゴリに分類できます。

-   システム プロセス

    これらは、重要な機能を実行し、オペレーティング システムの不可欠な一部であります。 システム プロセスには、ログオン プロセスとセッション マネージャー プロセスなどの項目が含まれます。

-   サーバー プロセス

    これらは、イベント ログと、スケジューラなどのオペレーティング システム サービスです。 ブート時に自動的に開始するように構成できます。

-   環境サブシステム

    これらのオプションを使用して、アプリケーションの完全なオペレーティング システム環境を作成します。 Windows には、次の 3 つの環境が用意されています。Win32、POSIX、および OS/2。

-   ユーザー アプリケーション

    5 つの種類があります。Win32、Windows 3.1、MS-DOS の Microsoft、POSIX 場合、OS/2。

<span id="user_mode_debugging"></span><span id="USER_MODE_DEBUGGING"></span>**ユーザー モードのデバッグ**  
ターゲットがユーザー モードで実行されているデバッガー セッションです。

<span id="user_mode_target"></span><span id="USER_MODE_TARGET"></span>**ユーザー モードのターゲット**  
ターゲット アプリケーションを参照してください。

 

 





