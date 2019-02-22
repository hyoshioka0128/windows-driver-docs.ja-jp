---
title: ネットワークの INF ファイルで DDInstall セクション
description: ネットワークの INF ファイルで DDInstall セクション
ms.assetid: f6621796-0d1f-4d96-9850-720718e7ac44
keywords:
- INF ファイルの WDK ネットワーク、DDInstall セクション
- ネットワーク INF ファイル、WDK DDInstall セクション
- DDInstall セクション WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce4968d47102e892fcc91b476044dfd0ab473c6c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553705"
---
# <a name="ddinstall-section-in-a-network-inf-file"></a>ネットワークの INF ファイルで DDInstall セクション





A *DDInstall*ネットワーク INF ファイルのセクションは、ジェネリックに基づきます[ **INF DDInstall セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547344)します。

A *DDInstall*ネットワーク INF ファイルでセクションが次のネットワークに固有のエントリには。

-   [特性](#characteristics)
-   [BusType](#bustype)
-   [Port1DeviceNumber と Port1FunctionNumber](#port1devicenumber-and-port1functionnumber)

### <a name="characteristics"></a>特性

各*DDInstall*ネットワーク INF ファイルのセクションがあります、**特性**エントリ。 **特性**エントリがインストールされているネットワーク コンポーネントの特定の特性を指定し、そのコンポーネントに関するユーザーの操作を制限することができます。 たとえば、**特性**エントリは、コンポーネントがユーザー インターフェイスをサポートするかどうか、かどうか削除する、またはユーザーから非表示かどうかを指定できます。

**特性**(複数の値がまとめて合計されます)、次の値の 1 つ以上のエントリを持つことができます。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">16 進値</th>
<th align="left">名前</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1</p></td>
<td align="left"><p>NCF_VIRTUAL</p></td>
<td align="left"><p>コンポーネントは、仮想アダプターです。 デバイスは、PCI バスや、USB などの物理バスではなくが、ルート バス上します。 このフラグは、Net のデバイス セットアップ クラスを使用するドライバーに適用のみ。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2</p></td>
<td align="left"><p>NCF_SOFTWARE_ENUMERATED</p></td>
<td align="left"><p>コンポーネントは、ソフトウェアで列挙されるアダプターです。 このフラグは、Net のデバイス セットアップ クラスを使用するドライバーに適用のみ。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x4</p></td>
<td align="left"><p>NCF_PHYSICAL</p></td>
<td align="left"><p>コンポーネントは、ドライバーが (たとえば、PCI バス) を介して直接通信する物理アダプターまたは間接的に (たとえば、USB 経由)。</p>
<p>このオプションのドライバーが物理ネットワーク インターフェイス。 a ケこのフラグをサポートしている場合はのみに適用 Net デバイス セットアップ クラスを使用してドライバーを選択します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x8</p></td>
<td align="left"><p>NCF_HIDDEN</p></td>
<td align="left"><p>コンポーネントは、任意のユーザー インターフェイスに表示しません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x10</p></td>
<td align="left"><p>NCF_NO_SERVICE</p></td>
<td align="left"><p>コンポーネントには、関連付けられているサービス (デバイス ドライバー) はありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x20</p></td>
<td align="left"><p>NCF_NOT_USER_</p>
<p>リムーバブル</p></td>
<td align="left"><p>(たとえば、コントロール パネルか、またはデバイス マネージャー) を通じて、ユーザーがコンポーネントを削除できません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x80</p></td>
<td align="left"><p>NCF_HAS_UI</p></td>
<td align="left"><p>コンポーネントは、ユーザー インターフェイス (たとえば、高度なページまたはカスタム プロパティ シート) をサポートします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x400</p></td>
<td align="left"><p>NCF_FILTER</p></td>
<td align="left"><p>コンポーネントは、中間フィルター ドライバーです。  Windows 10 以降、中間のフィルター ドライバーはサポートされていません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x4000</p></td>
<td align="left"><p>NCF_NDIS_PROTOCOL</p></td>
<td align="left"><p>コンポーネントが必要にバインディング エンジンによって提供されるアンロード イベント、 <strong>NetTrans</strong>デバイス セットアップ クラス (通常を使用する中間ドライバーをフィルターで使用される、 <strong>NetService</strong>デバイスのセットアップクラスの場合)。</p></td>
</tr>
</tr>
<tr class="even">
<td align="left"><p>0x40000</p></td>
<td align="left"><p>NCF_LW_FILTER</p></td>
<td align="left"><p>コンポーネントは、ライトウェイト フィルター ドライバーです。  このフラグは、NetService デバイス セットアップ クラスを使用するドライバーに適用のみ。</p></td>
</tr>
</tbody>
</table>

 

¹When Windows Server 2012 R2 を使用して、システム上の少なくとも 1 つのネットワーク インターフェイスと共に設定されなければなりません NCF\_DHCPv6 クライアントの条件に適合するために物理です。

次の組み合わせ**特性**値は許可されません。

-   NCF\_仮想、NCF\_ソフトウェア\_列挙、および NCF\_物理は相互に排他的です。 

-   NCF\_いいえ\_NCF でサービスを使用することはできません\_仮想、NCF\_ソフトウェア\_列挙、または NCF\_物理です。 仮想または物理、ソフトウェアで列挙されるアダプターには、関連付けられているサービス (デバイス ドライバー) が常に必要です。

例を次に、**特性**ユーザー インターフェイスをサポートする物理アダプターのエントリ。

```INF
Characteristics = 0x84; NCF_PHYSICAL, NCF_HAS_UI
```

### <a name="bustype"></a>BusType

A *DDInstall*セクションは、物理ネットワーク アダプターを含める必要があります、 **BusType**でアダプターが機能できます (PCI ISA など) のバスの種類を指定するエントリ。 使用可能な値を**BusType**エントリは、インターフェイスで指定された\_NDIS ヘッダー ファイル (ndis.h) で列挙型を次のように入力します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">BusType Entry</th>
<th align="left">Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>ISA</p></td>
<td align="left"><p>1</p></td>
</tr>
<tr class="even">
<td align="left"><p>EISA</p></td>
<td align="left"><p>2</p></td>
</tr>
<tr class="odd">
<td align="left"><p>マイクロ チャネル</p></td>
<td align="left"><p>3</p></td>
</tr>
<tr class="even">
<td align="left"><p>湧かない</p></td>
<td align="left"><p>4</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PCIBus</p></td>
<td align="left"><p>5</p></td>
</tr>
<tr class="even">
<td align="left"><p>VMEbus</p></td>
<td align="left"><p>6</p></td>
</tr>
<tr class="odd">
<td align="left"><p>通常</p></td>
<td align="left"><p>7</p></td>
</tr>
<tr class="even">
<td align="left"><p>PCMCIABus</p></td>
<td align="left"><p>8</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Cbus</p></td>
<td align="left"><p>9</p></td>
</tr>
<tr class="even">
<td align="left"><p>MPIBus</p></td>
<td align="left"><p>10</p></td>
</tr>
<tr class="odd">
<td align="left"><p>MPSABus</p></td>
<td align="left"><p>11</p></td>
</tr>
<tr class="even">
<td align="left"><p>PNPISABus</p></td>
<td align="left"><p>14</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PNPBus</p></td>
<td align="left"><p>15</p></td>
</tr>
</tbody>
</table>

 

**注**  アダプター バスの 2 つ以上の型で機能する場合は、そのアダプターをインストールする INF ファイルを含める必要があります、 *DDInstall*バスの種類ごとのセクション。

 

などの場合は、アダプターが ISA バスと PnPISA バスの両方で機能する INF ファイルをそのアダプターを含める必要があります、 *DDInstall*の ISA セクションと*DDInstall* PnPISA のセクション。 **BusType**でこれらの各エントリ*DDInstall*セクションでは、そのセクションの該当するバスの種類を次のように指定する必要があります。

```INF
[a1.isa]
BusType=1
 
[a1.pnpisa]
BusType=14
```

### <a name="port1devicenumber-and-port1functionnumber"></a>Port1DeviceNumber と Port1FunctionNumber

*DDInstall*マルチポートのネットワーク アダプターをインストールする INF ファイルのセクションでは、いずれかを含める必要があります、 **Port1DeviceNumber**エントリまたは**Port1FunctionNumber**エントリ。 このようなエントリを指定すると、アダプターのポート情報に表示される、**接続プロパティ** ダイアログ ボックス (を通じてアクセスされる、**ネットワーク**と**ダイアル アップ接続**フォルダー) アダプターの名前またはアイコンを選択するとします。

-   アダプターのポート番号は、PCI デバイス番号を順番にマップする場合は、使用、 **Port1DeviceNumber**エントリ。 設定**Port1DeviceNumber**シーケンスの最初の PCI デバイス数にします。 たとえば、PCI デバイス番号 4 ポート 1 にマップされる場合、ポート 2 に PCI デバイス数 5 マップ、PCI デバイス数 6 は、ポート 3、およびなどにマップされます、次のエントリを使用します。
    ```INF
    Port1DeviceNumber = 4
    ```

-   アダプターのポート番号は、PCI 関数の番号を順番にマップする場合は、使用、 **Port1FunctionNumber**エントリ。 設定**Port1FunctionNumber**シーケンスでは、最初の PCI 関数番号にします。 たとえば、PCI 関数番号 2 は、ポート 1 にマップして、ポート 2 などのポート 3、および PCI 関数番号 4 マップに PCI 関数番号 3 のマップは、次のエントリを使用します。
    ```INF
    Port1FunctionNumber = 2
    ```

**注**  PCI デバイス番号またはポート番号に PCI 関数のマッピングが静的であると見なされます。 また、アダプターのポートが順番に番号が付いている前提とします。

 

**Port1DeviceNumber**と**Port1FunctionNumber**エントリは相互に排他的です。 両方のエントリが存在する場合、指定された*DDInstall*セクションで、のみ、 **Port1DeviceNumber**エントリを使用します。

 

 





