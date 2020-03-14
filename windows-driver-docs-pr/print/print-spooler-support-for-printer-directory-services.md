---
title: プリンター ディレクトリ サービスの印刷スプーラー サポート
description: プリンター ディレクトリ サービスの印刷スプーラー サポート
ms.assetid: 23cd73a5-8628-4471-a6c6-e056536fcc75
keywords:
- ディレクトリサービス WDK プリンター
- 印刷スプーラディレクトリサービスサポート WDK
- WDK プリンターの発行
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 170dc2f1756fbea5763d073cd001bed8bc3013e1
ms.sourcegitcommit: b316c97bafade8b76d5d3c30d48496915709a9df
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79242981"
---
# <a name="print-spooler-support-for-printer-directory-services"></a>プリンター ディレクトリ サービスの印刷スプーラー サポート





ディレクトリサービスの Windows 2000 以降の印刷スプーラのサポートは次のもので構成されます。

-   印刷キューを公開しています。

-   3つのレジストリキーを保持する。

-   スプーラによって維持されるレジストリキーへのアクセスを許可します。

-   印刷キューのパブリケーション状態を返します。

### <a href="" id="ddk-publishing-print-queues-gg"></a>印刷キューの公開

Microsoft Windows SDK のドキュメントで説明されている**Setprinter**関数を使用すると、呼び出し元は印刷キューオブジェクトを発行、発行解除、または更新できます。 このため、 **setprinter**関数は、プリンタ\_INFO\_7 の入力構造を使用して呼び出す必要があります。

印刷キューオブジェクトを公開できるのは、ユーザーが接続されているプリントサーバーを記述するコンピュータオブジェクトに関連付けられている場合のみです。 ユーザーが印刷キューを公開できるかどうかは、ユーザーのクライアントのセキュリティコンテキストに含まれるアクセス権によって決まります。 印刷キューに対する "プリンターの管理" アクセス許可を持っている場合は、印刷キューを公開できます。

### <a href="" id="ddk-maintaining-three-registry-keys-gg"></a>3つのレジストリキーの保持

3つのレジストリキーには、印刷キューオブジェクトに公開されているすべての情報のコピーが含まれます。 この3つのキーは、winspool で定義されている次の識別子を使用して参照されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Key</th>
<th>Definition</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SPLDS_DRIVER_KEY</p></td>
<td><p>ドライバー固有の情報を格納するために使用します。この情報は、スプーラまたはドライバーによって提供されます。</p></td>
</tr>
<tr class="even">
<td><p>SPLDS_SPOOLER_KEY</p></td>
<td><p>スプーラによって提供されるスプーラ固有の情報を格納します。</p></td>
</tr>
<tr class="odd">
<td><p>SPLDS_USER_KEY</p></td>
<td><p>アプリケーションによって提供されるユーザー固有の情報を格納します。</p></td>
</tr>
</tbody>
</table>

 

スプーラは、DeviceCapabilities ドライバー\_キーを\_使用して、Microsoft Windows SDK **DeviceCapabilities**関数を呼び出すことによって取得できるドライバーの機能を格納します。 ドライバーは、「プリンター[ドライバーでのプリンターディレクトリサービスのサポート](printer-driver-support-for-printer-directory-services.md)」で説明されているように、スプーラが取得できないドライバー機能を格納する役割を担います。 これらのキーの下に格納される値は、winspool. h で定義されている、 **\_** プレフィックス付き定数で識別する必要があります。

スプーラは、最後に印刷キューオブジェクトが更新されてから、これらのキーの下にあるどの値が変更されたかを追跡します。 スプーラが印刷キューオブジェクトを公開または更新するたびに、変更されたすべての値がオブジェクトにコピーされます。

### <a href="" id="ddk-allowing-access-to-spooler-maintained-registry-keys-gg"></a>スプーラによって維持されるレジストリキーへのアクセスを許可する

スプーラを使用すると、プリンタードライバーは、 **Setprinter dataex**、 **getprinter dataex** 、および**enumprinter dataex**の各関数を呼び出すことによって、3つのスプーラで保持されるレジストリキーにアクセスできるようになります。これらの機能については、Microsoft Windows SDK のドキュメントを参照してください。 **Setプリンター dataex**関数は、キーの下に値を設定します。 **getプリンター Dataex**および**enumプリンター dataex**は、現在の値を返します。 (ドライバーでは、\_スプーラ\_キーキーの下に値を設定しないでください)。これらの関数の呼び出し元は、完全なレジストリパスを指定していません。関数は、指定された印刷キューのレジストリエントリへのパスを自動的に決定します。

### <a href="" id="ddk-returning-a-print-queues-publication-state-gg"></a>印刷キューのパブリケーション状態を返す

Microsoft Windows SDK ドキュメントに記載されている**Getprinter**関数を使用すると、印刷キューが現在発行されているかどうかを呼び出し元が判断できます。 このため、 **getprinter**関数は、プリンタ\_INFO\_7 の入力構造を使用して呼び出す必要があります。 関数は、印刷キューのパブリケーションの状態 (公開またはパブリッシュされていない) とオブジェクト識別子を返します。

前述のすべての関数については、Windows SDK のドキュメントを参照してください。 関数は、DS 関連の操作専用に使用されません。

 

 




