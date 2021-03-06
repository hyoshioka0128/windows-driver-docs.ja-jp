---
title: 印刷プロバイダーの概要
description: 印刷プロバイダーの概要
ms.assetid: a0e5e8c8-7af4-4715-9036-64ae851b307d
keywords:
- 印刷プロバイダー WDK、印刷プロバイダーについて
- WDK のジョブの印刷、印刷プロバイダー
- 印刷プロバイダー WDK、フロー パス
- OpenPrinter
- WDK のジョブの印刷、印刷プロバイダー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e43c86a73678fe6841147b08f883826224914990
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355661"
---
# <a name="introduction-to-print-providers"></a>印刷プロバイダーの概要

> [!WARNING]
> Windows 10 以降では、サード パーティの印刷プロバイダーをサポートする Api は非推奨します。 Microsoft には、サード パーティの印刷プロバイダーに他の投資はお勧めしません。 さらに、Windows 8 および v4 印刷ドライバー モデルが使用可能な新しい製品では、サード パーティの印刷プロバイダーが作成や v4 印刷ドライバーを使用するキューを管理します。

印刷のプロバイダーは、ローカルまたはリモートの印刷デバイスに印刷ジョブの指導を担当します。 または、開始、停止、およびサーバーの印刷キューを列挙するなど、印刷キューの管理操作を担当します。 印刷のプロバイダーは、プリント サーバーの高度なマシンに依存しない、オペレーティング システムに依存しないビューを定義します。

すべての印刷プロバイダー実装の共通セットを[プロバイダーの機能を印刷](print-provider-capabilities.md)します。 これらの機能は、一連の API 関数は、スプーラーのルーター (Spoolss.dll) によって呼び出されるによって定義されます。

印刷プロバイダーによって定義されているほとんどの関数では、入力としてプリンター ハンドルが必要とします。 スプーラ クライアントが呼び出すことによってプリンター ハンドルを取得**ようになりました**(Microsoft Windows SDK のドキュメントで説明) Winspool.drv でを呼び出し、API サーバー (Spoolsv.exe)。 スプーラのルーター (Spoolss.dll) が各印刷プロバイダーを呼び出す**ようになりました**うち 1 つがプリンター ハンドルを提供し、印刷プロバイダーを示す戻り値が指定されたプリンター名を認識するまで、機能します。 ルーターは、API サーバーにし、独自のハンドルを返します。 ルーターのハンドルには、プリンター ハンドルとプロバイダーのハンドルの両方が含まれています。 このハンドルは、アプリケーションからの後続の呼び出しは、適切なプロバイダーやプリンターに向けることができるように、アプリケーションに返されます。

マイクロソフトは、次の Windows 2000 以降のプロバイダーの印刷を提供します。

**Localspl.dll**  
[ローカルの印刷プロバイダー](local-print-provider.md)します。 ローカル サーバーから管理されているプリンターに送信されるすべての印刷ジョブを処理します。

**Win32spl.dll**  
Windows ネットワーク印刷プロバイダー。 ハンドルの印刷ジョブのリモート Win32 に送られます (NT-ベースのオペレーティング システムまたは Windows をワークグループの) サーバー。 リモート サーバーで、ジョブが到着すると、サーバーのローカルの印刷プロバイダーに渡されます。

**Nwprovau.dll**  
Novell NetWare の印刷プロバイダー。 ハンドルは、Novell NetWare のプリント サーバーに転送ジョブを印刷します。

**Inetpp.dll**  
HTTP の印刷プロバイダー。 ハンドルは、URL に送信されたジョブを印刷します。

ベンダーは、印刷プロバイダー、追加のネットワークを作成できます。 詳細については、次を参照してください。[ネットワーク印刷プロバイダーの記述](writing-a-network-print-provider.md)します。

次の図は、これらの印刷プロバイダーに関連するフローを可能なパスを示します。

![印刷プロバイダー フロー パス ](images/flowpths.png)

ダイアグラムを表示するときに、次の点を考慮してください。

-   によって、印刷ジョブを処理、プリンターがクライアント システムによって管理されている場合、[ローカル印刷プロバイダー](local-print-provider.md) (Localspl.dll)。 Localspl.dll によって管理されるプリンターを物理的にローカル クライアントにする必要はありません。これらは、ネットワーク カードに直接接続することができます。

-   NT-ベースのオペレーティング システムのサーバーには、プリンターが存在する場合 (Win32spl.dll) ネットワーク プロバイダーは RPC を使用して、クライアントのルーターから、サーバーの Spoolsv.exe プロセスへの呼び出しをリダイレクトします。 プリンターは、サーバーにローカルであるため、サーバーのローカルの印刷プロバイダーは、印刷ジョブを処理します。

-   プリンターが他の種類のサーバー上にある場合は、データ形式と、サーバーでサポートされるネットワーク プロトコルを使用して、そのサーバーの種類をサポートするネットワーク印刷プロバイダーやローカルの印刷プロバイダーによってアクセスできます。

-   リモート プリンターにアクセスするローカルの印刷プロバイダーを含める必要があります、[ポート モニター](https://docs.microsoft.com/windows-hardware/drivers/print/port-monitors)リモート プリンターまたはサーバーによって認識されるネットワーク プロトコルを使用することができます。
