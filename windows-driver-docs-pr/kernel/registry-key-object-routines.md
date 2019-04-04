---
title: レジストリ キー オブジェクトのルーチン
description: レジストリ キー オブジェクトのルーチン
ms.assetid: 9db6ff0d-8371-41bc-82c4-1bb56f5430f2
keywords:
- レジストリ WDK カーネルでは、オブジェクトのルーチン
- ドライバーのレジストリ情報 WDK カーネル、オブジェクトのルーチン
- オブジェクトのルーチンの WDK カーネル
- レジストリ キー オブジェクトの WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 364fbd4055f5399d80f93ea8bfba5c695fe7edd7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532818"
---
# <a name="registry-key-object-routines"></a>レジストリ キー オブジェクトのルーチン





Windows の役員は、オブジェクト マネージャーで管理されている executive オブジェクトとしてレジストリ キーを表します。 (オブジェクト マネージャーの詳細については、次を参照してください[オブジェクト管理](managing-kernel-objects.md)。)。具体的には、すべてのキーが、オブジェクト名とキーを識別するハンドルを開くことができます。

ユーザー モード アプリケーションがグローバルのハンドル、HKEY などの基準としたキーにアクセス\_ローカル\_マシンまたは HKEY\_現在\_ユーザー。 ただし、これらのハンドルでは、カーネル モード コードを使用できません。 そのオブジェクト名でキーを参照する代わりに、 すべてのレジストリ キーのルートは、 **\\レジストリ**オブジェクト。 子孫に対応して、グローバルのハンドル、 **\\レジストリ**オブジェクト、次の表に示すようにします。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>ユーザー モードのハンドル</th>
<th>対応するオブジェクト名</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>HKEY_LOCAL_MACHINE</p></td>
<td><p><strong>\Registry\Machine</strong></p></td>
</tr>
<tr class="even">
<td><p>HKEY_USERS</p></td>
<td><p><strong>\Registry\User</strong></p></td>
</tr>
<tr class="odd">
<td><p>HKEY_CLASSES_ROOT</p></td>
<td><p>カーネル モード同等はありません。</p></td>
</tr>
<tr class="even">
<td><p>HKEY_CURRENT_USER</p></td>
<td><p>単純なカーネル モードと同等の参照がない<a href="registry-run-time-library-routines.md" data-raw-source="[Registry Run-Time Library Routines](registry-run-time-library-routines.md)">レジストリ ランタイム ライブラリ ルーチン</a></p></td>
</tr>
</tbody>
</table>

 

ドライバーは、次の手順を実行することによって、レジストリ キー オブジェクトを操作できます。

1.  レジストリ キー オブジェクトを識別するハンドルを開きます。 詳細については、[レジストリ キー オブジェクトを識別するハンドルを開く](opening-a-handle-to-a-registry-key-object.md)を参照してください。

2.  適切な呼び出し、目的の操作を実行**Zw*Xxx*キー**ルーチン。 これを行う方法については、[レジストリ キー オブジェクトを識別するハンドルを使用して](using-a-handle-to-a-registry-key-object.md)を参照してください。

3.  呼び出すことで、ハンドルを閉じる[ **ZwClose**](https://msdn.microsoft.com/library/windows/hardware/ff566417)します。

 

 




