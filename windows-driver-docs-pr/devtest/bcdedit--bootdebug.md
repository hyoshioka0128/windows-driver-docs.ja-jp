---
title: BCDEdit /bootdebug
description: /Bootdebug のブート オプションを有効または現在または指定した Windows オペレーティング システムのブート エントリのブートのデバッグを無効にします。
ms.assetid: 85d0a25e-c411-4d7e-ae11-ce5bed1a37b8
ms.date: 05/21/2018
keywords:
- BCDEdit/bootdebug ドライバー開発ツール
topic_type:
- apiref
api_name:
- BCDEdit /bootdebug
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: bb7b5a8daf8b13a7d6539e3767612b7b95512b90
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581127"
---
# <a name="bcdedit-bootdebug"></a>BCDEdit /bootdebug


**/Bootdebug**ブート オプションを有効または現在または指定した Windows オペレーティング システムのブート エントリのブートのデバッグを無効にします。

> [!NOTE]
> BCDEdit のオプションを設定する前に、無効にするか、またはコンピューターの BitLocker とセキュア ブートを中断する必要があります。

 

``` syntax
    bcdedit /bootdebug [{ID}] { on | off } 
   
```

<a name="parameters"></a>パラメーター
----------

**{**<em>ID</em>**}**   

**{**<em>ID</em>**}** ブート エントリに関連付けられた GUID です。 指定しない場合、 **{**<em>ID</em>**}** のコマンドは、現在アクティブになっているオペレーティング システムを変更します。 ブート エントリに関連付けられた GUID を中かっこで囲む必要がありますブート エントリが指定されている場合 **{}** します。

**の**   

有効では、指定されたブート エントリのデバッグを起動します。 ブート エントリが指定されていない場合、現在のオペレーティング システムのブート デバッグが有効にします。

**オフ**   

無効には、指定されたブート エントリのデバッグを起動します。 ブート エントリが指定されていない場合、現在のオペレーティング システムはブート デバッグが無効にします。

### <a name="comments"></a>コメント

**/Bootdebug**ブート オプション ブートは、特定のブート エントリのデバッグを有効にします。 使用して、 **/dbgsettings**デバッグ接続の種類を構成するオプション (*debugtype*) および接続パラメーターを使用します。 ない場合は **/dbgsettings**グローバル デバッグの設定が使用されるのブート エントリを指定します。 グローバルな設定の既定値は、次の表に表示されます。

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
<td align="left"><p>Debugtype</p></td>
<td align="left"><p>シリアル</p></td>
</tr>
<tr class="even">
<td align="left"><p>Debugport</p></td>
<td align="left"><p>1</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Baudrate</p></td>
<td align="left"><p>115200</p></td>
</tr>
</tbody>
</table>

 

Windows デバッグ ツールの詳細については、次を参照してください。 [Windows デバッグ](https://msdn.microsoft.com/library/windows/hardware/ff551063)します。 設定して、カーネル モードの構成についてはデバッグ セッションを参照してください[カーネル モード デバッグ手作業でセットアップ](https://msdn.microsoft.com/library/windows/hardware/hh439378)します。

次のコマンドは、ブートの Windows ブート マネージャー (Bootmgr.exe) のデバッグを無効にします。 オペレーティング システムが起動し、次に、Windows ブート ローダーを読み込みます Windows ブート マネージャーを選択します。

```
bcdedit /bootdebug {bootmgr} off 
```

次のコマンドは、現在のオペレーティング システム用の Windows ブート ローダーのブートのデバッグを有効します。 Windows では、進行状況バー コントロールのローダー (Winload.exe) を起動し、カーネルのブート ドライバーを読み込みます。

```
bcdedit /bootdebug on 
```

次の例では、最初のコマンドは、グローバルなデバッガを 1394 カーネル デバッグ接続の設定に設定します。 次の 3 つのコマンドは、Windows ブート マネージャー、ブート ローダー、およびオペレーティング システムのカーネル デバッグをデバッグを有効にします。 この組み合わせにより、スタートアップのあらゆる段階でデバッグします。 この組み合わせを使用する場合、ターゲット コンピューターがデバッガーに割り込む 3 回: Windows ブート マネージャーが読み込まれたら、ブート ローダーが読み込まれたら、およびオペレーティング システムが起動します。

```
bcdedit /dbgsettings 1394 CHANNEL:1 
bcdedit /bootdebug {bootmgr} on 
bcdedit /bootdebug on 
bcdedit /debug on 
```

 

 





