---
title: プリンター ディレクトリ サービスの印刷スプーラー サポート
description: プリンター ディレクトリ サービスの印刷スプーラー サポート
ms.assetid: 23cd73a5-8628-4471-a6c6-e056536fcc75
keywords:
- ディレクトリ サービスの WDK プリンター
- 印刷スプーラー ディレクトリ サービスは、WDK をサポートします。
- WDK のプリンターを公開
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 170dc2f1756fbea5763d073cd001bed8bc3013e1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372076"
---
# <a name="print-spooler-support-for-printer-directory-services"></a>プリンター ディレクトリ サービスの印刷スプーラー サポート





Windows 2000 と印刷スプーラーを後では、ディレクトリ サービスから成るをサポートします。

-   印刷キューを公開します。

-   次の 3 つのレジストリ キーの管理。

-   スプーラで維持されるレジストリ キーへのアクセスを許可します。

-   印刷キューのパブリケーションの状態を返します。

### <a href="" id="ddk-publishing-print-queues-gg"></a>印刷キューの発行

**SetPrinter** Microsoft Windows SDK ドキュメントに記載されている関数には、発行、発行の取り消し、または印刷キューのオブジェクトを更新する呼び出し元ができるようにします。 これらの目的で、 **SetPrinter**プリンターの入力の構造を持つ関数を呼び出す必要があります\_情報\_7。

ユーザーが接続されているプリント サーバーを記述しているコンピューター オブジェクトに関連付けられている場合にのみ、印刷キューのオブジェクトをパブリッシュできます。 印刷キューを公開するユーザーの機能は、ユーザーのクライアントのセキュリティ コンテキストに含まれていると、自分のアクセス権によって決定されます。 印刷キューでプリンターの管理権限がある場合は、印刷キューを公開できます。

### <a href="" id="ddk-maintaining-three-registry-keys-gg"></a>次の 3 つのレジストリ キーの管理

次の 3 つのレジストリ キーには、印刷キューのオブジェクトで公開されているすべての情報のコピーが含まれます。 Winspool.h で定義されている、次の識別子を使用して 3 つのキーが参照されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Key</th>
<th>定義</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SPLDS_DRIVER_KEY</p></td>
<td><p>ドライバー固有の情報を格納するため、スプーラーまたはドライバーに指定することができます。</p></td>
</tr>
<tr class="even">
<td><p>SPLDS_SPOOLER_KEY</p></td>
<td><p>スプーラが提供するスプーラーに固有の情報を格納します。</p></td>
</tr>
<tr class="odd">
<td><p>SPLDS_USER_KEY</p></td>
<td><p>アプリケーションによって提供される、ユーザー固有の情報を格納します。</p></td>
</tr>
</tbody>
</table>

 

スプーラは SPLDS\_ドライバー\_キー ストアの Microsoft Windows SDK を呼び出して取得できるドライバー機能を**DeviceCapabilities**関数。 ドライバーは」の説明に従って、スプーラーを取得できないドライバーの機能を格納する責任を負います[ディレクトリ サービスのプリンターのプリンター ドライバーのサポート](printer-driver-support-for-printer-directory-services.md)します。 これらのキーの下に格納されている値を識別する必要があります**SPLDS\_**-winspool.h で定義されている定数をプレフィックスとして付加されます。

スプーラーは印刷キュー オブジェクトが更新された最終時刻以降では、これらのキー値に変更されたを追跡します。 スプーラーを発行または印刷キューのオブジェクトを更新するたびに、すべての変更後の値オブジェクトにコピーします。

### <a href="" id="ddk-allowing-access-to-spooler-maintained-registry-keys-gg"></a>スプーラで維持されるレジストリ キーへのアクセスを許可します。

スプーラーにより呼び出すことによって、次の 3 つのスプーラーで維持されるレジストリ キーにアクセスするプリンター ドライバー、 **SetPrinterDataEx**、 **GetPrinterDataEx**と**EnumPrinterDataEx**、Microsoft Windows SDK ドキュメントに記載されているすべての関数。 **SetPrinterDataEx**関数は、キーの下の値を設定中に**GetPrinterDataEx**と**EnumPrinterDataEx**現在値を返します。 (ドライバーでは、SPLDS の下の値を設定しないでください\_スプーラー\_キーのキー)。これらの関数の呼び出し元は、レジストリの完全なパスを指定しません。関数は、指定した印刷キューのレジストリ エントリへのパスを自動的に決定します。

### <a href="" id="ddk-returning-a-print-queues-publication-state-gg"></a>印刷キューのパブリケーションの状態を返します

**GetPrinter** Microsoft Windows SDK ドキュメントに記載されている関数には、印刷キューが現在パブリッシュされているかどうかを判断する呼び出し元ができるようにします。 この目的で、 **GetPrinter**プリンターの入力の構造を持つ関数を呼び出す必要があります\_情報\_7。 関数は、印刷キューのパブリケーションの状態 (公開または非公開) を返しますと、オブジェクト識別子。

前に説明したすべての関数は、Windows SDK のドキュメントで説明します。 関数は、専用の DS 関連の操作は使用されません。

 

 




