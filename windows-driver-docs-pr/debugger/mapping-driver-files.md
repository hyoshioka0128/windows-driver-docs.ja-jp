---
title: ドライバー ファイルのマッピング
description: ドライバー ファイルのマッピング
ms.assetid: 9a13a6a9-b585-4be1-b7c8-da65fa3ba6c6
keywords:
- ドライバーファイルのマッピング
- ドライバー置換マップ
- ドライバー置換マップ、概要
- ドライバー置換マップ、ファイル形式
- ドライバー置換マップ, ブートドライバーの置き換え
- ブートドライバーの置換
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: a9bc31d59ac8c3bdace42861938b696bf6c2deb5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834363"
---
# <a name="mapping-driver-files"></a>ドライバー ファイルのマッピング


## <span id="ddk_mapping_driver_files_dbg"></span><span id="DDK_MAPPING_DRIVER_FILES_DBG"></span>


ドライバーファイルを置き換えるのは困難な場合があります。 多くの場合、Microsoft Windows*セーフビルド*を起動し、ドライバーバイナリを交換してから、もう一度ブートする必要があります。

ただし、Windows XP 以降のバージョンの Windows では、ドライバーファイルをより簡単に置き換える方法がサポートされています。 この方法を使用して、任意のカーネルモードドライバー (ディスプレイドライバーを含む)、Windows サブシステムドライバー、またはその他のカーネルモードモジュールを置き換えることができます。 わかりやすくするために、このトピックでは、カーネルモードモジュールに対してこのメソッドを使用することもできますが、これらのファイルは*ドライバー*と呼ばれています。

このメソッドは、WinDbg または KD がカーネルデバッガーとしてアタッチされている場合に使用できます。 この方法はブートドライバーでも使用できますが、これはより困難です。 ブートドライバーでこの方法を使用する方法の詳細については、「ブートドライバーの置き換え」を参照してください。

ドライバー置換マップを使用してドライバーファイルを置き換えるには、次の手順を実行します。

1.  *ドライバー置換マップファイル*を作成します。 このファイルは、ホストコンピューター上のターゲットコンピューター上のドライバーとその交換用ドライバーの一覧を示すテキストファイルです。 任意の数のドライバーを置き換えることができます。 たとえば、次の情報が含まれているホストコンピューターの d:\\Map\_Files ディレクトリに、Mymap という名前のファイルを作成できます。

    ```ini
    map
    \Systemroot\system32\drivers\videoprt.sys
    \\myserver\myshare\new_drivers\videoprt.sys
    ```

    このファイルの構文の詳細については、「ドライバー置換マップファイル形式」を参照してください。

2.  ターゲットコンピューターへのカーネルデバッグ接続を設定し、ホストコンピューターでカーネルデバッガー (KD または WinDbg) を起動します。 (対象のコンピューターに実際に侵入する必要はありません)。

3.  次のいずれかの操作を行って、ドライバー置換マップファイルを読み込みます。
    -   カーネルデバッガーを起動する前に、\_NT\_KD\_FILES[環境変数](environment-variables.md)を設定します。

        ```console
        D:\Debugging Tools for Windows> set _NT_KD_FILES=d:\Map_Files\mymap.ini
        D:\Debugging Tools for Windows> kd
        ```

    -   カーネルデバッガーを起動した後、 [**kdfiles (ドライバー置換マップの設定)** ](-kdfiles--set-driver-replacement-map-.md)コマンドを使用します。

        ```console
        D:\Debugging Tools for Windows> kd
        kd> .kdfiles d:\Map_Files\mymap.ini
        KD file associations loaded from 'd:\Map_Files\mymap.ini'
        ```

        また、 **kdfiles**コマンドを使用して、現在のドライバー置換マップファイルを表示したり、ドライバー置換マップを削除したりすることもできます。 このコマンドを使用しない場合、マップはデバッガーを終了するまで保持されます。

この手順を完了すると、ドライバー置換マップが有効になります。

対象のコンピュータがドライバを読み込もうとするたびに、このドライバがマップされているかどうかをカーネルデバッガーに問い合わせます。 ドライバーがマップされている場合、置き換えファイルはカーネル接続を介して送信され、古いドライバーファイルにコピーされます。 新しいドライバーが読み込まれます。

### <a name="span-iddriver_replacement_map_file_formatspanspan-iddriver_replacement_map_file_formatspandriver-replacement-map-file-format"></a><span id="driver_replacement_map_file_format"></span><span id="DRIVER_REPLACEMENT_MAP_FILE_FORMAT"></span>ドライバー置換マップファイル形式

各ドライバーファイルの置換は、ドライバー置換マップファイルの3行で示されます。

-   最初の行は "map" という語で構成されています。

-   2行目では、ターゲットコンピューター上の古いドライバーのパスとファイル名を指定します。

-   3番目の行は、新しいドライバーの完全なパスを指定します。 このドライバーは、ホストコンピューターまたは他のサーバーに配置できます。

この情報のパターンは、何回でも繰り返すことができます。

パスとファイル名は大文字と小文字が区別されず、実際のドライバーファイル名は異なる場合があります。 3行目に指定したファイルは、対象のコンピューターがそのドライバーを読み込もうとしているときに、2行目に指定したファイルにコピーされます。

Kdfiles は、サービスコントロールマネージャー (SCM) データベースに格納されているファイル名を照合しようとします。 SCM データベースの名前は、MmLoadSystemImage に渡された名前と同じです。

Windows 10 以降のバージョンのデバッグツールでは、ドライバーマッピングはドライバー名を動的に一致させ、適切なパスを決定します。 完全なパスを指定する必要はなく、ファイル拡張子も省略可能です。 これらのエントリのいずれかを使用して、NT ファイルシステムドライバーと一致させることができます。

-   ntfs
-   NTFS
-   ntfs.sys
-   windows\\system32\\ドライバー\\ntfs.sys

これらのエントリのいずれかを使用して、NT カーネルドライバーと一致させることができます。

-   ntoskrnl.exe
-   NTOSKRNL.EXE
-   ntoskrnl.exe
-   windows\\system32\\ドライバー\\ntoskrnl.exe

マップファイルには空白行を含めることができ、シャープ記号 ( **\#** ) で始まるコメント行を含めることができます。 ただし、ファイルに "map" が表示された後、次の2行は古いドライバーと新しいドライバーである必要があります。 空白行とコメント行は、3行のマップブロックを分割できません。

ドライバー置換マップファイルの例を次に示します。

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

ドライバー置換マップファイルはテキストファイルである必要がありますが、任意のファイル名とファイル名拡張子 (.ini、.txt、マップなど) を使用できます。

### <a name="span-idadditional_notesspanspan-idadditional_notesspanadditional-notes"></a><span id="additional_notes"></span><span id="ADDITIONAL_NOTES"></span>その他の注意事項

ドライバーの置換が発生すると、カーネルデバッガーにメッセージが表示されます。

[**Ctrl + d**](ctrl-d--toggle-debug-info-.md) (KD の場合) または CTRL + ALT + d (WinDbg の場合) を使用すると、置換要求に関する詳細情報が表示されます。 この情報は、表示されている名前が SCM データベース内の名前と一致するかどうかわからない場合に役立ちます。

Bcdedit bootdebug オプションを有効にすると、カーネル、hal、またはブートドライバーの交換に役立つ初期ブート情報を表示できます。

```console
bcdedit -bootdebug on
```

詳細については、「 [BCDEdit Options Reference](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」を参照してください。

カーネルデバッガーが終了しても、ドライバーの交換は行われません。 ただし、ドライバーファイルが実際に上書きされるため、既に置き換えられているドライバーは、古いバイナリに戻りません。

このドライバーの置換機能は、自動的に Windows ファイル保護 (WFP) をバイパスします。

ターゲットコンピューターを再起動する必要はありません。 ドライバーの置き換えは、コンピューターが再起動されたかどうかに関係なく、対象のコンピューターがドライバーを読み込むたびに発生します。 もちろん、ほとんどのドライバーはブートプロセス中に読み込まれるので、実際には、マップファイルが読み込まれた後に、対象のコンピューターを再起動する必要があります。

\_NT\_KD\_ファイル変数が定義されている場合は、カーネルデバッガーの起動時に指定されたドライバー置換マップファイルが読み取られます。 **Kdfiles**コマンドを発行すると、指定したファイルが直ちに読み込まれます。 この時点で、デバッガーは、ファイルに基本マップ/行/行形式があることを確認します。 ただし、実際のパスとファイル名は、置換が行われるまで検証されません。

マップファイルが読み込まれると、デバッガーはその内容を格納します。 この時点より後にこのファイルを変更した場合、変更は無効になり**ます (kdfiles**コマンドを再発行しない限り)。

### <a name="span-idreplacing_boot_driversspanspan-idreplacing_boot_driversspanreplacing-boot-drivers"></a><span id="replacing_boot_drivers"></span><span id="REPLACING_BOOT_DRIVERS"></span>ブートドライバーの置換

このドライバー置換方法を使用してブートドライバーファイルを置き換える場合は、Windows カーネルではなく、カーネルデバッガーを Windows ブートローダー (Ntldr) に接続する必要があります。 この接続を確立するには、まず、特別なデバッガー対応バージョンの Ntldr をインストールする必要があります。 このバージョンの Ntldr は、Windows Driver Kit (WDK) の% DDKROOT%\\デバッグディレクトリにあります。

ターゲットコンピューターでは Boot.ini ファイルがバイパスされるため、通常の方法でカーネル接続プロトコルを設定することはできません。 接続は、ターゲットコンピューターの COM1 ポートを介して行う必要があります。 ボーレートは115200です。 そのため、ホストコンピューターのカーネルデバッガーは、115200の速度で COM 接続を使用するように構成する必要があります。

この特別な方法は、ブートドライバー (つまり、Acpi、Classpnp、disk.sys など) にのみ適用されます。 [**lm t n**](lm--list-loaded-modules-.md)は、初期の Windows ブレークポイントで表示されます。 ブートの完了後に**Mmloadsystemimage**が読み込まれる標準ドライバーを置き換える必要がある場合は、前に説明した標準の方法を使用する必要があります。

Boot.ini ファイルの代わりに EFI ファームウェアを使用するコンピューターのブートドライバーを置き換えることはできません。

 

 





