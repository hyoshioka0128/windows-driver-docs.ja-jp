---
title: UPS ServiceProviders レジストリ エントリ
description: UPS モデルごとに UPS ServiceProviders レジストリ キーの下のベンダー固有のサブキーを作成します。
ms.assetid: fa206f16-e136-4bfe-9823-7c324d62e1fb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bfe58745ac5f9ae1f3e880932914d35b6d3481d7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328425"
---
# <a name="upsserviceproviders-registry-entries"></a>UPS\\ServiceProviders レジストリ エントリ


## <span id="ddk_ups_serviceproviders_registry_entries_kg"></span><span id="DDK_UPS_SERVICEPROVIDERS_REGISTRY_ENTRIES_KG"></span>


で、 **UPS**\\**ServiceProviders**レジストリ キー、UPS ベンダーはベンダー固有サブキーを作成する必要があります。 仕入先は、このサブキーの下、UPS モデルごとにエントリを作成する必要があります。 ベンダーは、中にこれらのレジストリ エントリを作成する必要があります[UPS ミニドライバーをインストールする](installing-ups-minidrivers.md)します。

各モデルに固有のエントリは、値の名前と値で構成されます。 値の名前は、UPS モデルの名前を指定する必要があります。 この名前に関連付けられている値は、2 つの部分で構成される文字列です。

-   値の文字列の最初の部分では、モデルの機能を識別する 16 進数のビットマスクを表します。 ビット値は、次の表で定義されます。

    <table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">ビット値</th>
    <th align="left">説明</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><p>0x00000001</p></td>
    <td align="left"><p>UPS がインストールされます。</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>0x00000002</p></td>
    <td align="left"><p>UPS には、電源障害の通知がサポートされています。</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>0x00000004</p></td>
    <td align="left"><p>UPS は、バッテリ電源の通知をサポートしています。</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>0x00000008</p></td>
    <td align="left"><p>UPS は、シリアル ポートを使用してオフにすることができます。</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>0x00000010</p></td>
    <td align="left"><p>電源障害通知は、正のシグナルで示されます。</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>0x00000020</p></td>
    <td align="left"><p>バッテリ低下の通知は、正のシグナルで示されます。</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>0x00000040</p></td>
    <td align="left"><p>UPS は正のシグナルがオフになります。</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>0x00000080</p></td>
    <td align="left"><p>予約済み。 使わないでください。</p></td>
    </tr>
    </tbody>
    </table>

     

-   文字列の 2 番目の部分は省略可能です。 UPS ミニドライバーの名前とパスを表します。 このパスと名前が指定されている場合は、セミコロン (;) で前必要です。 だけの場合は、指定した名前の %systemroot% の既定のパス\\system32 を使用します。

UPS を使用して、システム管理者が有効にし、UPS ミニドライバーがインストールされたら、**電源オプション**、システムの UPS サービス モデルに固有のコピー **UPS** \\ **ServiceProviders**値は、他のシステム管理の対象のレジストリの場所。

例を次に、値の名前と 2 つの UPS モデルの値で、1 つのベンダーのサブキーの下**UPS**\\**ServiceProviders**:

``` syntax
UPS\ServiceProviders
    American Power Conversion
        Back-UPS "0x7f"
        Smart-UPS "0x1;apcups.dll"
```

 

 




