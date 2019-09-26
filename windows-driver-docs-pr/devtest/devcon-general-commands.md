---
title: デバイス コンソール (DevCon.exe) のコマンド
description: DevCon (DevCon) は、Windows を実行しているコンピューター上のデバイスに関する詳細情報を表示できるコマンドラインツールです。 また、DevCon を使用して、デバイスの有効化、無効化、インストール、構成、および削除を行うこともできます。 DevCon は、次の構文を使用します。
ms.assetid: b397c407-db1f-4e2a-8beb-4fe989bd06e0
keywords:
- デバイスコンソール (DevCon) コマンドドライバーの開発ツール
topic_type:
- apiref
api_name:
- Device Console (DevCon.exe) Commands
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc8a59d9e112b67109cf761e72b890e43405285c
ms.sourcegitcommit: 9dbb1ef59c3e797bfc3cc418dd2b9bdc44940d14
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71284911"
---
# <a name="device-console-devconexe-commands"></a>デバイス コンソール (DevCon.exe) のコマンド


DevCon (DevCon) は、Windows を実行しているコンピューター上のデバイスに関する詳細情報を表示できるコマンドラインツールです。 また、DevCon を使用して、デバイスの有効化、無効化、インストール、構成、および削除を行うこともできます。 DevCon は、次の構文を使用します。

```
devcon [/m:\\computer] [/r] command [arguments] 
```

## <a name="span-idddk_devcon_general_commands_toolsspanspan-idddk_devcon_general_commands_toolsspanparameters"></a><span id="ddk_devcon_general_commands_tools"></span><span id="DDK_DEVCON_GENERAL_COMMANDS_TOOLS"></span>パラメータ


**注デバイスの**状態または構成を変更するには、コンピューターの Administrators グループのメンバーである必要があります。  

 

DevCon コマンドのパラメーターは、構文に示されている順序で表示される必要があります。 パラメーターの順序が正しくない場合、DevCon はそれらを無視しますが、構文エラーは表示されません。 代わりに、残りのパラメーターを使用してコマンドを処理します。

コマンド構文のヘルプを表示するには、コマンドプロンプトウィンドウで次のコマンドを使用します。**Devcon ヘルプ**または**devcon ヘルプ***コマンド*。

<span id="________m___computer______"></span><span id="________M___COMPUTER______"></span> **/m:\\コンピューターは、指定されたリモートコンピューターでコマンドを実行します。\\** 円記号が必要です。
**注:**   リモートコンピューターで DevCon コマンドを実行するには、グループポリシー設定で、プラグアンドプレイサービスをリモートコンピューターで実行できるようにする必要があります。 Windows Vista 以降のバージョンの Windows を実行しているコンピューターでは、グループポリシーによって、サービスへのリモートアクセスが既定で無効になります。 WDK 8.1 および WDK 8 を実行するコンピューターでは、リモートアクセス機能を使用できません。

 

<span id="________r______"></span><span id="________R______"></span> **/r**条件付き再起動。 変更を有効にするために再起動が必要な場合にのみ、操作の完了後にシステムを再起動します。

このパラメーターは、システムを強制的に再起動する、 [**DevCon reboot**](devcon-reboot.md)操作とは異なります。 代わりに、 **/r**パラメーターによって、付随する操作からのリターンコードに基づいて再起動が必要かどうかが決定されます。詳細については、「[再起動と再起動](#ddk-rebooting-and-restarting-tools)」を参照してください。

<span id="_______command______"></span><span id="_______COMMAND______"></span>*コマンド*DevCon コマンドを指定します。 使用可能な DevCon コマンドとコマンド引数の詳細については、次の一覧を参照してください。

また、コマンドプロンプトウィンドウで、 **DevCon help** *コマンド*を使用して構文のヘルプを表示することもできます。

コンピューター上のデバイスに関する情報を*一覧表*示して表示するには、次のコマンドを使用します。

[**DevCon HwIDs**](devcon-hwids.md)

[**DevCon クラス**](devcon-classes.md)

[**DevCon ListClass**](devcon-listclass.md)

[**DevCon DriverFiles**](devcon-driverfiles.md)

[**DevCon DriverNodes**](devcon-drivernodes.md)

[**DevCon リソース**](devcon-resources.md)

[**DevCon スタック**](devcon-stack.md)

[**DevCon ステータス**](devcon-status.md)

[**DevCon Dp\_列挙型**](devcon-dp-enum.md)

コンピューター上のデバイスに関する情報を*検索*するには、次のコマンドを使用します。

[**DevCon 検索**](devcon-find.md)

[**DevCon FindAll**](devcon-findall.md)

デバイスを操作するか、その構成を*変更*するには、次のコマンドを使用します。

[**DevCon 有効化**](devcon-enable.md)

[**DevCon の無効化**](devcon-disable.md)

[**DevCon 更新プログラム**](devcon-update.md)

[**DevCon UpdateNI**](devcon-updateni.md)

[**DevCon インストール**](devcon-install.md)

[**DevCon の削除**](devcon-remove.md)

[**DevCon 再スキャン**](devcon-rescan.md)

[**DevCon の再起動**](devcon-restart.md)

[**DevCon 再起動**](devcon-reboot.md)

[**DevCon SetHwID**](devcon-sethwid.md)

[**DevCon ClassFilter**](devcon-classfilter.md)

[**DevCon Dp\_の追加**](devcon-dp-add.md)

[**DevCon Dp\_の削除**](devcon-dp-delete.md)

<span id="_______arguments______"></span><span id="_______ARGUMENTS______"></span>*引数*DevCon コマンドの引数を指定します。

<span id="__________or_help"></span><span id="__________OR_HELP"></span> **/?** また**はヘルプが**表示されます。 操作を指定すると、[DevCon] 操作の詳細なヘルプが表示されます。

パラメーターは指定された順序で表示される必要があります。 たとえば、 [**Devcon status**](devcon-status.md)操作のヘルプを表示するには、「devcon **/? status** 」 (または「devcon **help status**」) と入力します。これは devcon **status/?** ではありません。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>Comments

多くの DevCon 操作には、デバイスのハードウェア ID が必要です。 その後の DevCon 操作で使用する、コンピューター上のすべてのデバイスのハードウェア Id の一覧を作成するには、まず、 [**Devcon HwIDs**](devcon-hwids.md)コマンドを使用します。 詳細については、「[ハードウェア id](https://docs.microsoft.com/windows-hardware/drivers/install/hardware-ids)と[デバイス id 文字列](https://docs.microsoft.com/windows-hardware/drivers/install/device-identification-strings)」を参照してください。

### <a name="span-idddk_devcon_search_logic_toolsspanspan-idddk_devcon_search_logic_toolsspanhow-devcon-searches-for-devices"></a><span id="ddk_devcon_search_logic_tools"></span><span id="DDK_DEVCON_SEARCH_LOGIC_TOOLS"></span>デバイスを DevCon で検索する方法

DevCon は、コンピューター名、ハードウェア ID、互換性のある ID、デバイスインスタンス ID、デバイスセットアップクラスなどによってデバイスを識別します。

コマンドに複数の id または id パターン (ワイルドカード文字 (\*) を含む id) が含まれている場合、DevCon は、id または id パターンのいずれかに一致する id を持つデバイスを返します。 つまり、ID 引数の間に "or" があることを前提としています。

たとえば、 **devcon hwids \*pnp\* \*mou\*** は、ハードウェア id または互換性のある id に "pnp" または "mou" のいずれかを含むデバイスを返します。

コマンドにデバイスセットアップクラスが含まれている場合、DevCon は最初に検索をセットアップクラスに限定してから、クラス内の任意の ID パターンに一致するデバイスを返します。つまり、クラスと Id の間に "and" を、それぞれの ID 引数の間に "or" を指定します。

たとえば、 **devcon hwids \*= media pnp\* \*microsoft\*** は、ハードウェア id または互換性 id に "pnp" または "microsoft" を含むメディアデバイスセットアップクラスのデバイスを返します。

**注:**   リモートコンピューターで DevCon コマンドを実行するには、グループポリシー設定で、プラグアンドプレイサービスをリモートコンピューターで実行できるようにする必要があります。 Windows Vista 以降のバージョンの Windows を実行しているコンピューターでは、グループポリシーによって、サービスへのリモートアクセスが既定で無効になります。 WDK 8.1 および WDK 8 を実行するコンピューターでは、リモートアクセス機能を使用できません。

 

### <span id="ddk_rebooting_and_restarting_tools"></span><span id="DDK_REBOOTING_AND_RESTARTING_TOOLS"></span><a name="ddk-rebooting-and-restarting-tools"></a>再起動と再起動

DevCon には、オペレーティングシステムを再起動する方法と、デバイスを再起動する方法の2つが用意されています。

-   **/R**パラメーターは、付随する操作を有効にするために再起動が必要な場合にのみ、オペレーティングシステムを再起動する条件付き再起動です。 このパラメーターは、DevCon 操作を含むコマンドでのみ有効です。 ローカルコンピューターまたはリモートコンピューター (Windows XP およびそれ以前) でシステムを再起動することができます。

-   **DevCon の再起動**操作によって、オペレーティングシステムが強制的に再起動されます。 ローカルコンピューター上でのみ有効で、他の操作と組み合わせることはできません。 ユーザーは、通常、再起動操作を使用する代わりに、コマンドに **/r**パラメーターを追加します。

-   **DevCon Restart**操作は、指定されたデバイスを再起動します。 ローカルコンピューター上でのみ有効で、他の操作と組み合わせることはできません。

### <a name="span-idddk_devcon_return_codes_toolsspanspan-idddk_devcon_return_codes_toolsspandevcon-return-codes"></a><span id="ddk_devcon_return_codes_tools"></span><span id="DDK_DEVCON_RETURN_CODES_TOOLS"></span>DevCon リターンコード

DevCon は、DevCon コマンドが成功したかどうかを判断するためにプログラムおよびスクリプトで使用できる整数を返します (たとえば、 **return = DevCon hwids \*** )。

次の表に、リターンコードとその説明を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">リターン コード</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>成功</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>再起動が必要</p></td>
</tr>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p>失敗</p></td>
</tr>
<tr class="even">
<td align="left"><p>3</p></td>
<td align="left"><p>構文エラー</p></td>
</tr>
</tbody>
</table>

 

 

 





