---
title: ブート オプションの概要
description: 概念とブート オプションの内容は、Microsoft Windows オペレーティング システムを実行するすべてのコンピューターとよく似ています。
ms.assetid: e8e835c4-75de-4ce1-965f-d9b822e15044
keywords:
- ブート オプションの詳細については、ブート オプション WDK、
- ブート オプションを格納します。
- ブート ローダー WDK
ms.date: 07/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: d65ab2b31d8f6b885bb017f4ca678eb1985cd80b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557716"
---
# <a name="introduction-to-boot-options"></a>ブート オプションの概要

概念とブート オプションの内容は、Microsoft Windows オペレーティング システムを実行するすべてのコンピューターとよく似ています。 ただし、Windows Vista では、前にコンピューターと別のプロセッサのファームウェア ブート オプションを異なる方法で格納し、さまざまなツールを表示し、各システムのオプションを編集する必要があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Windows のバージョン</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="______Windows_7__Windows_Server_2008__Windows_Vista"></span><span id="______windows_7__windows_server_2008__windows_vista"></span><span id="______WINDOWS_7__WINDOWS_SERVER_2008__WINDOWS_VISTA"></span>Windows Server 2016、Windows 10、Windows Server 2012 R2、Windows 8.1、Windows Server 2012、Windows 8、Windows Server 2008 R2、Windows 7、Windows Server 2008、Windows Vista</p></td>
<td align="left"><p>Windows Vista、および以降のバージョンの Windows では、ファームウェアに依存しない記憶域の構成システムでブート オプションを格納します。 Windows Vista には、新しいブート マネージャーとシステムに固有のブート ローダーも導入されています。 詳細については、<a href="boot-options-in-windows-vista-and-later.md" data-raw-source="[Boot Options in Windows Vista and Later](boot-options-in-windows-vista-and-later.md)">Windows Vista 以降のブート オプション</a>を参照してください。</p></td>
</tr>
</tbody>
</table>

このセクションの内容:
- [Boot.ini ファイルでのブート オプション](boot-options-in-a-boot-ini-file.md)(Windows XP、Windows Server 2003)
- [EFI NVRAM にブート オプション](boot-options-in-efi-nvram.md)(Windows XP、Windows Server 2003)
- [Windows Vista 以降のブート オプションの概要](boot-options-in-windows-vista-and-later.md)
