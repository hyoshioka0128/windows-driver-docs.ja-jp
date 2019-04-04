---
title: BCDEdit/debug
description: /Debug のブート オプションを有効または指定されたブート エントリまたは現在のブート エントリに関連付けられている Windows オペレーティング システムのカーネルのデバッグを無効にします。
ms.assetid: 013ec247-f2ca-4918-9dfa-8b1348d0b4e5
ms.date: 07/02/2018
keywords:
- BCDEdit/debug ドライバー開発ツール
topic_type:
- apiref
api_name:
- BCDEdit /debug
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a2893cd491e6d910924f3557d5e52897363cf12d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556556"
---
# <a name="bcdedit-debug"></a>BCDEdit/debug


**/Debug**ブート オプションを有効または指定されたブート エントリまたは現在のブート エントリに関連付けられている Windows オペレーティング システムのカーネルのデバッグを無効にします。

> [!NOTE]
> BCDEdit のオプションを設定する前に、無効にするか、またはコンピューターの BitLocker とセキュア ブートを中断する必要があります。

 

``` syntax
    bcdedit /debug [{ID}] { on | off } 

   
```

<a name="parameters"></a>パラメーター
----------

**{**<em>ID</em>**}**   
**{**<em>ID</em>**}** ブート エントリに関連付けられた GUID です。 指定しない場合、 **{**<em>ID</em>**}** のコマンドは、現在アクティブになっているオペレーティング システムを変更します。 ブート エントリに関連付けられた GUID を中かっこで囲む必要がありますブート エントリが指定されている場合 **{}** します。

 **の**   
カーネルは、指定されたブート エントリのデバッグを有効にします。 ブート エントリが指定されていない場合、現在のオペレーティング システムのカーネル デバッグが有効にします。

**オフ**   
指定されたブート エントリのカーネル デバッガーを無効にします。 ブート エントリが指定されていない場合、現在のオペレーティング システムのカーネル デバッグが無効です。

### <a name="comments"></a>コメント

**/Debug**ブート オプションは、特定のブート エントリのカーネル デバッグできるようにします。 使用して、 **/dbgsettings**デバッグ接続を使用して、接続パラメーターの種類を構成するオプション。 ない場合は **/dbgsettings**グローバル デバッグの設定が使用されるのブート エントリを指定します。 グローバルな設定の既定値は、次の表に表示されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">dbgsetting パラメーター</th>
<th align="left">既定値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>接続の種類</p></td>
<td align="left"><p>シリアル</p></td>
</tr>
<tr class="even">
<td align="left"><p>デバッグ ポート</p></td>
<td align="left"><p>1</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ボー レート</p></td>
<td align="left"><p>115200</p></td>
</tr>
</tbody>
</table>

 

Windows デバッグ ツールの詳細については、[Windows デバッグ](https://msdn.microsoft.com/library/windows/hardware/ff551063)を参照してください。 設定して、カーネル モードの構成についてはデバッグ セッションを参照してください[カーネル モード デバッグ手作業でセットアップ](https://msdn.microsoft.com/library/windows/hardware/hh439378)します。

次の例は、カーネルが 49916baf-0e08-11db-9af4-000bdbd316a0 の GUID を持つブート エントリのデバッグを有効にします。

```
bcdedit /debug {49916baf-0e08-11db-9af4-000bdbd316a0} on 
```

次の例では、最初のコマンドは、グローバルなデバッガの USB 2.0 の設定を設定し、ターゲット myVistaTarget の名前します。 2 番目のコマンドは、現在のセッションで、デバッガーを使用できます。

```
bcdedit /dbgsettings usb targetname:myVistaTarget 
bcdedit /debug ON 
```

 

 





