---
title: レジストリ キー オブジェクトのルーチン
description: レジストリ キー オブジェクトのルーチン
ms.assetid: 9db6ff0d-8371-41bc-82c4-1bb56f5430f2
keywords:
- レジストリ WDK カーネル、オブジェクトルーチン
- ドライバーレジストリ情報 WDK カーネル、オブジェクトルーチン
- オブジェクトルーチン WDK カーネル
- レジストリキーオブジェクト WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 08d6d29525a9d7a4ccaf3dd34d41cca9592aa5ab
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838459"
---
# <a name="registry-key-object-routines"></a>レジストリ キー オブジェクトのルーチン





Windows executive は、オブジェクトマネージャーによって管理される executive オブジェクトとしてレジストリキーを表します。 (オブジェクトマネージャーの詳細については、「[オブジェクトの管理](managing-kernel-objects.md)」を参照してください)。特に、すべてのキーにはオブジェクト名があり、キーへのハンドルを開くことができます。

ユーザーモードのアプリケーションは、HKEY\_LOCAL\_MACHINE や HKEY\_CURRENT\_USER など、グローバルハンドルに関連するキーにアクセスします。 ただし、これらのハンドルはカーネルモードコードでは使用できません。 代わりに、オブジェクト名でキーを参照します。 すべてのレジストリキーのルートは、 **\\レジストリ**オブジェクトです。 グローバルハンドルは、次の表に示すように、 **\\Registry**オブジェクトの子孫に対応します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>ユーザーモードハンドル</th>
<th>対応するオブジェクト名</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>HKEY_LOCAL_MACHINE</p></td>
<td><p><strong>\ レジストリ \ コンピューター</strong></p></td>
</tr>
<tr class="even">
<td><p>HKEY_USERS</p></td>
<td><p><strong>\Registry\User</strong></p></td>
</tr>
<tr class="odd">
<td><p>HKEY_CLASSES_ROOT</p></td>
<td><p>カーネルモードに対応していません</p></td>
</tr>
<tr class="even">
<td><p>HKEY_CURRENT_USER</p></td>
<td><p>同等の単純なカーネルモードはありませんが、「<a href="registry-run-time-library-routines.md" data-raw-source="[Registry Run-Time Library Routines](registry-run-time-library-routines.md)">レジストリランタイムライブラリルーチン</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>

 

ドライバーは、次の手順を実行して、レジストリキーオブジェクトを操作できます。

1.  レジストリキーオブジェクトへのハンドルを開きます。 詳細については、「[レジストリキーオブジェクトへのハンドルを開く](opening-a-handle-to-a-registry-key-object.md)」を参照してください。

2.  適切な**Zw*Xxx*キー**ルーチンを呼び出して、目的の操作を実行します。 その方法については、「[レジストリキーオブジェクトへのハンドルの使用](using-a-handle-to-a-registry-key-object.md)」を参照してください。

3.  [**Zwclose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose)を呼び出してハンドルを閉じます。

 

 




