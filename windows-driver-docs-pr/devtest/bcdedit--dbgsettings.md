---
title: BCDEdit/dbgsettings
description: /Dbgsettings オプションを設定またはコンピューターの現在のグローバルなデバッガ設定を表示します。
ms.assetid: df2fe55c-2752-4e0c-a4c0-004235b85e22
ms.date: 07/02/2018
keywords:
- BCDEdit/dbgsettings ドライバー開発ツール
topic_type:
- apiref
api_name:
- BCDEdit /dbgsettings
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2f2bda2c91ab1de08815a61f3ee85080cb625381
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549053"
---
# <a name="bcdedit-dbgsettings"></a>BCDEdit/dbgsettings


**/Dbgsettings**オプションを設定またはコンピューターの現在のグローバルなデバッガ設定を表示します。 有効またはカーネル デバッガーを無効にする、使用、 [ **BCDEdit/debug** ](bcdedit--debug.md)オプション。

> [!NOTE]
> BCDEdit のオプションを設定する前に、無効にするか、またはコンピューターの BitLocker とセキュア ブートを中断する必要があります。

 

``` syntax
bcdedit /dbgsettings SERIAL [DEBUGPORT:port] [BAUDRATE:baud] [/start startpolicy] [/noumex] 

bcdedit /dbgsettings 1394 [CHANNEL:channel] [/start startpolicy] [/noumex] 

bcdedit /dbgsettings USB [TARGETNAME:targetname] [/start startpolicy] [/noumex] 

bcdedit /dbgsettings NET HOSTIP:ip PORT:port [KEY:key] [nodhcp] [newkey] [/start startpolicy] [/noumex] 
```

<a name="parameters"></a>パラメーター
----------

**シリアル**   
ターゲット マシンとホスト マシンが使用するシリアル接続のデバッグを指定します。 このオプションを使用する場合、 **DEBUGPORT**と**BAUDRATE**パラメーターに指定できますも。 詳細については、次を参照してください。[カーネル モード デバッグのセットアップをシリアル ケーブルを手動で](https://msdn.microsoft.com/library/windows/hardware/ff556867)します。

**1394**   
ターゲット マシンとホスト マシンが使用する IEEE 1394 (FireWire) 接続のデバッグを指定します。 このオプションを使用する場合、**チャネル**パラメーターに指定できますも。 詳細については、次を参照してください。[カーネル モード デバッグのセットアップを手動での 1394 ケーブル](https://msdn.microsoft.com/library/windows/hardware/ff556866)します。

**USB**   
ターゲット マシンとホスト マシンは接続を使用、USB 2.0 接続または USB 3.0 のデバッグを指定します。 このオプションを使用する場合、 **TARGETNAME**パラメーターを含めることは同様です。 詳しくは、次のトピックをご覧ください。

-   [カーネル モード経由でのデバッグ、USB 3.0 ケーブル手動での設定](https://msdn.microsoft.com/library/windows/hardware/hh439372)
-   [カーネル モード経由でのデバッグ、USB 2.0 ケーブル手動での設定](https://msdn.microsoft.com/library/windows/hardware/ff556869)

**NET**   
ターゲット マシンとホスト コンピューターを使用して、イーサネット ネットワーク接続のデバッグを指定します。 このオプションを使用する場合、**終点アドレス**と**ポート**パラメーターを含めることは同様です。 ターゲット コンピューターでは、Windows のツールをデバッグでサポートされているネットワーク アダプターが必要です。 詳しくは、次のトピックをご覧ください。

-   [カーネル モードのネットワーク ケーブル経由でのデバッグを手動での設定](https://msdn.microsoft.com/library/windows/hardware/hh439346)

**地元の**   
**ローカル**オプションは、ローカル デバッグにグローバルなデバッグ オプションを設定します。 これは、1 台のコンピューターでカーネル モードのデバッグです。 つまり、デバッガーは、デバッグ中のと同じコンピューターで実行されます。 ローカル デバッグには、ことになる実行を停止する OS カーネル モード プロセスに、状態が中断しないを確認できます。

ローカル カーネル モードの設定については、手動でのデバッグを参照してください[ローカル カーネル デバッグのセットアップの 1 つのコンピューターを手動で](https://msdn.microsoft.com/library/windows/hardware/dn553412)します。

ローカル オプションは、以降 Windows 8.0 および Windows Server 2012 で利用できます。

**BAUDRATE:**<em>ボー</em>   
(接続の種類が場合にのみ使用**シリアル**)。使用するボー レートを指定します。 このパラメーターは省略可能です。 有効な値*ボー* 9600、38400、19200、57600、および 115200 です。 既定のボー レートは、115200 bps です。

> [!NOTE]
> Windows の特殊な管理コンソール (SAC) アプリケーションは、シリアル ポート経由のカーネル モードのデバッグ用に構成されているターゲット コンピューター上で実行している、SAC アプリケーションがデバッガー接続の切断にあります。 このイベントは、デバッガーの接続が確立された後に、COM ポートのボー値が変更されるために発生します。 デバッガーを実行する前に、SAC アプリケーションを閉じるか、9600 にデバッガー COM ポートのボー値を変更します。

 
**チャネル:**<em>チャネル</em>   
(接続の種類が場合にのみ使用**1394**)。使用する、1394 チャネルを指定します。 値は、*チャネル*0 ~ 62、両端を含む 10 進数の整数である必要があり、ホスト コンピューターで使用されるチャネル番号に一致する必要があります。 このパラメーターで指定されたチャネルは、アダプターで選択した物理 1394 ポートに依存しません。 既定値*チャネル*は 0 です。

**DEBUGPORT:**<em>ポート</em>   
(接続の種類が場合にのみ使用**シリアル**)。デバッグ ポートとして使用するシリアル ポートを指定します。 この設定は省略可能です。 既定のポートは**1** (COM 1)。

**終点アドレス:**<em>ip</em>   
(接続の種類が場合にのみ使用**NET**)。ネットワークのデバッグは、ホストのデバッガーの IPv4 アドレスを指定します。

**キー:**<em>キー</em>   
ネットワークのデバッグにも、接続の暗号化に使用するキーを指定します。 \[0 ~ 9\]と\[a ~ z\]のみ許可します。 指定した場合、このパラメーターを指定して、 **newkey**パラメーター。

**newkey**   
ネットワークのデバッグは、接続の新しい暗号化キーを生成することを指定します。 指定した場合、このパラメーターを指定して、**キー**パラメーター。

**nodhcp**   
ネットワークのデバッグ ターゲットの IP アドレスを取得する DHCP の使用ができなくなります。

<strong>ポート:</strong>*ポート*   
ネットワークのデバッグにも、ホストのデバッガーとの通信にポートを指定します。 49152 またはそれ以降にする必要があります。

<strong>TARGETNAME:</strong>*targetname*   
(接続の種類が場合にのみ使用**USB**)。ターゲット名を使用する文字列値を指定します。 この文字列は、任意の値を指定できます。

<strong>\start</strong> *startpolicy*   
このオプションは、デバッガー開始のポリシーを指定します。 次の表のオプションを示します、 *startpolicy*します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">構成方法</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>アクティブ</strong></p></td>
<td align="left"><p>カーネル デバッガーがアクティブであるを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>AUTOENABLE</strong></p></td>
<td align="left"><p>カーネル デバッガーが例外またはその他の重要なイベントが発生したときに自動的に有効なことを指定します。 それまでは、デバッガーはアクティブですが、無効にします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>無効にします。</strong></p></td>
<td align="left"><p>入力すると、カーネル デバッガーが有効になっているを指定します。 <strong>kdbgctrl</strong>を有効にするブロックをオフにします。 それまでは、デバッガーはアクティブですが、無効にします。</p></td>
</tr>
</tbody>
</table>

 

開始のポリシーが指定されていない場合は、アクティブは、既定値です。

</strong>/noumex</strong>   
カーネル デバッガーがユーザー モード例外を無視することを指定します。 既定では、カーネル デバッガーが中断特定の状態などのユーザー モード例外\_ブレークポイントと状態\_単一\_手順。 **/Noumex**パラメータは、ユーザー モード デバッガーをプロセスにアタッチされていない場合にのみ有効です。

### <a name="comments"></a>コメント

**/Dbgsettings**オプションは、グローバルのデバッグ設定を構成しますが、デバッグを有効にしません。 使用する必要があります、 **/debug**特定のブート エントリのデバッグを有効にするにはオプションです。 特定のブート エントリに指定されたデバッグの設定がない場合は、グローバルのデバッグの設定が使用されます。 グローバル設定を上書きするには、使用する必要があります、 [ **BCDEdit/set** ](bcdedit--set.md)コマンドし、デバッグのパラメーターと値のペアと共にブート エントリの ID を指定します。

グローバルな設定の既定値は、115,200 ボー レートで COM1 を使用してシリアル通信です。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">/dbgsetting parameter</th>
<th align="left">既定値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>接続の種類</p></td>
<td align="left"><p>シリアル</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>DEBUGPORT:</strong><em>ポート</em></p></td>
<td align="left"><p>1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>BAUDRATE:</strong><em>レート</em></p></td>
<td align="left"><p>115200</p></td>
</tr>
</tbody>
</table>

 

Windows デバッグ ツールの詳細については、次を参照してください。 [Windows デバッグ](https://msdn.microsoft.com/library/windows/hardware/ff551063)します。 設定して、カーネル モードの構成についてはデバッグ セッションを参照してください[カーネル モード デバッグ手作業でセットアップ](https://msdn.microsoft.com/library/windows/hardware/hh439378)します。

<a name="examples"></a>例
--------

次のコマンドは、デバッグに、イーサネット接続を使用するターゲット コンピューターを構成し、ホスト コンピューターの IP アドレスを指定します。 コマンドには、ホスト コンピューターを使用して、ターゲット コンピューターに接続するポート番号も指定します。 詳細については、次を参照してください。[カーネル モード デバッグのセットアップを手動でのネットワーク ケーブル](https://msdn.microsoft.com/library/windows/hardware/hh439346)します。

``` syntax
bcdedit /dbgsettings net hostip:10.125.5.10 port:50000
```

次のコマンドは、デバッグに 1394 接続を使用する対象のコンピュータを構成します。 コマンドには、ホスト コンピューターがターゲット コンピューターへの接続に使用できるチャネル数も指定します。 詳細については、次を参照してください。[カーネル モード デバッグのセットアップを手動での 1394 ケーブル](https://msdn.microsoft.com/library/windows/hardware/ff556866)します。

``` syntax
bcdedit /dbgsettings 1394 channel:1
```

次のコマンドは、デバッグに USB 接続を使用する対象のコンピュータを構成します。 コマンドには、ホスト コンピューターがターゲット コンピューターへの接続に使用できるターゲットの名前も指定します。 詳細については、次を参照してください。[カーネル モード デバッグのセットアップを手動で USB 3.0 ケーブル](https://msdn.microsoft.com/library/windows/hardware/hh439372)と[カーネル モード デバッグのセットアップを手動で USB 2.0 ケーブル](https://msdn.microsoft.com/library/windows/hardware/ff556869)します。

``` syntax
bcdedit /dbgsettings usb targetname:myTarget
```

次のコマンドは、シリアル接続を使用して、デバッグの対象となるコンピューターを構成します。 コマンドでは、COM2、および、115,200 ボー レートに、デバッグの接続が使用するも指定します。 詳細については、次を参照してください。[カーネル モード デバッグのセットアップをシリアル ケーブルを手動で](https://msdn.microsoft.com/library/windows/hardware/ff556867)します。

``` syntax
bcdedit /dbgsettings serial debugport:2 baudrate:115200
```

<a name="see-also"></a>関連項目
--------

[カーネル モードのデバッグを手動での設定](https://msdn.microsoft.com/library/windows/hardware/hh439378)


 





