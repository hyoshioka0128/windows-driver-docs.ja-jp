---
title: EFI でのブート オプションの概要
description: EFI でのブート オプションの概要
ms.assetid: 2237d321-75e6-4723-9f08-484bd9097360
keywords:
- NVRAM ブートオプション WDK、EFI NVRAM ブートオプションについて
- EFI NVRAM ブートオプション WDK、EFI NVRAM ブートオプションについて
- グローバルに定義された変数 WDK ブートオプション
- ブートオプション WDK、変数
- ブートエントリ Id WDK
- EFI ブートエントリ Id WDK
- 識別子 WDK ブートオプション
- ブートエントリ WDK
- Bootcfg ツール
ms.date: 07/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5542f5a30344ff56fdad1ef4c68d48a77b80b7f0
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769564"
---
# <a name="overview-of-boot-options-in-efi"></a>EFI でのブート オプションの概要

BIOS ファームウェアが搭載されたシステムのブートオプションと同様に、EFI NVRAM には次の2種類のブートオプションがあります。

-   コンピューター上のすべての起動可能なデバイスと起動可能なプログラムに適用*されるグローバルに定義された変数*。

-   *ブートオプション変数*は、オペレーティングシステムなどの起動可能なデバイスまたはプログラムの特定の負荷構成にのみ適用されます。 システム固有の変数は、起動可能なデバイスまたはコンピューター上の起動可能なプログラムの各構成のブートエントリを構成します。

「 [Efi のブートオプションの編集](editing-boot-options-in-efi.md)」で説明されている[Bootcfg](https://docs.microsoft.com/windows-server/administration/windows-commands/bootcfg)ツールを使用すると、efi NVRAM のブートオプションを表示および編集できます。

次のサンプルは、Itanium プロセッサを搭載したコンピューターの Bootcfg ディスプレイを示しています。

```
Boot Options
------------
Timeout:             30
Default:             \Device\HarddiskVolume3\WINDOWS
CurrentBootEntryID:  1

Boot Entries
------------

Boot entry ID:    1
OS Friendly Name: Windows Server 2003, Enterprise
OsLoadOptions: /debug /debugport=COM1 /baudrate=57600
BootFilePath:     \Device\HarddiskVolume1\EFI\Microsoft\WINNT50\ia64ldr.efi
OsFilePath:       \Device\HarddiskVolume3\WINDOWS

Boot entry ID:    2
OS Friendly Name: EFI Shell [Built-in]
```

次の表では、EFI NVRAM でのブートデータの Bootcfg 表示の要素について説明します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">フィールド</th>
<th align="left">説明</th>
<th align="left">例</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>ブートオプション</strong></p></td>
<td align="left"><p>すべてのブートエントリに適用されるオプションが含まれています。</p></td>
<td align="left"><p>(セクション見出し)</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>タイムアウト</strong></p></td>
<td align="left"><p>ブートメニューを表示する期間を指定します。 この値が有効期限切れになると、ブートローダーによって既定のオペレーティングシステムが読み込まれます。</p></td>
<td align="left"><pre space="preserve"><code>Timeout:   30</code></pre></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>[Default]</strong></p></td>
<td align="left"><p>既定のオペレーティングシステムの場所を指定します。</p></td>
<td align="left"><pre space="preserve"><code>\Device\HarddiskVolume3\WINDOWS</code></pre></td>
</tr>
<tr class="even">
<td align="left"><p><strong>CurrentBootEntryID</strong></p></td>
<td align="left"><p>オペレーティングシステムの現在のセッションを開始するために使用されたブートエントリを識別します。</p></td>
<td align="left"><pre space="preserve"><code>CurrentBootEntryID:  1</code></pre></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ブートエントリ</strong></p></td>
<td align="left"><p>システム固有のデータを格納します。 コンピューターにインストールされているオペレーティングシステムまたは起動可能なプログラムごとに1つ以上の<em>ブートエントリ</em>から構成されます。</p>
<p><em>ブートエントリ</em>は、オペレーティングシステムまたは起動可能なプログラムの負荷構成を定義する一連のオプションです。</p></td>
<td align="left"><p>(セクション見出し)</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ブートエントリ ID</strong></p></td>
<td align="left"><p>Bootcfg に対するブートエントリを識別します。 この値は、ブートエントリの順序を変更するときに変更されます。</p>
<p>これは efi コンポーネントの永続的な識別子ではなく、 <em>efi ブートエントリ ID</em>ではありません。</p></td>
<td align="left"><pre space="preserve"><code>Boot entry ID:    1</code></pre></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>OS フレンドリ名</strong></p></td>
<td align="left"><p>ブートメニューのブートエントリを表します。</p></td>
<td align="left"><pre space="preserve"><code>Windows Server 2003,
Enterprise</code></pre></td>
</tr>
<tr class="even">
<td align="left"><p><strong>OsLoadOptions</strong></p></td>
<td align="left"><p>エントリの<em>ブートパラメーター</em>を指定します。 <em>ブートパラメーター</em>は、オペレーティングシステムの機能を有効化、無効化、および構成するためのコマンドです。 EFI ブートマネージャーは、これらのパラメーターを、解釈および実装する起動可能なデバイスまたはシステムに渡します。</p>
<p>ドライバーのデバッグとテストに関連するブートパラメーターの一覧については、「boot.ini<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/boot-options-in-a-boot-ini-file" data-raw-source="[Boot Options in a Boot.ini File](https://docs.microsoft.com/windows-hardware/drivers/devtest/boot-options-in-a-boot-ini-file)">ファイルのブートオプション</a>」を参照してください。</p></td>
<td align="left"><pre space="preserve"><code>OsLoadOptions: /debug
/debugport=COM1 /baudrate=57600</code></pre></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>BootFilePath</strong></p></td>
<td align="left"><p>オペレーティングシステムの EFI ブートローダーの場所を指定します。 EFI ベースのシステムでは、各オペレーティングシステムまたは起動可能なデバイスには、EFI パーティションにブートローダーの独自のコピーがあります。</p>
<p>EFI NVRAM では、ブートローダーのファイルパスは、グローバル一意識別子 (GUID) を使用して EFI パーティションを識別するバイナリ EFI デバイスパスとして保存されます。</p>
<p>Bootcfg は、パス表示でパーティションの NT デバイス名を使用します。</p></td>
<td align="left"><pre space="preserve"><code>BootFilePath: \Device\HarddiskVolume1
\EFI\Microsoft\WINNT50\ia64ldr.efi</code></pre></td>
</tr>
<tr class="even">
<td align="left"><p><strong>OsFilePath</strong></p></td>
<td align="left"><p>オペレーティングシステムの場所を指定します。</p>
<p>NVRAM では、この値は、ブートディスクパーティションの GUID と、オペレーティングシステムを含むディレクトリへのパスとして、EFI デバイスパスとして保存されます。</p>
<p>Bootcfg は、パス表示でパーティションの NT デバイス名を使用します。</p></td>
<td align="left"><pre space="preserve"><code>OsFilePath: \Device\HarddiskVolume3
\WINDOWS</code></pre></td>
</tr>
</tbody>
</table>

また、Bootcfg には*efi ブートエントリ ID*が表示されない efi ブートエントリの重要な要素があります。 EFI ブートエントリは、EFI ブートエントリの一意の識別子です。 この識別子は、ブートエントリが作成されるときに割り当てられ、変更されることはありません。 ブートエントリは、ブート*順序*の配列など、いくつかのリストに含まれています。これは、ブートエントリのバックアップコピーを含む、ブートエントリに関連するデータをシステムが格納するディスク上のディレクトリの名前です。 EFI ブートエントリ ID の形式は Boot*xxxx*です。ここで、 *xxxx*は、ブートエントリが作成される順序を反映した16進数です。

> [!NOTE] 
> Bootcfg の**ブートエントリ id**フィールドと、Nvrboot のブートエントリ番号には、EFI ブートエントリ id は表示されません。 Bootcfg と Nvrboot の Id は **、ブートエントリセクション内**のブートエントリの順序を表す行番号であり、エントリの順序が変更されると変更されます。

Itanium ベースシステムでのブートオプションの詳細については、「拡張ファームウェアインターフェイスの仕様」を参照してください。 仕様のコピーは、 [Intel 拡張ファームウェアインターフェイス](https://www.intel.com/content/www/us/en/architecture-and-technology/unified-extensible-firmware-interface/efi-homepage-general-technology.html)の web サイトからダウンロードできます。
