---
title: ポート モニター
description: ポート モニター
ms.assetid: 4758ebda-f93e-49fb-8605-17cf43194afc
keywords:
- WDK 印刷モニターは、ポートを監視します。
- ポート モニター WDK を印刷します。
- WDK のポート モニターを印刷するポート モニタについて
- WDK のポート モニターを印刷する Dll
- 印刷キュー、WDK ポート モニター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d09bfdd9c4dd0b707298aa3c8ae68804754fba37
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331782"
---
# <a name="port-monitors"></a>ポート モニター





ポート モニターは、ユーザー モード Dll で構成されます。 ユーザー モードの印刷スプーラーと I/O ポートのハードウェアにアクセスするポートのカーネル モードのドライバーの間の通信パスを提供する責任を負います。 ポートを使用して監視通常、 [ **CreateFile**](https://msdn.microsoft.com/library/windows/desktop/aa363858)、 **WriteFile**、 **ReadFile**、および**DeviceIOControl**関数、ポートのカーネル モード ドライバーとの通信に、Microsoft Windows SDK ドキュメントに記載します。 ポート モニターも担当の管理と、サーバーのプリンター ポートの構成」の説明に従って[管理ポート](managing-a-port.md)します。

「プリンター」の NT-ベースのオペレーティング システム ユーザーのビューは、1 つまたは複数の物理プリンター デバイスを接続できる、印刷キューでは本当に。 ポートは、印刷キューとプリンター 1 台のデバイス間の物理的な接続です。 各ポート モニターは、1 つまたは複数の種類のポートの 1 つまたは複数のインスタンスをサポートします。 たとえばの Localmon.dll、[サンプル ポート モニター](sample-port-monitor.md)、すべてのサーバーのローカル COM と LPT ポートをサポートできます。 (印刷フォルダーによってポート モニターを呼び出して、Windows SDK ドキュメントのポートが割り当てられます**AddPrinter**関数です。)。

印刷キューの複数のプリンター デバイス (を通じて複数のポート) を表す場合は、スプーラーは、最初の使用可能なポートに各印刷ジョブを送信します。 ポート モニターには、指定したポートがビジー状態か、エラーが発生しましたが示されている場合、ポート モニターでサポートされている別のポートを指定して、キューにジョブが、スプーラーに再送信します。

Localmon.dll、だけでなく、Windows 2000 と以降のオペレーティング システム バージョンは、いくつかの追加のポート モニターを提供します。 *Windows 2000 Server Resource Kit*これらのポート モニターのそれぞれについて説明します。 (このリソースできない場合がありますのいくつかの言語および国。)

カスタマイズされたポート モニタは、I/O ポートのハードウェアの他の種類をサポートするために記述できます。

Windows 2000 以降では、各ポート モニターが 2 つの Dll に分かれています。

<a href="" id="port-monitor-ui-dll-"></a>**ポート モニター UI DLL**   
ポート モニターのユーザー インターフェイス DLL は、ユーザー インターフェイスの機能が含まれていて、印刷クライアント システムで実行します。

この DLL は、クライアント システムの System32 サブディレクトリ内に存在する必要があります。

<a href="" id="port-monitor-server-dll-"></a>**ポート監視のサーバー DLL**   
ポート モニターのサーバー DLL では、ポートの通信機能が含まれていて、プリント サーバー上で実行します。 ユーザー インターフェイスは表示しないでください。

UI の DLL が、スプーラーを呼び出すことによって、サーバー DLL と通信する[ **XcvData** ](https://msdn.microsoft.com/library/windows/hardware/ff564255)関数。

A[サンプル ポート モニター](sample-port-monitor.md) Windows Driver Kit (WDK) では含まれています。

 

 




