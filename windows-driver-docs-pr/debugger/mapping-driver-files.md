---
title: ドライバー ファイルのマッピング
description: ドライバー ファイルのマッピング
ms.assetid: 9a13a6a9-b585-4be1-b7c8-da65fa3ba6c6
keywords:
- ドライバー ファイルのマッピング
- ドライバーの置換のマップ
- ドライバーの置換マップ, 概要
- ドライバーの置換マップ、ファイルの形式
- ドライバーの置換のマップ、ブート ドライバーを置き換える
- ブート ドライバーの置換
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc8b2024711501fc64f02a9b967dd9c24fd74f23
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528684"
---
# <a name="mapping-driver-files"></a>ドライバー ファイルのマッピング


## <span id="ddk_mapping_driver_files_dbg"></span><span id="DDK_MAPPING_DRIVER_FILES_DBG"></span>


ドライバー ファイルの置換は難しくなります。 必要がある多くの場合、Microsoft Windows をブート*セーフ ビルド*し、バイナリ、ドライバーを置き換えて、もう一度起動します。

ただし、Windows XP および Windows の以降のバージョンは、ドライバー ファイルを置き換える単純なメソッドをサポートします。 このメソッドを使用すると、カーネル モード ドライバー (ディスプレイ ドライバーを含む)、Windows サブシステム ドライバー、またはその他のカーネル モードのモジュールを置き換えます。 わかりやすくするため、これらのファイルを呼び出す*ドライバー* 、このトピックでにもかかわらずするこのメソッドを使用、カーネル モードのモジュール。

WinDbg、KD または、カーネル デバッガーに割り当てられているときに、このメソッドを使用できます。 ブート ドライバーでは、このメソッドを使用することもできますより難しくなります。 ブート ドライバーでこのメソッドを使用する方法の詳細については、ブート ドライバーの交換を参照してください。

ドライバー置換マップを使用して、ドライバー ファイルを置き換えるするには、次の操作を行います。

1.  作成、*ドライバー置換マップ ファイル*します。 このファイルは、ターゲット コンピューター上のドライバーと、ホスト コンピューターで、置換ドライバー一覧を含むテキスト ファイルです。 ドライバーの任意の数を置き換えることができます。 D: で Mymap.ini がという名前のファイルを作成するなど、\\マップ\_次の情報を含む、ホスト コンピューターのファイルのディレクトリ。

    ```ini
    map
    \Systemroot\system32\drivers\videoprt.sys
    \\myserver\myshare\new_drivers\videoprt.sys
    ```

    このファイルの構文の詳細については、ドライバーの置換マップ ファイルの形式を参照してください。

2.  カーネル デバッグ対象のコンピュータへの接続を設定し、ホスト コンピューター上でカーネル デバッガー (KD または WinDbg) を起動します。 (必要はありません、ターゲット コンピューターを実際に中断します。)

3.  次のいずれかの方法でドライバーの置換のマップ ファイルを読み込みます。
    -   設定、 \_NT\_KD\_ファイル[環境変数](environment-variables.md)カーネル デバッガーを開始する前にします。

        ```console
        D:\Debugging Tools for Windows> set _NT_KD_FILES=d:\Map_Files\mymap.ini
        D:\Debugging Tools for Windows> kd
        ```

    -   使用して、 [ **.kdfiles (ドライバー置換マップの設定)** ](-kdfiles--set-driver-replacement-map-.md)カーネル デバッガーを開始した後にコマンドします。

        ```console
        D:\Debugging Tools for Windows> kd
        kd> .kdfiles d:\Map_Files\mymap.ini
        KD file associations loaded from 'd:\Map_Files\mymap.ini'
        ```

        使用することも、 **.kdfiles**コマンド ドライバー交換の現在のマップ ファイルを表示するか、ドライバーの置換のマップを削除します。 このコマンドを使用しない場合、デバッガーを終了するまで、マップが永続化します。

この手順を完了すると、ドライバーの置換のマップが有効になります。

ターゲット コンピューターのドライバーをロードしようとしていますが、このドライバーがマップされているかどうかを判断するには、カーネル デバッガーを照会します。 ドライバーがマップされている場合は、置換ファイルがカーネル接続経由で送信され、古いドライバー ファイルにコピーします。 新しいドライバーは、読み込まれます。

### <a name="span-iddriverreplacementmapfileformatspanspan-iddriverreplacementmapfileformatspandriver-replacement-map-file-format"></a><span id="driver_replacement_map_file_format"></span><span id="DRIVER_REPLACEMENT_MAP_FILE_FORMAT"></span>ドライバーの置換マップ ファイルの形式

各ドライバー ファイルを置き換えるには、交換用のドライバー マップ ファイルの 3 つの行が表示されます。

-   最初の行は、"map"という単語で構成されます。

-   2 番目の行では、ターゲット コンピューターに古いドライバーのパスとファイル名を指定します。

-   3 行目では、新しいドライバーの完全なパスを指定します。 このドライバーは、ホスト コンピューターまたはその他のいくつかのサーバーに配置できます。

情報のこのパターンは、何回繰り返すことができます。

パスとファイル名は小文字が区別され、実際のドライバー ファイル名を異なることができます。 3 番目の行で指定されたファイルは、ターゲット コンピューターがそのドライバーを読み込むと、2 行目で指定したファイルにコピーされます。

Kdfiles については、サービス コントロール マネージャー (SCM) データベースに格納されているファイル名の一致を試みます。 SCM のデータベースの名前は、MmLoadSystemImage に渡された名前と同じです。

Windows 10 とデバッグ ツールの以降のバージョンでは、ドライバーのマッピングは、ドライバー名を動的に一致し、適切なパスを確認するのには機能します。 完全なパスを指定する必要はありませんし、ファイル拡張子は省略可能です。 NT ファイル システム ドライバーと一致するのにには、これらのエントリを使用できます。

-   ntfs
-   NTFS
-   ntfs.sys
-   windows\\system32\\ドライバー\\ntfs.sys

これらのエントリを使用するには、NT カーネル ドライバーの一致するようにします。

-   ntoskrnl
-   NTOSKRNL
-   ntoskrnl.sys
-   windows\\system32\\ドライバー\\ntoskrnl.sys

マップ ファイルは空白行を含めることができ、番号記号で始まるコメント行を含めることができます (**\#**)。 ただし、ファイルに「マップ」が表示されたら、次の 2 つの行は古いドライバーと、新しいドライバーをある必要があります。 空白行とコメント行は、マップの 3 行のブロックを解除できません。

次の例では、ドライバーの置換のマップ ファイルを示します。

```text
map
\Systemroot\system32\drivers\videoprt.sys
e:\MyNewDriver\binaries\videoprt.sys
map
\Systemroot\system32\mydriver.sys
\\myserver\myshare\new_drivers\mydriver0031.sys

# Here is a comment
map
\??\c:\windows\system32\beep.sys
\\myserver\myshare\new_drivers\new_beep.sys
```

ドライバーの置換のマップ ファイルは、テキスト ファイルである必要がありますが、あらゆるファイル名およびファイル名拡張子 (.ini、.txt、.map、およびなど) を使用することができます。

### <a name="span-idadditionalnotesspanspan-idadditionalnotesspanadditional-notes"></a><span id="additional_notes"></span><span id="ADDITIONAL_NOTES"></span>その他のメモ

ドライバーの置換が発生すると、カーネル デバッガーで、メッセージが表示されます。

使用する場合[ **CTRL + D** ](ctrl-d--toggle-debug-info-.md) (KD) のまたは CTRL + ALT + D (WinDbg) で置換要求の詳細情報を表示します。 この情報は、表示されている名前が SCM データベースで 1 つと一致するかどうかが不明である場合に便利です。

カーネル、hal、またはブート ドライバーを置換するために役立つ初期ブート情報を表示する bcdedit bootdebug オプションを有効にすることができます。

```console
bcdedit -bootdebug on
```

詳細については、[オプションの参照を BCDEdit](https://msdn.microsoft.com/library/windows/hardware/ff542205)を参照してください。

カーネル デバッガーが終了した場合は複数のドライバーの置き換えなしに発生します。 ただし、既に置き換えられているすべてのドライバーに戻りません、古いバイナリでは、ドライバー ファイルが実際に上書きされるためです。

このドライバーの置換機能には、Windows ファイル保護 (WFP) が自動的にバイパスされます。

ターゲット コンピューターを再起動する必要はありません。 ドライバーの置換には、ターゲット コンピューターが再起動されるかどうかに関係なく、ドライバーを読み込むたびに発生します。 もちろん、ほとんどのドライバーは、ブート プロセス中に読み込まれるため、実際には、マップ ファイルが読み込まれた後、ターゲット コンピューターを再起動する必要があります。

場合、 \_NT\_KD\_ファイルの変数が定義されている場合は、カーネル デバッガーの起動時には指定されたドライバーの置換マップ ファイルの読み取り。 発行した場合、 **.kdfiles**コマンド、指定したファイルは、すぐに読み取りができます。 この時点では、デバッガーは、基本的なマップ/行/フォーマット ファイルであることを確認します。 実際のパスとファイル名の置換が行われるまでを確認はいません。

マップ ファイルが読み取られた後、デバッガーはその内容を保存します。 影響を与える変更がない場合、この時点より後にこのファイルを変更すると、(再実行していない限り、 **.kdfiles**コマンド)。

### <a name="span-idreplacingbootdriversspanspan-idreplacingbootdriversspanreplacing-boot-drivers"></a><span id="replacing_boot_drivers"></span><span id="REPLACING_BOOT_DRIVERS"></span>ブート ドライバーを置き換える

このドライバー置換メソッドを使用して、ブート ドライバー ファイルを置換する場合は、Windows カーネルではなく、Windows ブート ローダー (Ntldr) にカーネル デバッガーを接続する必要があります。 この接続を行うことができます、前に、Ntldr の特別なデバッガーが有効なバージョンをインストールする必要があります。 Windows Driver Kit (WDK)、%ddkroot に Ntldr のこのバージョンを見つけることができます\\デバッグ ディレクトリ。

対象のコンピュータが、Boot.ini ファイルをバイパスするため、一般的な方法でカーネルの接続プロトコルを設定できません。 ターゲット コンピューター上の COM1 ポート経由の接続を行う必要があります。 ボー レートは、115200 です。 したがって、115200 速度で COM 接続を使用するホスト コンピューターでカーネル デバッガーを構成する必要があります。

この特殊なメソッドは、ブート ドライバーにのみ適用されます (つまり、Acpi.sys、Classpnp.sys、Disk.sys、およびその他を[ **lm t n** ](lm--list-loaded-modules-.md)初期 Windows ブレークポイントが表示されます)。 標準のドライバーを交換する必要がある場合を**MmLoadSystemImage**ブートが完了した後に読み込み、前に説明した標準的な方法を使用する必要があります。

Boot.ini ファイルではなく EFI ファームウェアを使用するコンピューター上のブート ドライバーを置き換えることはできません。

 

 





