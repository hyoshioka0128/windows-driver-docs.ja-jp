---
title: EFI でのブート オプションの概要
description: EFI でのブート オプションの概要
ms.assetid: 2237d321-75e6-4723-9f08-484bd9097360
keywords:
- WDK、NVRAM ブート オプションは、NVRAM の EFI ブート オプションの詳細について
- WDK、EFI NVRAM ブート オプションは、NVRAM の EFI ブート オプションの詳細について
- グローバルに定義されている変数 WDK ブート オプション
- ブート WDK を変数オプション
- ブート エントリ Id WDK
- EFI ブート エントリ Id WDK
- WDK のブート オプションの識別子
- WDK のブート エントリ
- Bootcfg ツール
ms.date: 07/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: d43b51305430f823e7bba91990343e9e5f02c474
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356354"
---
# <a name="overview-of-boot-options-in-efi"></a>EFI でのブート オプションの概要

システムの BIOS ファームウェアでブート オプション のようには、EFI NVRAM にブート オプションの 2 つの種類があります。

-   *グローバルに定義されている変数*起動可能なデバイスとコンピューターの起動可能なプログラムをすべてに適用されます。

-   *起動オプション変数*起動可能なデバイスやオペレーティング システムなどのプログラムの特定のロード構成にのみ適用されます。 システム固有の変数には、起動可能なデバイスまたはコンピューターの起動可能なプログラムの各構成用のブート エントリが構成されています。

[Bootcfg](https://docs.microsoft.com/windows-server/administration/windows-commands/bootcfg)で説明したツール[efi ブート オプションを編集](editing-boot-options-in-efi.md)の表示し、EFI NVRAM にブート オプションを編集することができます。

次の例では、Itanium プロセッサ搭載のコンピューターの Bootcfg 表示を示します。

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

次の表では、EFI NVRAM にブート データの Bootcfg 表示の要素について説明します。

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
<td align="left"><p><strong>ブート オプション</strong></p></td>
<td align="left"><p>ブート エントリをすべてに適用されるオプションが含まれています。</p></td>
<td align="left"><p>(セクションの見出し)</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Timeout</strong></p></td>
<td align="left"><p>ブート メニューを表示する時間を決定します。 この値が経過すると、ブート ローダーは、既定のオペレーティング システムを読み込みます。</p></td>
<td align="left"><pre space="preserve"><code>Timeout:   30</code></pre></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>Default</strong></p></td>
<td align="left"><p>既定のオペレーティング システムの場所を指定します。</p></td>
<td align="left"><pre space="preserve"><code>\Device\HarddiskVolume3\WINDOWS</code></pre></td>
</tr>
<tr class="even">
<td align="left"><p><strong>CurrentBootEntryID</strong></p></td>
<td align="left"><p>オペレーティング システムの現在のセッションを開始するために使用されたブート エントリを識別します。</p></td>
<td align="left"><pre space="preserve"><code>CurrentBootEntryID:  1</code></pre></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ブート エントリ</strong></p></td>
<td align="left"><p>システムに固有のデータが含まれています。 1 つ以上の構成<em>ブート エントリ</em>の各オペレーティング システムまたは起動可能なプログラムがコンピューターにインストールされています。</p>
<p>A<em>ブート エントリの</em>は、オペレーティング システムまたは起動可能なプログラムのロード構成を定義するオプションのセットです。</p></td>
<td align="left"><p>(セクションの見出し)</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ブート エントリ ID</strong></p></td>
<td align="left"><p>Bootcfg するブート エントリを識別します。 この値は、ブート エントリの順序を変更するときに変更します。</p>
<p>これは、 <em>EFI ブート エントリ ID</em>EFI のコンポーネントの永続的な識別子であります。</p></td>
<td align="left"><pre space="preserve"><code>Boot entry ID:    1</code></pre></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>OS のフレンドリ名</strong></p></td>
<td align="left"><p>ブート メニューのブート エントリを表します。</p></td>
<td align="left"><pre space="preserve"><code>Windows Server 2003,
Enterprise</code></pre></td>
</tr>
<tr class="even">
<td align="left"><p><strong>OsLoadOptions</strong></p></td>
<td align="left"><p>指定します、<em>ブート パラメーター</em>エントリ。 <em>起動パラメーター</em>有効化、無効化、およびオペレーティング システムの機能を構成するためのコマンドします。 EFI ブート マネージャは、起動可能なデバイスまたはシステムを解釈し、実装にこれらのパラメーターを渡します。</p>
<p>ドライバーのデバッグとテストに関連するブート パラメーターの一覧は、次を参照してください。 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/boot-options-in-a-boot-ini-file" data-raw-source="[Boot Options in a Boot.ini File](https://docs.microsoft.com/windows-hardware/drivers/devtest/boot-options-in-a-boot-ini-file)">Boot.ini ファイルでのブート オプション</a>します。</p></td>
<td align="left"><pre space="preserve"><code>OsLoadOptions: /debug
/debugport=COM1 /baudrate=57600</code></pre></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>BootFilePath</strong></p></td>
<td align="left"><p>オペレーティング システム用の EFI ブート ローダーの場所を指定します。 EFI ベースのシステムでは、各オペレーティング システムまたは起動可能なデバイスがブート ローダーの独自のコピーで EFI パーティション。</p>
<p>EFI の NVRAM にブート ローダーのファイル パスは、EFI パーティションを識別するためにグローバル一意識別子 (GUID) を使用するバイナリ EFI デバイス パスとして保存されます。</p>
<p>Bootcfg は、そのパスの表示で、パーティションの NT デバイス名を使用します。</p></td>
<td align="left"><pre space="preserve"><code>BootFilePath: \Device\HarddiskVolume1
\EFI\Microsoft\WINNT50\ia64ldr.efi</code></pre></td>
</tr>
<tr class="even">
<td align="left"><p><strong>OsFilePath</strong></p></td>
<td align="left"><p>オペレーティング システムの場所を指定します。</p>
<p>NVRAM には、この値は、EFI デバイス パスのブート ディスクのパーティションの GUID を使用して、オペレーティング システムを含むディレクトリへのパスとして保存されます。</p>
<p>Bootcfg は、そのパスの表示で、パーティションの NT デバイス名を使用します。</p></td>
<td align="left"><pre space="preserve"><code>OsFilePath: \Device\HarddiskVolume3
\WINDOWS</code></pre></td>
</tr>
</tbody>
</table>

さらに、Bootcfg を表示しない、EFI ブート エントリの重要な要素がある、 *EFI ブート エントリ ID*します。 EFI ブート エントリは、EFI ブート エントリの一意の識別子です。 ブート エントリが作成され、変更しない場合は、この識別子が割り当てられます。 など、いくつかのリストのブート エントリを表す、 *BootOrder*配列は、システムがブート エントリのバックアップ コピーを含む、ブート エントリに関連するデータを格納するディスク上のディレクトリの名前。 EFI ブート エントリ ID が、形式、ブート*xxxx*ここで、 *xxxx*ブート エントリが作成される順序を反映する 16 進数です。

> [!NOTE] 
> **ブート エントリ ID** Bootcfg 内のフィールドと Nvrboot でブート エントリの数で EFI ブート エントリ ID が表示されません。 Bootcfg と Nvrboot Id は、行番号のブート エントリの順序を表す、**ブート エントリ**セクションおよびエントリの順序は変更時に変更します。

Itanium ベース システムのブート オプションの詳細については、拡張ファームウェア インターフェイスの仕様を参照してください。 仕様のコピーをダウンロードすることができます、 [Intel Extensible Firmware Interface](https://go.microsoft.com/fwlink/p/?linkid=10596) web サイト。
