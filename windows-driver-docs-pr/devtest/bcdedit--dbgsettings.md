---
title: BCDEdit /dbgsettings
description: /Dbgsettings オプションは、コンピューターの現在のグローバルデバッガー設定を設定または表示します。
ms.assetid: df2fe55c-2752-4e0c-a4c0-004235b85e22
ms.date: 04/23/2019
keywords:
- BCDEdit/dbgsettings ドライバー開発ツール
topic_type:
- apiref
api_name:
- BCDEdit /dbgsettings
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2909e571302eff8b01f2ddd3399415e476b67f59
ms.sourcegitcommit: 1b77487f8ef5dcf8219df05524e322c27f9dcad8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/20/2020
ms.locfileid: "83707709"
---
# <a name="bcdedit-dbgsettings"></a>BCDEdit /dbgsettings


**/Dbgsettings**オプションは、コンピューターの現在のグローバルデバッガー設定を設定または表示します。 カーネルデバッガーを有効または無効にするには、 [**BCDEdit/debug**](bcdedit--debug.md)オプションを使用します。

> [!NOTE]
> BCDEdit オプションを設定する前に、コンピューターで BitLocker とセキュアブートを無効にしたり、中断したりすることが必要になる場合があります。


``` syntax
bcdedit /dbgsettings NET HOSTIP:ip PORT:port [KEY:key] [nodhcp] [newkey] [/start startpolicy] [/noumex] 

bcdedit /dbgsettings LOCAL [/start startpolicy] [/noumex] 

bcdedit /dbgsettings SERIAL [DEBUGPORT:port] [BAUDRATE:baud] [/start startpolicy] [/noumex] 

bcdedit /dbgsettings USB [TARGETNAME:targetname] [/start startpolicy] [/noumex] 

bcdedit /dbgsettings 1394 [CHANNEL:channel] [/start startpolicy] [/noumex] NOTE: The 1394 TRANSPORT IS DEPRECATED
```

<a name="parameters"></a>パラメーター
----------

## <a name="net"></a>NET

ターゲットコンピューターとホストコンピューターが、デバッグにイーサネットネットワーク接続を使用することを指定します。 このオプションを使用する場合は、 **Hostip**と**PORT**パラメーターも含める必要があります。 ターゲットコンピューターには、Windows 用デバッグツールでサポートされているネットワークアダプターが必要です。 

**Hostip:**<em>ip</em>   
ネットワークデバッグの場合は、ホストデバッガーの IP アドレスを指定します。

**キー:**<em>キー</em>   
ネットワークデバッグの場合は、接続の暗号化に使用するキーを指定します。 \[0-9 \] および a-z \[ は \] 使用できません。 **Newkey**パラメーターを指定した場合は、このパラメーターを指定しないでください。

**ポート:**<em>ポート</em>  
ネットワークデバッグの場合は、ホストデバッガーでと通信するポートを指定します。 49152以上である必要があります。

**newkey**   
ネットワークデバッグでは、接続に対して新しい暗号化キーを生成する必要があります。 **キー**パラメーターを指定した場合は、このパラメーターを指定しないでください。

**nodhcp**

*Nodhcp*を設定すると、dhcp を使用してターゲット IP アドレスを取得できなくなります。 このオプションは、小規模なルーターでも DHCP がサポートされるため、ほとんど必要ありません。 *Nodhcp*オプションは、ネットワーク上に DHCP サーバーがないことがわかっている場合にのみ使用してください。  ほとんどの場合、このオプションが設定されておらず、DHCP が有効になっていると、KDNET transport が最適に動作します。

**busparams** =*Bus. 関数*は、複数のコントローラーが存在する場合にターゲットコントローラーを指定します。 *バス番号を指定し*、*デバイス*はデバイス番号を指定し、*関数*は関数の番号を指定します。  

バスパラメーターを指定するにはデバイスマネージャーを開き、デバッグに使用するネットワークアダプターを探します。 ネットワークアダプターのプロパティページを開き、バス番号、デバイス番号、および関数番号をメモしておきます。 管理者特権でのコマンドプロンプトウィンドウで、次のコマンドを入力します。ここで、b、d、および f は、10進形式のバス、デバイス、および関数の数値です。

```console
bcdedit /set "{dbgsettings}" busparams b.d.f
```

デバッガー接続を手動で構成する場合は、バスパラメーターを指定する必要があります。 詳細については、「 [KDNET Network カーネルデバッグを手動で設定](https://docs.microsoft.com/windows-hardware/drivers/debugger/setting-up-a-network-debugging-connection)する」と「 [USB 3.0 ケーブル経由でカーネルモードのデバッグを手動で設定する](https://docs.microsoft.com/windows-hardware/drivers/debugger/setting-up-a-usb-3-0-debug-cable-connection)」を参照してください。

### <a name="examples"></a>例

次のコマンドは、デバッグにイーサネット接続を使用するようにターゲットコンピューターを構成し、ホストコンピューターの IP アドレスを指定します。 また、このコマンドは、ホストコンピューターがターゲットコンピューターに接続するために使用できるポート番号を指定します。 

``` console
bcdedit /dbgsettings net hostip:10.125.5.10 port:50000
```

次のコマンドは、グローバルデバッガー設定を、2001:48: d8: 2f: 5e: c0:42:28: 4f5b 通信 (ポート 5万) でのデバッガーホストを使用したネットワークデバッグに、グローバルデバッガー設定を設定します。

``` console
bcdedit /dbgsettings NET HOSTIPV6:2001:48:d8:2f:5e:c0:42:28:4f5b PORT:50000
```

 > [!IMPORTANT]
> ネットワークデバッグを手動で設定することは、複雑でエラーが発生しやすいプロセスです。
> ネットワークデバッグを自動的に設定する方法については、「 [KDNET Network カーネルデバッグの自動](https://docs.microsoft.com/windows-hardware/drivers/debugger/setting-up-a-network-debugging-connection-automatically)セットアップ」を参照してください。 すべてのデバッガーユーザーには、KDNET ユーティリティを使用することを**強く**お勧めします。

手動セットアップの詳細については、「[ネットワークケーブル経由でカーネルモードのデバッグを手動で設定](https://docs.microsoft.com/windows-hardware/drivers/debugger/setting-up-a-network-debugging-connection)する」を参照してください。


## <a name="local"></a>LOCAL

**Local**オプションは、グローバルデバッグオプションをローカルデバッグに設定します。 これは、1台のコンピューターでのカーネルモードのデバッグです。 つまり、デバッガーは、デバッグされているのと同じコンピューター上で実行されます。 ローカルデバッグでは、状態を調べることができますが、OS の実行を停止するカーネルモードプロセスを中断することはできません。

### <a name="example"></a>例

グローバルデバッガー設定をローカルデバッグに設定するコマンドを次に示します。

``` console
bcdedit /dbgsettings LOCAL
```

ローカルオプションは、Windows 8.0 および Windows Server 2012 以降で使用できます。

ローカルカーネルモードのデバッグを手動で設定する方法については、「 [1 台のコンピューターのローカルカーネルデバッグを手動](https://docs.microsoft.com/windows-hardware/drivers/debugger/setting-up-local-kernel-debugging-of-a-single-computer-manually)で設定する」を参照してください。

## <a name="serial"></a>シリアル

ターゲットコンピューターとホストコンピューターがデバッグにシリアル接続を使用することを指定します。 このオプションを使用する場合は、 **DEBUGPORT**パラメーターと**ボーレート**パラメーターを指定する必要があります。

**ボーレート:**<em>ボー</em>   
使用するボーレートを指定します。 このパラメーターは省略可能です。 *Baud*の有効な値は、9600、19200、38400、57600、および115200です。 既定のボーレートは 115200 bps です。

**DEBUGPORT:**<em>ポート</em>   
 デバッグポートとして使用するシリアルポートを指定します。 この設定は省略可能です。 既定のポートは**1** (COM 1) です。

### <a name="example"></a>例

デバッグにシリアル接続を使用するように対象のコンピューターを構成するコマンドを次に示します。 このコマンドは、デバッグ接続が COM1 を使用し、115200のボーレートを使用することも指定します。 

``` console
bcdedit /dbgsettings serial debugport:1 baudrate:115200
```
詳細については、「[シリアルケーブル経由でカーネルモードのデバッグを手動で設定する](https://docs.microsoft.com/windows-hardware/drivers/debugger/setting-up-a-null-modem-cable-connection)」を参照してください。

## <a name="usb"></a>USB   
ターゲットコンピューターとホストコンピューターがデバッグに USB 2.0 または USB 3.0 接続を使用するように指定します。 このオプションを使用する場合は、 **TARGETNAME**パラメーターも含める必要があります。 

**Targetname:** <em>targetname</em>   
ターゲット名に使用する文字列値を指定します。 TargetName はターゲットコンピューターの正式な名前である必要はないことに注意してください。次の制限を満たしている限り、任意の文字列を指定できます。

- 文字列では、大文字と小文字の組み合わせで TargetName 内の任意の場所に "debug" を含めることはできません。 たとえば、targetname 内の任意の場所で "DeBuG" または "DEBUG" を使用すると、デバッグは正しく機能しません。
- 文字列内の文字は、ハイフン (-)、アンダースコア (_)、0 ~ 9 の数字、および文字 A ~ Z (大文字または小文字) のみです。
- 文字列の最大長は24文字です。


### <a name="example"></a>例

デバッグに USB 接続を使用するように対象のコンピューターを構成するコマンドを次に示します。 また、このコマンドは、ホストコンピューターがターゲットコンピューターに接続するために使用できるターゲット名を指定します。 

``` console
bcdedit /dbgsettings usb targetname:myTarget
```

詳細については、次を参照してください。

- [USB 3.0 ケーブル経由のカーネルモード デバッグの手動設定](https://docs.microsoft.com/windows-hardware/drivers/debugger/setting-up-a-usb-3-0-debug-cable-connection)
- [USB 2.0 ケーブルを経由のカーネルモード デバッグの手動設定](https://docs.microsoft.com/windows-hardware/drivers/debugger/setting-up-a-usb-2-0-debug-cable-connection)



## <a name="1394"></a>1394   

> [!IMPORTANT]
> 1394トランスポートは、Windows 10 バージョン1607以前で使用できます。 これは、以降のバージョンの Windows では使用できません。 イーサネットを使用して KDNET などの他のトランスポートにプロジェクトを移行する必要があります。 そのトランスポートの詳細については、「 [KDNET Network カーネルデバッグの自動](https://docs.microsoft.com/windows-hardware/drivers/debugger/setting-up-a-network-debugging-connection-automatically)セットアップ」を参照してください。
>

ターゲットコンピューターとホストコンピューターがデバッグに IEEE 1394 (FireWire) 接続を使用することを指定します。 このオプションを使用する場合は、 **CHANNEL**パラメーターも含めることができます。 

**チャネル:**<em>チャネル</em>   
(接続の種類が**1394**の場合にのみ使用されます。)使用する1394チャネルを指定します。 *Channel*の値には、0 ~ 62 の10進数の整数を指定し、ホストコンピューターで使用されるチャネル番号と一致させる必要があります。 このパラメーターで指定したチャネルは、アダプターで選択されている物理1394ポートに依存しません。 *Channel*の既定値は0です。

詳細については、「 [1394 ケーブル経由でカーネルモードのデバッグを手動で設定する](https://docs.microsoft.com/windows-hardware/drivers/debugger/setting-up-a-1394-cable-connection)」を参照してください。

## <a name="general-debugger-settings"></a>デバッガーの全般設定

**/start** <em>startpolicy</em>   
このオプションは、デバッガーの開始ポリシーを指定します。 次の表は、 *startpolicy*のオプションを示しています。

|オプション|説明|
|--- |--- |
|ACTIVE|カーネルデバッガーがアクティブであることを指定します。|
|AUTOENABLE|例外またはその他の重大なイベントが発生したときに、カーネルデバッガーが自動的に有効になるように指定します。 それまでは、デバッガーはアクティブですが、無効になっています。|
|DISABLE|Kdbgctrl キーを押して enable ブロックをクリアすると、カーネルデバッガーが有効になることを指定します。 それまでは、デバッガーはアクティブですが、無効になっています。|
 

開始ポリシーが指定されていない場合、[アクティブ] が既定値になります。

**/noumex**   
カーネルデバッガーがユーザーモードの例外を無視することを指定します。 既定では、カーネルデバッガーは、状態の \_ ブレークポイントやステータスのシングルステップなど、特定のユーザーモードの例外に対して中断し \_ \_ ます。 **/Noumex**パラメーターは、プロセスにアタッチされたユーザーモードのデバッガーがない場合にのみ有効です。

### <a name="comments"></a>説明

**/Dbgsettings**オプションは、デバッグ設定を構成しますが、デバッグは有効にしません。 特定のブートエントリのデバッグを有効にするには、 **/debug**オプションを使用する必要があります。 特定のブートエントリにデバッグ設定が指定されていない場合は、既定のデバッグ設定が使用されます。 

次の表に、dbgsettings の既定値を示します。

|dbgsetting パラメーター|既定値|
|--- |--- |
|debugtype|ローカル|
|debugstart|アクティブ|
|noumex|はい|


<a name="see-also"></a>関連項目
--------

Windows デバッグツールの詳細については、「 [Windows デバッグ](https://docs.microsoft.com/windows-hardware/drivers/debugger/index)」を参照してください。 

カーネルモードのデバッグセッションの設定と構成の詳細については、「[カーネルモードデバッグを手動で設定](https://docs.microsoft.com/windows-hardware/drivers/debugger/setting-up-kernel-mode-debugging-in-windbg--cdb--or-ntsd)する」と「 [KDNET Network カーネルデバッグを自動的に設定](https://docs.microsoft.com/windows-hardware/drivers/debugger/setting-up-a-network-debugging-connection-automatically)する」を参照してください。



 





