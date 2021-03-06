---
title: カーネル オブジェクトの管理
description: カーネル オブジェクトの管理
ms.assetid: d45aca94-67b7-444d-8585-713ec982e3bc
keywords:
- カーネル モード ドライバー WDK、オブジェクトの管理
- オブジェクト マネージャー WDK カーネル
- オブジェクト管理 WDK カーネル
- オブジェクトを参照します。
- WDK のユーザー モードのオブジェクト名
- オブジェクトの WDK ユーザー モードの管理
- カーネル モード オブジェクト WDK
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3883195353e59c1ed62819b03ed5af3dfb673d6b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380278"
---
# <a name="managing-kernel-objects"></a>カーネル オブジェクトの管理





Windows オブジェクト マネージャー コントロール*オブジェクト*はカーネル モードのオペレーティング システムの一部であります。 オブジェクトは、オペレーティング システムを管理するデータのコレクションです。

一般的なカーネル モードのオブジェクトには、次のオブジェクトが含まれます。

-   デバイス オブジェクト (を参照してください[デバイス オブジェクトとデバイス スタック](device-objects-and-device-stacks.md))。

-   ファイル オブジェクト。

-   シンボリック リンク。

-   レジストリ キーです。

-   スレッドとプロセス。

-   イベント オブジェクトおよびミュー テックス オブジェクトなどのカーネル ディスパッチャー オブジェクト。 (を参照してください[カーネルのディスパッチャー オブジェクト](kernel-dispatcher-objects.md))。

-   コールバック オブジェクト。 (を参照してください[コールバック オブジェクト](callback-objects.md))。

-   セクション オブジェクト。 (を参照してください[セクション オブジェクトとビュー](section-objects-and-views.md))。

カーネル モードのオブジェクトを使用すると、オペレーティング システムが必要なオブジェクトの部分に影響を及ぼさずに、オブジェクト マネージャーとパートナーシップのオブジェクトを操作できます。 この原則と呼びます*カプセル化*オブジェクト指向プログラミングの主要な概念の 1 つです。 (カーネル モードのオブジェクトはオブジェクト指向の他の側面を指定しないため、カーネル モードのプログラミングは通常呼ば[*オブジェクトに基づく*](object-based.md))。カーネル モードのオブジェクトは、C++ または Microsoft COM 内のオブジェクトと同じ規則に従っていません。

カーネル モードのオブジェクトは、ポインターによって参照できます。 オブジェクトには、オブジェクトの名前を付ける可能性があります。 オブジェクト名の詳細については、次を参照してください。[オブジェクト名](object-names.md)します。

ユーザー モードのプログラマは、オブジェクトは、間接参照を通じてのみを参照できますを使用して、*処理*します。 オブジェクトの名前が、ユーザー モードでのハンドルを取得するのにことを使用できます。 ハンドルの詳細については、次を参照してください。[オブジェクト ハンドル](object-handles.md)します。

カーネル モードのオブジェクトでは、非常に特定のライフ サイクルがあります。 オブジェクトのライフ サイクルの詳細については、次を参照してください。[オブジェクトのライフ サイクル](life-cycle-of-an-object.md)します。

オブジェクトのセキュリティは、カーネル モードのプログラミングの主な問題です。 オブジェクトのセキュリティの詳細については、次を参照してください。[オブジェクト セキュリティ](object-security.md)します。

カーネル モードの環境は、仮想ディレクトリのシステムでは、オブジェクトの名前空間とも呼ばれるオブジェクトを格納します。 これにより、親の階層的な方法でアクセスできるオブジェクトと子オブジェクト。 この名前空間は、ディレクトリのファイル システムのセットに似ていますが、コンピューターに特定のファイル システムに対応して一致しません。 オブジェクトのディレクトリの詳細については、次を参照してください。[オブジェクト ディレクトリ](object-directories.md)します。

 

 




