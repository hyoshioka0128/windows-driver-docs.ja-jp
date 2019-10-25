---
title: Hyper-V 拡張可能スイッチ拡張機能の INF 要件
description: Hyper-V 拡張可能スイッチ拡張機能の INF 要件
ms.assetid: 378F619A-C799-4330-A388-9955A67251F8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 758db3f222f8a48ac864d1a96d7541f6043bc10f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824610"
---
# <a name="inf-requirements-for-hyper-v-extensible-switch-extensions"></a>Hyper-V 拡張可能スイッチ拡張機能の INF 要件


Hyper-v 拡張可能スイッチ拡張機能は、NDIS フィルタードライバーとして開発されています。 そのため、拡張機能の INF 要件は、すべての NDIS フィルタードライバーの INF 要件に基づいています。 拡張可能なスイッチ拡張機能の INF ファイルを作成する場合は、変更または監視フィルタードライバーの INF 設定を使用する必要があります。 これらの設定の詳細については、「[フィルタードライバーの INF ファイル設定](inf-file-settings-for-filter-drivers.md)」を参照してください。

また、拡張可能なスイッチ拡張機能については、次のガイドラインに従って INF ファイルを作成する必要があります。

- 拡張可能なスイッチ拡張機能は、変更フィルタードライバーとしてインストールする必要があります。

  フィルタードライバーの変更に関する INF の要件の詳細については、「[変更フィルタードライバーの Inf ファイルの構成](configuring-an-inf-file-for-a-modifying-filter-driver.md)」を参照してください。

  **メモ** フィルタークラスが**ms\_switch\_capture**の拡張機能は、監視フィルタードライバーと同じタスクを実行できます。 詳細については、「[フィルタードライバーの種類](types-of-filter-drivers.md)」を参照してください。

     

- フィルター INF ファイルの**FilterMediaTypes**エントリは、ドライバーの他のドライバーとインターフェイスへのバインドを定義します。 拡張可能なスイッチ拡張機能の**FilterMediaTypes**エントリには、 **vmnetextension**値を含める必要があります。 この値は、拡張可能スイッチ拡張機能のミニポートアダプターへのバインドを指定します。

  **FilterMediaTypes**エントリを使用すると、メディアの種類のコンマ区切りリストを指定できます。 これにより、拡張機能を物理インターフェイスまたは拡張可能なスイッチインターフェイスにバインドできます。

  次の例は、 **FilterMediaTypes**エントリを示しています。これにより、拡張機能を物理イーサネットネットワークアダプターまたは拡張可能なスイッチ仮想ネットワークアダプターのいずれかにバインドできます。

  ```INF
  HKR, Ndi\Interfaces, FilterMediaTypes, , "ethernet, vmnetextension"
  ```

  **FilterMediaTypes**エントリで**vmnetextension**値のみが指定されている場合、拡張機能は、システム上のすべての拡張可能なスイッチのドライバースタックにのみバインドします。

  **FilterMediaTypes**エントリで**vmnetextension**とその他のメディアの種類が指定されている場合、拡張機能は[**NdisFGetOptionalSwitchHandlers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfgetoptionalswitchhandlers)を呼び出すことによって拡張可能なスイッチドライバースタック内でバインドされているかどうかを判断できます。 関数が NDIS\_STATUS\_SUCCESS を返した場合、拡張機能は拡張機能のドライバースタック内でバインドされます。 関数が NDIS\_STATUS を返し\_\_サポートされていない場合、拡張機能は別の物理ネットワークインターフェイスのドライバースタック内でバインドされます。

  **FilterMediaTypes**エントリの詳細については、「[中間ドライバー UpperRange と LOWERRANGE INF ファイルのエントリ](intermediate-driver-upperrange-and-lowerrange-inf-file-entries.md)」を参照してください。

- 拡張機能の INF ファイルの**Filterclass**値によって、フィルターの順序が決定されます。 **Filterclass**エントリには、次の表のいずれかの値が含まれている必要があります。

  <table>
  <colgroup>
  <col width="50%" />
  <col width="50%" />
  </colgroup>
  <thead>
  <tr class="header">
  <th align="left">FilterClass 値</th>
  <th align="left">説明</th>
  </tr>
  </thead>
  <tbody>
  <tr class="odd">
  <td align="left"><p><strong>ms_switch_capture</strong></p></td>
  <td align="left"><p>このクラスの拡張は、パケットトラフィックを監視します。 ただし、この拡張機能のクラスでは、ポートポリシーを適用したり、パケットの宛先ポートを変更したりすることはできません。</p>
  <p>このクラスの拡張機能の詳細については、「<a href="capturing-extensions.md" data-raw-source="[Capturing Extensions](capturing-extensions.md)">拡張機能のキャプチャ</a>」を参照してください。</p></td>
  </tr>
  <tr class="even">
  <td align="left"><p><strong>ms_switch_filter</strong></p></td>
  <td align="left"><p>このクラスの拡張では、パケットトラフィックをフィルター処理し、拡張可能スイッチを介してパケットを配信するためのポートまたはスイッチポリシーを適用します。 また、このクラスのドライバーは、ポリシー設定に基づいて各パケットの宛先ポートを検査および削除することもできます。</p>
  <p>このクラスの拡張機能の詳細については、「<a href="filtering-extensions.md" data-raw-source="[Filtering Extensions](filtering-extensions.md)">拡張機能のフィルター選択</a>」を参照してください。</p></td>
  </tr>
  <tr class="odd">
  <td align="left"><p><strong>ms_switch_forward</strong></p></td>
  <td align="left"><p>このクラスの拡張には、 <strong>ms_switch_filter</strong>クラスと同じ機能があります。 この拡張機能のクラスは、他の拡張可能なスイッチポートにパケットを転送するだけでなく、任意の拡張可能なスイッチポートにパケットトラフィックを挿入することもできます。</p>
  <p>受信データパスでは、拡張機能の<strong>ms_switch_filter</strong>クラスの後に、この拡張機能のクラスが呼び出されます。 送信データパスでは、拡張機能の<strong>ms_switch_filter</strong>クラスの前にこのクラスの拡張機能が呼び出されます。</p>
  <p>このクラスの拡張機能の詳細については、「<a href="forwarding-extensions.md" data-raw-source="[Forwarding Extensions](forwarding-extensions.md)">拡張機能の転送</a>」を参照してください。</p>
  <div class="alert">
  <strong>メモ</strong> 拡張可能なスイッチドライバースタックでは、このクラスの1つの拡張のみが許可されます。
  </div>
  <div>
     
  </div></td>
  </tr>
  </tbody>
  </table>

     

これらの INF 設定を使用して拡張機能をインストールすると、拡張可能なすべてのスイッチインスタンスにバインドするように構成されます。 ただし、バインドは無効になり、PowerShell コマンドレットを使用して明示的に有効にする必要があります。 この手順の詳細については、「 [Hyper-v 拡張可能スイッチ拡張機能の有効化](enabling-hyper-v-extensibility-switch-extensions.md)」を参照してください。

 

 





