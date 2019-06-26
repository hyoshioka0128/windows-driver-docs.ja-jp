---
title: Hyper-V 拡張可能スイッチ拡張機能の INF 要件
description: Hyper-V 拡張可能スイッチ拡張機能の INF 要件
ms.assetid: 378F619A-C799-4330-A388-9955A67251F8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 74230af31314fd6d9b3fd12f9959aaa80bab6b7f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385097"
---
# <a name="inf-requirements-for-hyper-v-extensible-switch-extensions"></a>Hyper-V 拡張可能スイッチ拡張機能の INF 要件


HYPER-V 拡張可能スイッチの拡張機能は、NDIS フィルター ドライバーとして開発されています。 その結果、拡張機能の INF 要件は、すべての NDIS フィルター ドライバーの INF 要件に基づいています。 拡張可能スイッチの拡張機能の INF ファイルを作成するときに、変更、または監視フィルター ドライバーの INF 設定を使用する必要があります。 これらの設定の詳細については、次を参照してください。[フィルター ドライバーの INF ファイルの設定](inf-file-settings-for-filter-drivers.md)します。

さらに、拡張可能スイッチの拡張機能の INF ファイルの次のガイドラインを従う必要があります。

- 拡張可能スイッチの拡張機能は、変更、フィルター ドライバーとしてインストールする必要があります。

  変更フィルター ドライバーの INF 要件の詳細については、次を参照してください。[変更フィルター ドライバーの INF ファイルを構成する](configuring-an-inf-file-for-a-modifying-filter-driver.md)します。

  **注**のフィルター クラスを使用して拡張機能**ms\_切り替える\_キャプチャ**監視フィルター ドライバーと同じタスクを実行できます。 詳細については、次を参照してください。[型のフィルター ドライバー](types-of-filter-drivers.md)します。

     

- **FilterMediaTypes**フィルター INF ファイルのエントリは、他のドライバーやインターフェイスに、ドライバーのバインドを定義します。 **FilterMediaTypes**拡張可能スイッチの拡張機能のエントリを含める必要があります、 **vmnetextension**値。 この値は、拡張可能スイッチ拡張機能のミニポート アダプターへのバインドを指定します。

  **FilterMediaTypes**エントリを指定するメディアの種類のコンマ区切りのリストを使用します。 これにより、物理インターフェイスまたは拡張可能スイッチのインターフェイスにバインドする拡張機能です。

  次の例は、 **FilterMediaTypes**物理イーサネット ネットワーク アダプターまたは拡張可能スイッチの仮想ネットワーク アダプターのいずれかにバインドする拡張機能を許可するエントリ。

  ```INF
  HKR, Ndi\Interfaces, FilterMediaTypes, , "ethernet, vmnetextension"
  ```

  場合、 **FilterMediaTypes**エントリのみを指定します。、 **vmnetextension**値、拡張機能は、システム上のすべての拡張可能スイッチのドライバー スタックにバインドのみです。

  場合、 **FilterMediaTypes**エントリを指定します**vmnetextension**拡張機能や他のメディアの種類としてを呼び出すことによって、拡張可能スイッチドライバースタック内でバインドされているかどうかを判断できます[ **NdisFGetOptionalSwitchHandlers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfgetoptionalswitchhandlers)します。 関数は、NDIS を返す場合\_状態\_成功すると、拡張機能は、拡張機能ドライバー スタック内でバインドします。 関数は、NDIS を返す場合\_状態\_いない\_、サポートされている拡張機能が、別の物理ネットワーク インターフェイスのドライバー スタック内でバインドします。

  詳細については、 **FilterMediaTypes**エントリを参照してください[中間ドライバー UpperRange と LowerRange INF ファイルのエントリ](intermediate-driver-upperrange-and-lowerrange-inf-file-entries.md)します。

- **FilterClass** INF ファイルで値の拡張機能は、フィルターのスタック内での順序を決定します。 **FilterClass**エントリには、次の表の値の 1 つ含める必要があります。

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
  <td align="left"><p>このクラスの拡張機能は、パケットのトラフィックを監視します。 ただし、このクラスの拡張機能は、ポート ポリシーを適用またはパケットの宛先ポートを変更することはできません。</p>
  <p>このクラスの拡張機能の詳細については、次を参照してください。<a href="capturing-extensions.md" data-raw-source="[Capturing Extensions](capturing-extensions.md)">キャプチャ拡張機能</a>します。</p></td>
  </tr>
  <tr class="even">
  <td align="left"><p><strong>ms_switch_filter</strong></p></td>
  <td align="left"><p>このクラスの拡張機能では、パケットのトラフィックをフィルター処理し、拡張可能スイッチ経由のパケット配送のポートやスイッチのポリシーを適用します。 このクラスのドライバーを検査し、ポリシー設定に基づき、各パケットの宛先ポートを削除することもできます。</p>
  <p>このクラスの拡張機能の詳細については、次を参照してください。<a href="filtering-extensions.md" data-raw-source="[Filtering Extensions](filtering-extensions.md)">拡張機能のフィルタ リング</a>します。</p></td>
  </tr>
  <tr class="odd">
  <td align="left"><p><strong>ms_switch_forward</strong></p></td>
  <td align="left"><p>このクラスの拡張機能と同じ機能を持つ、 <strong>ms_switch_filter</strong>クラス。 このクラスの拡張機能のことができますも他の拡張可能スイッチ ポートにパケットを転送するだけでなく任意の拡張可能スイッチ ポートにパケット トラフィックを挿入します。</p>
  <p>イングレス データ パスで、このクラスの拡張機能が後に呼び出され、 <strong>ms_switch_filter</strong>拡張機能のクラス。 エグレス データ パスで、このクラスの拡張機能は前に呼び出さ、 <strong>ms_switch_filter</strong>拡張機能のクラス。</p>
  <p>このクラスの拡張機能の詳細については、次を参照してください。<a href="forwarding-extensions.md" data-raw-source="[Forwarding Extensions](forwarding-extensions.md)">転送拡張機能</a>します。</p>
  <div class="alert">
  <strong>注</strong>拡張可能スイッチのドライバー スタックでこのクラスの拡張機能を 1 つだけが許可されています。
  </div>
  <div>
     
  </div></td>
  </tr>
  </tbody>
  </table>

     

これらの INF 設定で、拡張機能のインストール時は、すべての拡張可能スイッチのインスタンスにバインドする構成されます。 ただし、バインディングを使用しては無効になります、PowerShell コマンドレットで明示的に有効にする必要があります。 この手順の詳細については、次を参照してください。[の有効化の Hyper-v 拡張可能スイッチの拡張](enabling-hyper-v-extensibility-switch-extensions.md)します。

 

 





