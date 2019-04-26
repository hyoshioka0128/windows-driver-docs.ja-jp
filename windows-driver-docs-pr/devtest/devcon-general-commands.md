---
title: デバイス コンソール (DevCon.exe) のコマンド
description: DevCon (DevCon.exe) は、Windows を実行しているコンピューターにデバイスの詳細情報を表示できるコマンド ライン ツールです。 有効にする、無効にする、インストール、構成、およびデバイスを削除する DevCon を使用することもできます。 DevCon では、次の構文を使用します。
ms.assetid: b397c407-db1f-4e2a-8beb-4fe989bd06e0
keywords:
- デバイスのコンソール (DevCon.exe) ドライバーの開発ツールをコマンドします。
topic_type:
- apiref
api_name:
- Device Console (DevCon.exe) Commands
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6faefcb9433e56c0e752a413ede69719525dc1a0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347048"
---
# <a name="device-console-devconexe-commands"></a>デバイス コンソール (DevCon.exe) のコマンド


DevCon (DevCon.exe) は、Windows を実行しているコンピューターにデバイスの詳細情報を表示できるコマンド ライン ツールです。 有効にする、無効にする、インストール、構成、およびデバイスを削除する DevCon を使用することもできます。 DevCon では、次の構文を使用します。

```
devcon [/m:\\computer] [/r] command [arguments] 
```

## <a name="span-idddkdevcongeneralcommandstoolsspanspan-idddkdevcongeneralcommandstoolsspanparameters"></a><span id="ddk_devcon_general_commands_tools"></span><span id="DDK_DEVCON_GENERAL_COMMANDS_TOOLS"></span>パラメーター


**注**  状態またはデバイスの構成を変更するには、コンピューターの Administrators グループのメンバーであります。

 

DevCon コマンドのパラメーターは、構文に示されている順序で表示する必要があります。 パラメーターの順序が正しくありません DevCon は、それを無視しますが、構文エラーは表示されません。 代わりに、残りのパラメーターを使用してコマンドを処理します。

コマンドの構文については、コマンド プロンプト ウィンドウで、次のコマンドを使用できます。**DevCon ヘルプ**または**DevCon ヘルプ***コマンド*します。

<span id="________m___computer______"></span><span id="________M___COMPUTER______"></span> **m:\\\\**<em>コンピューター</em>指定したリモート コンピューターでコマンドを実行します。 円記号が必要です。
**注**   DevCon コマンドをリモート コンピューターで実行する、グループ ポリシー設定がリモート コンピューターで実行するプラグ アンド プレイ サービスを許可する必要があります。 Windows Vista と Windows の以降のバージョンを実行しているコンピューターで、グループ ポリシーには、既定では、サービスへのリモート アクセスが無効にします。 WDK 8 WDK 8.1 を実行するコンピューターでのリモート アクセス機能は使用できません。

 

<span id="________r______"></span><span id="________R______"></span> **/r**条件付き再起動します。 再起動が必要な変更を有効にする場合にのみ操作を完了した後、システムを再起動します。

このパラメーターとは異なります、 [ **DevCon 再起動**](devcon-reboot.md)操作で、強制的にシステムを再起動します。 代わりに、 **/r**かどうか、再起動が必要、付随する操作からのリターン コードに基づくパラメーターを決定します。詳細については、次を参照してください。[再起動と再起動](#ddk-rebooting-and-restarting-tools)します。

<span id="_______command______"></span><span id="_______COMMAND______"></span> *コマンド*DevCon コマンドを指定します。 使用可能な DevCon コマンドとコマンド引数の詳細については、次の一覧を使用します。

使用してコマンド プロンプト ウィンドウで構文のヘルプを取得することも**DevCon ヘルプ***コマンド*します。

*一覧し、表示*コンピューターで、デバイスに関する情報は、次のコマンドを使用します。

[**DevCon HwIDs**](devcon-hwids.md)

[**DevCon クラス**](devcon-classes.md)

[**DevCon ListClass**](devcon-listclass.md)

[**DevCon DriverFiles**](devcon-driverfiles.md)

[**DevCon DriverNodes**](devcon-drivernodes.md)

[**DevCon リソース**](devcon-resources.md)

[**DevCon スタック**](devcon-stack.md)

[**DevCon 状態**](devcon-status.md)

[**DevCon Dp\_列挙型**](devcon-dp-enum.md)

*検索*コンピューター上のデバイスについては、次のコマンドを使用します。

[**DevCon 検索**](devcon-find.md)

[**DevCon FindAll**](devcon-findall.md)

デバイスを操作するまたは*変更*の構成では、次のコマンドを使用します。

[**DevCon 有効にします。**](devcon-enable.md)

[**DevCon 無効にします。**](devcon-disable.md)

[**DevCon Update**](devcon-update.md)

[**DevCon UpdateNI**](devcon-updateni.md)

[**DevCon インストール**](devcon-install.md)

[**DevCon の削除**](devcon-remove.md)

[**DevCon 再スキャン**](devcon-rescan.md)

[**DevCon 再起動**](devcon-restart.md)

[**DevCon 再起動**](devcon-reboot.md)

[**DevCon SetHwID**](devcon-sethwid.md)

[**DevCon ClassFilter**](devcon-classfilter.md)

[**DevCon Dp\_追加**](devcon-dp-add.md)

[**DevCon Dp\_削除**](devcon-dp-delete.md)

<span id="_______arguments______"></span><span id="_______ARGUMENTS______"></span> *引数*DevCon コマンドの引数を指定します。

<span id="__________or_help"></span><span id="__________OR_HELP"></span> **/?** または**ヘルプ**ヘルプを表示します。 操作を指定すると、DevCon は、操作の詳細なヘルプを表示します。

パラメーターは、指定した順序で表示する必要があります。 たとえばのヘルプを表示するため、 [ **DevCon 状態**](devcon-status.md)型、操作**devcon/でしょうかステータス**(または**devcon ヘルプ状態**) ではなく、 。**devcon 状態/でしょうか。**.

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

多くの DevCon 操作には、デバイスのハードウェア ID が必要です。 DevCon の後続の操作で使用するためのコンピューター上のすべてのデバイスのハードウェア Id の一覧を作成するで始まる、 [ **DevCon HwIDs** ](devcon-hwids.md)コマンド。 詳細については、次を参照してください。[ハードウェア Id](https://msdn.microsoft.com/library/windows/hardware/ff546152)と[識別文字列](https://msdn.microsoft.com/library/windows/hardware/ff541224)します。

### <a name="span-idddkdevconsearchlogictoolsspanspan-idddkdevconsearchlogictoolsspanhow-devcon-searches-for-devices"></a><span id="ddk_devcon_search_logic_tools"></span><span id="DDK_DEVCON_SEARCH_LOGIC_TOOLS"></span>DevCon でデバイスを検索する方法

DevCon では、そのコンピューター名、ハードウェア ID、互換性 ID、デバイス インスタンス ID、およびデバイス セットアップ クラス別にデバイスを識別します。

コマンドが含まれている場合は複数の ID または ID パターン (ワイルドカード文字が含まれる ID (\*))、DevCon 返しますデバイス Id の Id または ID と一致パターン。 これは、「または」ID の引数間と仮定します。

たとえば、 **devcon hwids \*pnp\* \*マウス\\*** がハードウェア ID または互換性 ID の"pnp"または「マウス」のいずれかを含む、デバイスを返します

コマンドには、デバイス セットアップ クラスが含まれている場合、DevCon が最初にセットアップ クラスが、検索を制限し、ID パターンのいずれかに一致するクラスのデバイスを返します、「と」クラスと、Id と、「または」の各 ID の引数間のものは、します。

たとえば、 **devcon hwids = メディア\*pnp\* \*microsoft\\***、ハードウェア ID のデバイスのいずれかを含むメディアのデバイス セットアップ クラスの"pnp"または"microsoft"を返しますまたは互換性のある id。

**注**   DevCon コマンドをリモート コンピューターで実行する、グループ ポリシー設定がリモート コンピューターで実行するプラグ アンド プレイ サービスを許可する必要があります。 Windows Vista と Windows の以降のバージョンを実行しているコンピューターで、グループ ポリシーには、既定では、サービスへのリモート アクセスが無効にします。 WDK 8 WDK 8.1 を実行するコンピューターでのリモート アクセス機能は使用できません。

 

### <span id="ddk_rebooting_and_restarting_tools"></span><span id="DDK_REBOOTING_AND_RESTARTING_TOOLS"></span><a name="ddk-rebooting-and-restarting-tools"></a>再起動と再起動

DevCon では、オペレーティング システムを再起動する 2 つのメソッドとデバイスを再起動する 1 つのメソッドを提供します。

-   **/R**パラメーターは、再起動が必要です、付随する操作を有効にする場合にのみ、オペレーティング システムが再起動される条件付き再起動します。 このパラメーターは、DevCon 操作を含むコマンドでのみ有効です。 ローカル コンピューターまたはリモート コンピューター上のシステムを再起動できます (Windows XP 以前のバージョン)。

-   **DevCon 再起動**操作は、オペレーティング システムの再起動を強制します。 ローカル コンピューターでのみ有効ですし、他の操作と組み合わせて使用できません。 ユーザーの通常の追加、再起動操作を使用する代わりに、 **/r**コマンドのパラメーター。

-   **DevCon 再起動**操作は、指定したデバイスを再起動します。 ローカル コンピューターでのみ有効ですし、他の操作と組み合わせて使用できません。

### <a name="span-idddkdevconreturncodestoolsspanspan-idddkdevconreturncodestoolsspandevcon-return-codes"></a><span id="ddk_devcon_return_codes_tools"></span><span id="DDK_DEVCON_RETURN_CODES_TOOLS"></span>DevCon リターン コード

DevCon がプログラムと DevCon コマンドの成功を判断するためのスクリプトで使用できる整数を返します (たとえば、* * を返す devcon hwids = \\* * *)。

次の表は、リターン コードの一覧です。

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
<td align="left"><p>再起動が必要です。</p></td>
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

 

 

 





