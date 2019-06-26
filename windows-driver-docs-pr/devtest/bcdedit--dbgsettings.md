---
title: BCDEdit /dbgsettings
description: /Dbgsettings オプションを設定またはコンピューターの現在のグローバルなデバッガ設定を表示します。
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
ms.openlocfilehash: 8e5441240e79c050ab937d5e7b581eb991598393
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371669"
---
# <a name="bcdedit-dbgsettings"></a>BCDEdit /dbgsettings


**/Dbgsettings**オプションを設定またはコンピューターの現在のグローバルなデバッガ設定を表示します。 有効またはカーネル デバッガーを無効にする、使用、 [ **BCDEdit/debug** ](bcdedit--debug.md)オプション。

> [!NOTE]
> BCDEdit のオプションを設定する前に、無効にするか、またはコンピューターの BitLocker とセキュア ブートを中断する必要があります。


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

ターゲット マシンとホスト コンピューターを使用して、イーサネット ネットワーク接続のデバッグを指定します。 このオプションを使用する場合、**終点アドレス**と**ポート**パラメーターを含めることは同様です。 ターゲット コンピューターでは、Windows のツールをデバッグでサポートされているネットワーク アダプターが必要です。 

**終点アドレス:** <em>ip</em>   
ネットワークのデバッグは、ホストのデバッガーの IP アドレスを指定します。

**キー:** <em>キー</em>   
ネットワークのデバッグにも、接続の暗号化に使用するキーを指定します。 \[0 ~ 9\]と\[a ~ z\]のみ許可します。 指定した場合、このパラメーターを指定して、 **newkey**パラメーター。

**ポート:** <em>ポート</em>  
ネットワークのデバッグにも、ホストのデバッガーとの通信にポートを指定します。 49152 またはそれ以降にする必要があります。

**newkey**   
ネットワークのデバッグは、接続の新しい暗号化キーを生成することを指定します。 指定した場合、このパラメーターを指定して、**キー**パラメーター。

**nodhcp**

設定*nodhcp*ターゲット IP アドレスを取得する DHCP を使用できないようにします。 このオプションは、小さなルーターで DHCP のサポートを提供するために必要なことはほとんどありません。 *Nodhcp*オプションは、ネットワーク上の DHCP サーバーがないことがわかっている場合にのみ使用する必要があります。  KDNET トランスポートはほとんどの場合はこのオプションが設定されていないと、DHCP が有効になっているときに最適な動作します。

**busparams**=*Bus.Device.Function*複数のコント ローラーが存在する場合は、ターゲット コント ローラーを指定します。 *バス*バス番号を指定します*デバイス*デバイス番号を指定し、*関数*関数の数を指定します。  

デバイス マネージャーを開き、バスのパラメーターを指定し、デバッグに使用するネットワーク アダプターを探します。 ネットワーク アダプターのプロパティ ページを開き、バス番号、デバイスの数、および関数の数をメモしておきます。 管理者特権のコマンド プロンプト ウィンドウで、b、d、および f、bus、デバイス、および関数に数値が 10 進形式、次のコマンドを入力します。

```console
bcdedit /set "{dbgsettings}" busparams b.d.f
```

デバッガーの接続を手動で構成している場合は、バス パラメーターを指定する必要があります。 詳細については、次を参照してください。 [KDNET ネットワーク カーネル デバッグ手作業でセットアップ](https://docs.microsoft.com/windows-hardware/drivers/debugger/setting-up-a-network-debugging-connection)と[カーネル モード デバッグのセットアップを手動で USB 3.0 ケーブル](https://docs.microsoft.com/windows-hardware/drivers/debugger/setting-up-a-usb-3-0-debug-cable-connection)します。

### <a name="examples"></a>例

次のコマンドは、デバッグに、イーサネット接続を使用するターゲット コンピューターを構成し、ホスト コンピューターの IP アドレスを指定します。 コマンドには、ホスト コンピューターを使用して、ターゲット コンピューターに接続するポート番号も指定します。 

``` console
bcdedit /dbgsettings net hostip:10.125.5.10 port:50000
```

次のコマンドは、ネットワーク 2001:48:d8:2f:5e:c0:42:28:4f5b ポート 50000 上での通信でデバッガー ホストで IPv6 を使用したデバッグの設定、グローバルなデバッガを設定します。

``` console
bcdedit /dbgsettings NET HOSTIPV6:2001:48:d8:2f:5e:c0:42:28:4f5b PORT:50000
```

 > [!IMPORTANT]
> デバッグを手動でネットワークの設定は、複雑で、エラーが発生しやすいプロセスです。
> デバッグが自動的にネットワークを設定するを参照してください。[設定を KDNET ネットワーク カーネル デバッグを自動的に](https://docs.microsoft.com/windows-hardware/drivers/debugger/setting-up-a-network-debugging-connection-automatically)します。 KDNET ユーティリティを使用して**強く**デバッガーのすべてのユーザーをお勧めします。

手動セットアップの詳細については、次を参照してください。[カーネル モード デバッグのセットアップを手動でのネットワーク ケーブル](https://docs.microsoft.com/windows-hardware/drivers/debugger/setting-up-a-network-debugging-connection)します。


## <a name="local"></a>LOCAL

**ローカル**オプションは、ローカル デバッグにグローバルなデバッグ オプションを設定します。 これは、1 台のコンピューターでカーネル モードのデバッグです。 つまり、デバッガーは、デバッグ中のと同じコンピューターで実行されます。 ローカル デバッグには、ことになる実行を停止する OS カーネル モード プロセスに、状態が中断しないを確認できます。

### <a name="example"></a>例

次のコマンドでは、ローカル デバッグに、グローバルなデバッガ設定を設定します。

``` console
bcdedit /dbgsettings LOCAL
```

ローカル オプションは、以降 Windows 8.0 および Windows Server 2012 で利用できます。

ローカル カーネル モードの設定については、手動でのデバッグを参照してください[ローカル カーネル デバッグのセットアップの 1 つのコンピューターを手動で](https://docs.microsoft.com/windows-hardware/drivers/debugger/setting-up-local-kernel-debugging-of-a-single-computer-manually)します。

## <a name="serial"></a>シリアル

ターゲット マシンとホスト マシンが使用するシリアル接続のデバッグを指定します。 このオプションを使用する場合、 **DEBUGPORT**と**BAUDRATE**パラメーターを指定する必要があります。

**BAUDRATE:** <em>ボー</em>   
使用するボー レートを指定します。 このパラメーターは省略可能です。 有効な値*ボー* 9600、38400、19200、57600、および 115200 です。 既定のボー レートは、115200 bps です。

**DEBUGPORT:** <em>ポート</em>   
 デバッグ ポートとして使用するシリアル ポートを指定します。 この設定は省略可能です。 既定のポートは**1** (COM 1)。

### <a name="example"></a>例

次のコマンドは、シリアル接続を使用して、デバッグの対象となるコンピューターを構成します。 コマンドでは、COM2、および、115,200 ボー レートに、デバッグの接続が使用するも指定します。 

``` console
bcdedit /dbgsettings serial debugport:1 baudrate:115200
```
詳細については、次を参照してください。[カーネル モード デバッグのセットアップをシリアル ケーブルを手動で](https://docs.microsoft.com/windows-hardware/drivers/debugger/setting-up-a-null-modem-cable-connection)します。

## <a name="usb"></a>USB   
ターゲット マシンとホスト マシンは接続を使用、USB 2.0 接続または USB 3.0 のデバッグを指定します。 このオプションを使用する場合、 **TARGETNAME**パラメーターを含めることは同様です。 

**TARGETNAME:** <em>targetname</em>   
ターゲット名を使用する文字列値を指定します。 対象のコンピューターの公式名である TargetName がないことに注意してください。これらの制限を満たしている限り、作成した任意の文字列を指定できます。

- 文字列は使用できません"debug"任意の場所で任意の大文字または小文字で TargetName します。 "DeBuG"を使用した場合または"DEBUG"任意の場所、targetname では、デバッグは正しく動きません。
- 文字列内の唯一の文字は、ハイフン (-)、アンダー、数字 0 ~ 9 の文字 A ~ Z (大文字または小文字) です。
- 文字列の最大長は、24 文字です。


### <a name="example"></a>例

次のコマンドは、デバッグに USB 接続を使用する対象のコンピュータを構成します。 コマンドには、ホスト コンピューターがターゲット コンピューターへの接続に使用できるターゲットの名前も指定します。 

``` console
bcdedit /dbgsettings usb targetname:myTarget
```

詳しくは、次のトピックをご覧ください。

- [カーネル モード経由でのデバッグ、USB 3.0 ケーブル手動での設定](https://docs.microsoft.com/windows-hardware/drivers/debugger/setting-up-a-usb-3-0-debug-cable-connection)
- [カーネル モード経由でのデバッグ、USB 2.0 ケーブル手動での設定](https://docs.microsoft.com/windows-hardware/drivers/debugger/setting-up-a-usb-2-0-debug-cable-connection)



## <a name="1394"></a>1394   

> [!IMPORTANT]
> 1394 トランスポートは、Windows 10 バージョン 1607 およびそれ以前で使用できます。 以降のバージョンの Windows でご利用いただけません。 イーサネットを使用して KDNET などの他のトランスポートにプロジェクトを移行する必要があります。 トランスポートの詳細については、次を参照してください。[設定を KDNET ネットワーク カーネル デバッグを自動的に](https://docs.microsoft.com/windows-hardware/drivers/debugger/setting-up-a-network-debugging-connection-automatically)します。
>

ターゲット マシンとホスト マシンが使用する IEEE 1394 (FireWire) 接続のデバッグを指定します。 このオプションを使用する場合、**チャネル**パラメーターに指定できますも。 

**チャネル:** <em>チャネル</em>   
(接続の種類が場合にのみ使用**1394**)。使用する、1394 チャネルを指定します。 値は、*チャネル*0 ~ 62、両端を含む 10 進数の整数である必要があり、ホスト コンピューターで使用されるチャネル番号に一致する必要があります。 このパラメーターで指定されたチャネルは、アダプターで選択した物理 1394 ポートに依存しません。 既定値*チャネル*は 0 です。

詳細については、次を参照してください。[カーネル モード デバッグのセットアップを手動での 1394 ケーブル](https://docs.microsoft.com/windows-hardware/drivers/debugger/setting-up-a-1394-cable-connection)します。

## <a name="general-debugger-settings"></a>デバッガーの全般設定

**/start** <em>startpolicy</em>   
このオプションは、デバッガー開始のポリシーを指定します。 次の表のオプションを示します、 *startpolicy*します。

|構成方法|説明|
|--- |--- |
|ACTIVE|カーネル デバッガーがアクティブであるを指定します。|
|AUTOENABLE|カーネル デバッガーが例外またはその他の重要なイベントが発生したときに自動的に有効なことを指定します。 それまでは、デバッガーはアクティブですが、無効にします。|
|無効にします。|有効にするブロックをオフに kdbgctrl を入力すると、カーネル デバッガーが有効になっているを指定します。 それまでは、デバッガーはアクティブですが、無効にします。|
 

開始のポリシーが指定されていない場合は、アクティブは、既定値です。

**/noumex**   
カーネル デバッガーがユーザー モード例外を無視することを指定します。 既定では、カーネル デバッガーが中断特定の状態などのユーザー モード例外\_ブレークポイントと状態\_単一\_手順。 **/Noumex**パラメータは、ユーザー モード デバッガーをプロセスにアタッチされていない場合にのみ有効です。

### <a name="comments"></a>コメント

**/Dbgsettings**オプションはデバッグの設定を構成しますが、デバッグを有効にしません。 使用する必要があります、 **/debug**特定のブート エントリのデバッグを有効にするにはオプションです。 特定のブート エントリに指定されたデバッグの設定がない場合は、既定のデバッグ設定が使用されます。 

次の表に、dbgsettings の既定値が表示されます。

|dbgsetting パラメーター|既定値|
|--- |--- |
|debugtype|ローカル|
|debugstart|Active|
|noumex|〇|


<a name="see-also"></a>関連項目
--------

Windows デバッグ ツールの詳細については、次を参照してください。 [Windows デバッグ](https://docs.microsoft.com/windows-hardware/drivers/debugger/index)します。 

設定して、カーネル モードの構成についてはデバッグ セッションを参照してください[カーネル モード デバッグ手作業でセットアップ](https://docs.microsoft.com/windows-hardware/drivers/debugger/setting-up-kernel-mode-debugging-in-windbg--cdb--or-ntsd)と[設定を KDNET ネットワーク カーネル デバッグを自動的に](https://docs.microsoft.com/windows-hardware/drivers/debugger/setting-up-a-network-debugging-connection-automatically)します。



 





