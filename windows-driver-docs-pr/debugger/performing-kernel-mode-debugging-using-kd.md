---
title: ライブ KD を使用してカーネル モードのデバッグ
description: ライブ KD を使用してカーネル モードのデバッグ
ms.assetid: 4C3DB315-CF92-44FC-A54C-0C100A32EB3C
ms.date: 06/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 3fa0e69c775859a620f1a7510773e1feda3b7e19
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539025"
---
# <a name="span-iddebuggerperformingkernel-modedebuggingusingkdspanlive-kernel-mode-debugging-using-kd"></a><span id="debugger.performing_kernel-mode_debugging_using_kd"></span>ライブ KD を使用してカーネル モードのデバッグ


コマンド プロンプト ウィンドウで、KD を起動したときに、ライブのカーネル モードのデバッグ セッションを開始できます。 次のコマンドのいずれかを入力します。

kd \[-y *SymbolPath*\] -k net:port=*PortNumber*,key=*Key*\[,target=*TargetIPAddress*|*TargetHostName*\] 

kd \[-y *SymbolPath*\] -k 1394:channel=*1394Channel*\[,symlink=*1394Protocol*\]

kd \[-y *SymbolPath* \] -k usb:targetname =*USBString*

kd \[-y *SymbolPath* \] -k com:port =*com ポート*、ボー =*BaudRate*

kd \[-y *SymbolPath* \] -k com:pipe、ポート =\\\\*VMHost*\\パイプ\\*PipeName*\[、リセット = 0\]\[、再接続\]

kd \[-y *SymbolPath* \] -k com:*モデム*

kd \[-y *SymbolPath* \] -kl

kd \[-y *SymbolPath* \] -k

詳細については、次を参照してください。 [ **KD コマンド ライン オプション**](kd-command-line-options.md)します。

### <a name="span-idenvironmentvariablesspanspan-idenvironmentvariablesspanspan-idenvironmentvariablesspanenvironment-variables"></a><span id="Environment_Variables"></span><span id="environment_variables"></span><span id="ENVIRONMENT_VARIABLES"></span>環境変数

シリアル (COM ポート) または 1394 接続経由でデバッグは、接続設定を指定するのに環境変数を使用することができます。

次の変数を使用すると、シリアル接続を指定できます。

設定\_NT\_デバッグ\_ポート = *com ポート*

設定\_NT\_デバッグ\_ボー\_率 = *BaudRate*

1394 接続を指定するのにには、次の変数を使用します。

設定\_NT\_デバッグ\_BUS 1394 を =

設定\_NT\_デバッグ\_1394\_チャネル = *1394Channel* 

設定\_NT\_デバッグ\_1394\_シンボリック リンク = *1394Protocol*

詳細については、次を参照してください。[カーネル モードの環境変数](kernel-mode-environment-variables.md)します。

### <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメーター

<span id="_______SymbolPath______"></span><span id="_______symbolpath______"></span><span id="_______SYMBOLPATH______"></span> *SymbolPath*   
シンボル ファイルが配置されているディレクトリの一覧。 ディレクトリの一覧では、セミコロンで区切られます。 詳細については、次を参照してください。[シンボル パス](symbol-path.md)します。

<span id="_______PortNumber______"></span><span id="_______portnumber______"></span><span id="_______PORTNUMBER______"></span> *PortNumber*   
ネットワークのデバッグに使用するポート番号。 49152 ~ 65535 から任意の数を選択できます。 詳細については、次を参照してください。[設定を、ネットワーク接続を手動で](setting-up-a-network-debugging-connection.md)します。

<span id="_______Key______"></span><span id="_______key______"></span><span id="_______KEY______"></span> *キー*   
ネットワークのデバッグに使用する暗号化キー。 対象のコンピュータを構成するときに、bcdedit によって提供される、自動的に生成されたキーを使用することをお勧めします。 詳細については、次を参照してください。[設定を、ネットワーク接続を手動で](setting-up-a-network-debugging-connection.md)します。


<span id="_______TargetIp______"></span><span id="_______targetip______"></span><span id="_______TARGETIP______"></span> *TargetIPAddress*   
ターゲット コンピューターの IPv4 アドレス。 

ときに、ターゲット = IP アドレスを指定すると、これにより、デバッガーに、デバッガーに接続を試みると、ターゲットに特殊なパケットを送信することによって、指定されたターゲット マシンへの接続を開始します。 デバッガーがパケットを送信、ターゲットに繰り返し約 0.5 秒おき、接続しようとしています。 接続が成功した場合、ターゲットは、既存の接続を削除し、デバッガーのこのインスタンスとのみ通信。 これにより、デバッグの既存の接続から、デバッグ セッションを制御することができます。 

ターゲットを指定する必要はありません、ターゲットがホストの IP アドレスで構成されているし、デバッガーが構成されているホストの IP アドレスを持つコンピューターで実行される、IP アドレス パラメーターを = です。 ホストの IP アドレスを持つターゲットを構成する場合にプランにパケットを送信ホスト 3 秒です。  プラン パケットがないターゲットのときに、ホストへの接続にデバッガーを許可する = IP アドレスを指定します。

ターゲットのホストの IP アドレスを構成する方法の詳細については、次を参照してください。[設定を KDNET ネットワーク カーネル デバッグを自動的に](setting-up-a-network-debugging-connection-automatically.md)と[KDNET ネットワーク カーネル デバッグ手作業でセットアップ](setting-up-a-network-debugging-connection.md)します。


<span id="_______TargetName______"></span><span id="_______targetname______"></span><span id="_______TARGETNAME______"></span> *TargetMachineName*   
対象の PC のコンピューター名。 コンピューター名を使用するには、ネットワーク上の DNS システムにコンピューター名は対象のコンピューターの IP アドレスに関連付けられていることが必要です。
 
<span id="_______1394Channel______"></span><span id="_______1394channel______"></span><span id="_______1394CHANNEL______"></span> *1394Channel*   
1394 チャネルの数。 有効なチャネル番号は、0 ~ 62、包括的な整数です。 *1394Channel*対象のコンピューターで使用される数に一致する必要がありますが、アダプターで選択した物理 1394 ポートに依存しません。 詳細については、次を参照してください。[を 1394 接続を手動で設定](setting-up-a-1394-cable-connection.md)します。

<span id="_______1394Protocol______"></span><span id="_______1394protocol______"></span><span id="_______1394PROTOCOL______"></span> *1394Protocol*   
1394 カーネルの接続に使用する接続プロトコルです。 これは、ほぼ常に省略できます、デバッガーは自動的に適切なプロトコルを選択するためです。 これを手動で設定して、ターゲット コンピューターが Windows XP を実行している場合*1394Protocol* 「チャネル」を等しく設定する必要があります。 ターゲット コンピューターで Windows Server 2003 以降を実行している場合*1394Protocol* 「インスタンス」と等しく設定する必要があります。 省略した場合は、デバッガーが既定の現在のターゲット コンピューターの適切なプロトコルになります。 これは、コマンドラインまたは WinDbg のグラフィカル インターフェイスではなく、環境変数を介してのみ指定できます。

<span id="_______USBString______"></span><span id="_______usbstring______"></span><span id="_______USBSTRING______"></span> *USBString*   
USB 接続文字列。 これは、/targetname ブート オプションを使用して指定した文字列と一致する必要があります。 詳細については、次を参照してください。[設定を、USB 3.0 接続を手動で](setting-up-a-usb-3-0-debug-cable-connection.md)と[設定を、USB 2.0 接続を手動で](setting-up-a-usb-2-0-debug-cable-connection.md)します。

<span id="_______ComPort______"></span><span id="_______comport______"></span><span id="_______COMPORT______"></span> *ComPort*   
COM ポートの名前。 "Com2"の形式で、または形式で指定できます"\\\\.\\com2"、数値を単純にすることはできませんが、します。 詳細については、次を参照してください。[設定を、シリアル接続を手動で](setting-up-a-null-modem-cable-connection.md)します。

<span id="_______BaudRate______"></span><span id="_______baudrate______"></span><span id="_______BAUDRATE______"></span> *BaudRate*   
ボー レート。 これは、9600、19200、38400、57600、または 115200 です。

<span id="_______VMHost______"></span><span id="_______vmhost______"></span><span id="_______VMHOST______"></span> *VMHost*   
仮想マシンをデバッグするときに*VMHost*仮想マシンが実行されている物理コンピューターの名前を指定します。 仮想マシンがカーネル デバッガー自体と同じコンピューターで実行している場合は、1 つのピリオド (.) を使用して、 *VMHost*します。 詳細については、次を参照してください。[接続を設定、仮想マシンに](attaching-to-a-virtual-machine--kernel-mode-.md)します。

<span id="_______PipeName______"></span><span id="_______pipename______"></span><span id="_______PIPENAME______"></span> *PipeName*   
デバッグ接続用の仮想マシンによって作成されたパイプの名前。

<span id="_______resets_0"></span><span id="_______RESETS_0"></span> リセット = 0  
ホストとターゲットを同期するときに、リセット パケットの数に制限はありませんをターゲットに送信できることを指定します。 このパラメーターは、特定の種類の仮想マシンをデバッグするときにのみ必要です。

<span id="_______reconnect"></span><span id="_______RECONNECT"></span> 再接続  
原因のデバッガーが自動的に切断し、読み取り/書き込みエラーが発生した場合は、パイプを再接続します。 さらに、デバッガーが開始されると、名前付きパイプが検出されなかった場合、再接続パラメーターと、表示するには、この名前のパイプを待機します。 このパラメーターは、特定の種類の仮想マシンをデバッグするときにのみ必要です。

<span id="_______-kl"></span><span id="_______-KL"></span> -kl  
ローカル カーネル モードのデバッグを実行するデバッガーをによりします。 詳細については、次を参照してください。[ローカル カーネル モード デバッグ](performing-local-kernel-debugging.md)します。

### <a name="span-idexamplesspanspan-idexamplesspanspan-idexamplesspanexamples"></a><span id="Examples"></span><span id="examples"></span><span id="EXAMPLES"></span>例

次のバッチ ファイルを設定し、COM ポート接続経由でデバッグ セッションが開始される可能性があります。

```console
set _NT_SYMBOL_PATH=d:\mysymbols
set _NT_DEBUG_PORT=com1
set _NT_DEBUG_BAUD_RATE=115200
set _NT_DEBUG_LOG_FILE_OPEN=d:\debuggers\logfile1.log
kd
```

次のバッチ ファイルは、設定を 1394 接続経由でデバッグ セッションが開始される可能性があります。

```console
set _NT_SYMBOL_PATH=d:\mysymbols
set _NT_DEBUG_BUS=1394
set _NT_DEBUG_1394_CHANNEL=44
set _NT_DEBUG_LOG_FILE_OPEN=d:\debuggers\logfile1.log
kd
```

任意の環境変数を含まない WinDbg を開始する次のコマンドラインを使用できます。

**kd -y d:\\mysymbols -k com:port=com2,baud=57600**

**kd -y d:\\mysymbols -k com:port=\\\\.\\com2,baud=115200**

**kd -y d:\\mysymbols -k 1394:channel=20,symlink=instance**

**kd -y d:\\mysymbols -k net:port=50000,key=**<em>AutoGeneratedKey</em>

 

 





