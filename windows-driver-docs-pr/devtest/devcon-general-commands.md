---
title: デバイス コンソール (DevCon.exe) のコマンド
description: DevCon (DevCon.exe) は、Windows を実行しているコンピューター上のデバイスに関する詳細情報を表示できるコマンド ライン ツールです。 DevCon を使用して、デバイスを有効化、無効化、インストール、構成、削除することもできます。 DevCon で使用される構文は次のとおりです。
ms.assetid: b397c407-db1f-4e2a-8beb-4fe989bd06e0
keywords:
- デバイス コンソール (DevCon.exe) のコマンド、ドライバー開発ツール
topic_type:
- apiref
api_name:
- Device Console (DevCon.exe) Commands
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: high
ms.openlocfilehash: aeff1990d5695440e0f7431334f26e7782863027
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "78335944"
---
# <a name="device-console-devconexe-commands"></a>デバイス コンソール (DevCon.exe) のコマンド


DevCon (DevCon.exe) は、Windows を実行しているコンピューター上のデバイスに関する詳細情報を表示できるコマンド ライン ツールです。 DevCon を使用して、デバイスを有効化、無効化、インストール、構成、削除することもできます。 DevCon で使用される構文は次のとおりです。

```
devcon [/m:\\computer] [/r] command [arguments] 
```

## <a name="span-idddk_devcon_general_commands_toolsspanspan-idddk_devcon_general_commands_toolsspanparameters"></a><span id="ddk_devcon_general_commands_tools"></span><span id="DDK_DEVCON_GENERAL_COMMANDS_TOOLS"></span>パラメーター


**注**   デバイスの状態または構成を変更するには、そのコンピューターの Administrators グループのメンバーである必要があります。

 

DevCon コマンドのパラメーターは、構文に示されている順序で表示される必要があります。 順序が正しくないパラメーターがある場合、DevCon では無視され、構文エラーは表示されません。 その代わりに、残りのパラメーターを使用してコマンドが処理されます。

コマンド構文のヘルプを表示するには、コマンド プロンプト ウィンドウで次のコマンドを使用します: **DevCon help** または **DevCon help** *command*。

<span id="________m___computer______"></span><span id="________M___COMPUTER______"></span> **/m:\\\\** <em>computer</em> 指定したリモート コンピューターでコマンドが実行されます。 円記号が必須です。
**注**   リモート コンピューターで DevCon コマンドを実行するには、リモート コンピューター上でのプラグアンドプレイ サービスの実行がグループ ポリシー設定によって許可されている必要があります。 Windows Vista 以降のバージョンの Windows を実行しているコンピューターでは、そのサービスへのリモート アクセスがグループ ポリシーによって既定で無効にされています。 WDK 8.1 および WDK 8 を実行するコンピューターでは、リモート アクセス機能を使用できません。

 

<span id="________r______"></span><span id="________R______"></span> **/r** 条件付き再起動です。 変更を有効にするために再起動が必要な場合にのみ、操作の完了後にシステムが再起動されます。

このパラメーターは、システムを強制的に再起動する [**DevCon Reboot**](devcon-reboot.md) 操作とは異なります。 **/r** パラメーターを使用すると、付随する操作からのリターン コードに基づいて再起動が必要かどうかが決定されます。詳細については、「[再起動 (rebooting) と再起動 (restarting)](#ddk-rebooting-and-restarting-tools)」を参照してください。

<span id="_______command______"></span><span id="_______COMMAND______"></span> *command* DevCon コマンドが指定されます。 使用可能な DevCon コマンドとコマンド引数については、次の一覧を参照してください。

また、コマンド プロンプト ウィンドウで **DevCon help** *command* を使用することで、構文のヘルプを表示することもできます。

コンピューター上のデバイスに関する情報を "*一覧および表示*" するには、次のコマンドを使用します。

[**DevCon HwIDs**](devcon-hwids.md)

[**DevCon Classes**](devcon-classes.md)

[**DevCon ListClass**](devcon-listclass.md)

[**DevCon DriverFiles**](devcon-driverfiles.md)

[**DevCon DriverNodes**](devcon-drivernodes.md)

[**DevCon Resources**](devcon-resources.md)

[**DevCon Stack**](devcon-stack.md)

[**DevCon Status**](devcon-status.md)

[**DevCon Dp\_enum**](devcon-dp-enum.md)

コンピューター上のデバイスに関する情報を "*検索*" するには、次のコマンドを使用します。

[**DevCon Find**](devcon-find.md)

[**DevCon FindAll**](devcon-findall.md)

デバイスの操作またはその構成の "*変更*" を行うには、次のコマンドを使用します。

[**DevCon Enable**](devcon-enable.md)

[**DevCon Disable**](devcon-disable.md)

[**DevCon Update**](devcon-update.md)

[**DevCon UpdateNI**](devcon-updateni.md)

[**DevCon Install**](devcon-install.md)

[**DevCon Remove**](devcon-remove.md)

[**DevCon Rescan**](devcon-rescan.md)

[**DevCon Restart**](devcon-restart.md)

[**DevCon Reboot**](devcon-reboot.md)

[**DevCon SetHwID**](devcon-sethwid.md)

[**DevCon ClassFilter**](devcon-classfilter.md)

[**DevCon Dp\_add**](devcon-dp-add.md)

[**DevCon Dp\_delete**](devcon-dp-delete.md)

<span id="_______arguments______"></span><span id="_______ARGUMENTS______"></span> *arguments* DevCon コマンドの引数が指定されます。

<span id="__________or_help"></span><span id="__________OR_HELP"></span> **/?** または **help** ヘルプが表示されます。 操作を指定すると、操作の詳細なヘルプが DevCon によって表示されます。

パラメーターは指定された順序で表示される必要があります。 たとえば、[**DevCon Status**](devcon-status.md) 操作のヘルプを表示するには、「**devcon /? status**」 (または「**devcon help status**」) と入力します。「**devcon status /?** 」とはしません。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

DevCon 操作の多くに、デバイスのハードウェア ID が必要です。 その後の DevCon 操作で使用するために、コンピューター上のデバイスすべてのハードウェア ID の一覧を作成するには、[**DevCon HwIDs**](devcon-hwids.md) コマンドから始めます。 詳細については、「[Hardware ID (ハードウェア ID)](https://docs.microsoft.com/windows-hardware/drivers/install/hardware-ids)」と「[デバイスの識別用文字列](https://docs.microsoft.com/windows-hardware/drivers/install/device-identification-strings)」を参照してください。

### <a name="span-idddk_devcon_search_logic_toolsspanspan-idddk_devcon_search_logic_toolsspanhow-devcon-searches-for-devices"></a><span id="ddk_devcon_search_logic_tools"></span><span id="DDK_DEVCON_SEARCH_LOGIC_TOOLS"></span>デバイスを DevCon で検索する方法

DevCon では、コンピューター名、ハードウェア ID、互換性 ID、デバイス インスタンス ID、デバイス セットアップ クラス、またはそのいずれかによってデバイスが識別されます。

コマンドに複数の ID または ID パターン (ワイルドカード文字 (\*) を含む ID) が含まれている場合、その ID または ID パターンのいずれかに一致する ID を持つデバイスが DevCon から返されます。 つまり、各 ID 引数の間に "or" があるものと想定されます。

たとえば、**devcon hwids \*pnp\* \*mou\*** の場合、ハードウェア ID または互換性 ID に "pnp" または "mou" のいずれを含むデバイスが返されます。

コマンドにデバイス セットアップ クラスが含まれている場合、DevCon では、まず検索がそのセットアップ クラスに限定され、次に該当するクラス内の、ID パターンのいずれかに一致するデバイスが返されます。つまり、クラスと ID の間に "and" が、各 ID 引数の間に "or" があるものと想定されます。

たとえば、**devcon hwids =media \*pnp\* \*microsoft\*** の場合、ハードウェア ID または互換性 ID に "pnp" または "microsoft" のいずれかを含む、メディア デバイス セットアップ クラス内のデバイスが返されます。

**注**   リモート コンピューターで DevCon コマンドを実行するには、リモート コンピューター上でのプラグアンドプレイ サービスの実行がグループ ポリシー設定によって許可されている必要があります。 Windows Vista 以降のバージョンの Windows を実行しているコンピューターでは、そのサービスへのリモート アクセスがグループ ポリシーによって既定で無効にされています。 WDK 8.1 および WDK 8 を実行するコンピューターでは、リモート アクセス機能を使用できません。

 

### <a name="span-idddk_rebooting_and_restarting_toolsspanspan-idddk_rebooting_and_restarting_toolsspanrebooting-and-restarting"></a><span id="ddk_rebooting_and_restarting_tools"></span><span id="DDK_REBOOTING_AND_RESTARTING_TOOLS"></span><a name="ddk-rebooting-and-restarting-tools"></a>再起動 (rebooting) と再起動 (restarting)

DevCon には、オペレーティング システムを再起動する方法として 2 つが、デバイスを再起動する方法として 1 つが用意されています。

-   **/r** パラメーターは条件付き再起動であり、付随する操作を有効にするために再起動が必要な場合にのみオペレーティング システムが再起動されます。 このパラメーターは、DevCon 操作を含むコマンドでのみ有効です。 ローカル コンピューター上でもリモート コンピューター上でもシステム (Windows XP およびそれ以前) を再起動することができます。

-   **DevCon Reboot** 操作を使用すると、オペレーティング システムが強制的に再起動されます。 これはローカル コンピューター上でのみ有効であり、他の操作と組み合わせることはできません。 ユーザーは通常、再起動操作を使用するのでなく、 **/r** パラメーターをコマンドに追加します。

-   **DevCon Restart** 操作では、指定したデバイスの再起動が行われます。 これはローカル コンピューター上でのみ有効であり、他の操作と組み合わせることはできません。

### <a name="span-idddk_devcon_return_codes_toolsspanspan-idddk_devcon_return_codes_toolsspandevcon-return-codes"></a><span id="ddk_devcon_return_codes_tools"></span><span id="DDK_DEVCON_RETURN_CODES_TOOLS"></span>DevCon リターン コード

DevCon コマンドが成功したかどうかを判断するためにプログラムおよびスクリプトで使用できる整数が、DevCon によって返されます (たとえば、**return = devcon hwids \*** )。

次の表に、リターン コードを一覧して説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">リターン コード</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>成功</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>再起動が必要です</p></td>
</tr>
<tr class="odd">
<td align="left"><p>2 で保護されたプロセスとして起動されました</p></td>
<td align="left"><p>障害</p></td>
</tr>
<tr class="even">
<td align="left"><p>3</p></td>
<td align="left"><p>構文エラーです</p></td>
</tr>
</tbody>
</table>

 

 

 





