---
title: ネットワーク INF ファイル内の Version セクション
description: ネットワーク INF ファイル内の Version セクション
ms.assetid: c76151e9-fef2-4bfe-8587-d58d95d234bc
keywords:
- INF ファイルの WDK ネットワーク、バージョン セクション
- ネットワーク INF ファイルにバージョン セクション
- バージョン セクション WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb813db3c53693f66f49abe8aa064b967db88025
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384357"
---
# <a name="version-section-in-a-network-inf-file"></a>ネットワーク INF ファイル内の Version セクション





**バージョン**ネットワーク INF ファイルのセクションは、ジェネリックに基づきます[ **INF バージョン セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-version-section)します。

**バージョン**ネットワーク INF ファイルでセクションが次のネットワークに固有のエントリには。

-   [Class](#class)
-   [ClassGuid](#classguid)
-   [署名とオペレーティング システム エントリ](#signature-and-operating-system-entries)
-   [PnpLockDown](#pnplockdown)
-   [CatalogFile](#catalogfile)
-   [バージョン セクションの例](#version-section-example)

### <a name="class"></a>クラス

**バージョン**セクションを含める必要があります、**クラス**エントリ ファイルがインストールされているネットワーク コンポーネントのクラスを識別します。

これには 4 つのネットワーク クラスがあります。

<a href="" id="net"></a>**Net**  
物理または仮想ネットワーク アダプターを指定します。 Net クラスでは、仮想ネットワーク アダプターをエクスポートするには、NDIS 中間ドライバが含まれます。

<a href="" id="nettrans"></a>**NetTrans**  
TCP/IP、IPX、接続指向のクライアントでは、接続指向のコール マネージャーなどのネットワーク プロトコルを指定します。

<a href="" id="netclient"></a>**NetClient**  
ネットワークや NetWare クライアント用の Microsoft クライアントなどのネットワーク クライアントを指定します。 ネットワーク クライアント コンポーネントはネットワーク プロバイダーであると見なされます、印刷プロバイダーであるも考慮ネットワーク経由で印刷サービスを提供する場合。

**注**  **NetClient**コンポーネントは Windows 8.1、Windows Server 2012 R2 で非推奨以降。

 

<a href="" id="netservice"></a>**NetService**  
ファイル サービスや印刷サービスなどのネットワーク サービスを指定します。

**注**  赤外線 Data Association (IrDA) 準拠のデバイスは、前の 4 つのネットワーク クラスのいずれかに分類されないネットワーク クラスのインストーラーによってこれらがインストールされている場合でもです。 IrDA デバイスのインストールに使用される INF ファイルである必要があります、 **クラス** @property **赤外線**します。 このクラスには、シリアル IR と高速 IR の両方のデバイスが含まれています。

 

**注**  から (Windows 8) の NDIS 6.30 以降 IrDA ミニポート ドライバーのサポートは削除されました。

 

### <a name="classguid"></a>ClassGuid

**バージョン**セクションを含める必要があります、 **ClassGuid**エントリ。 ネットワーク クラスのインストーラーを使用して、 **ClassGuid**エントリをインストールされているネットワーク コンポーネントのクラスを判別します。

次の 4 つのネットワークがある**ClassGuid**ネットワーク クラスに対応するそれぞれの値。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ネットワーク クラス</th>
<th align="left">ClassGuid</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Net</strong></p></td>
<td align="left"><p>{4D36E972-E325-11CE-BFC1-08002BE10318}</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>NetTrans</strong></p></td>
<td align="left"><p>{4D36E975-E325-11CE-BFC1-08002BE10318}</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>NetClient</strong></p></td>
<td align="left"><p>{4D36E973-E325-11CE-BFC1-08002BE10318}</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>NetService</strong></p></td>
<td align="left"><p>{4D36E974-E325-11CE-BFC1-08002BE10318}</p></td>
</tr>
</tbody>
</table>

 

デバイスの IrDA INF ファイルをする必要がありますが、 **ClassGuid**の値

{6bdd1fc5 81-d 0-bec7-08002be2092f}。

### <a name="signature-and-operating-system-entries"></a>署名とオペレーティング システム エントリ

**署名**エントリである必要があります **$Windows NT$** します。

### <a name="pnplockdown"></a>PnpLockDown

**PnpLockDown**エントリは、アプリケーションがドライバー パッケージの INF ファイルを指定するファイルを直接変更するを防ぐに 1 に設定する必要があります。 このエントリの詳細については、次を参照してください。 [ **INF バージョン セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-version-section)します。

### <a name="catalogfile"></a>CatalogFile

**CatalogFile**エントリを使用して、省略可能なドライバーによって提供される .cat ファイルを宣言します。 詳細については、のベンダーから提供されたファイルのセクションを参照してください。[コンポーネントとネットワーク コンポーネントのインストールに使用されるファイル](components-and-files-used-for-network-component-installation.md)します。

### <a name="version-section-example"></a>バージョン セクションの例

例を次に、**バージョン**ネットワーク アダプターをインストールする INF ファイルのセクション。

```INF
[Version]
Signature = $Windows NT$
Class=Net
ClassGuid = {4D36E972-E325-11CE-BFC1-08002BE10318}
Provider = %Msft%
DriverVer=06/22/2010,6.1.7065.0
PnpLockDown = 1
CatalogFile = netvmini630.cat
```

**注**   、**プロバイダー**エントリが、開発者は、INF ファイルによってインストールされたコンポーネントの開発者ではなく、INF ファイルのことを示します。

 

 

 





