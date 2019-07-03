---
title: バグ チェック 0x7B INACCESSIBLE_BOOT_DEVICE
description: INACCESSIBLE_BOOT_DEVICE のバグ チェックでは、0x0000007B の値を持ちます。 このバグ チェックでは、Microsoft Windows オペレーティング システムが起動中にシステム パーティションへのアクセスを失ったことを示します。
ms.assetid: 0dfcb519-4ea3-4419-a1c3-60fdff96404d
keywords:
- バグ チェック 0x7B INACCESSIBLE_BOOT_DEVICE
- INACCESSIBLE_BOOT_DEVICE
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- INACCESSIBLE_BOOT_DEVICE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: abedcab42ac95183cc62ac15566c2eef3565ca89
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67519191"
---
# <a name="bug-check-0x7b-inaccessiblebootdevice"></a>バグ チェック 0x7B:アクセスできない\_ブート\_デバイス


アクセス不可能\_ブート\_デバイス バグ チェックが 0x0000007B の値を持ちます。 このバグ チェックでは、Microsoft Windows オペレーティング システムが起動中にシステム パーティションへのアクセスを失ったことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


## <a name="inaccessiblebootdevice-parameters"></a>アクセスできない\_ブート\_デバイス パラメーター


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>UNICODE_STRING 構造体のアドレス、またはマウントされていないデバイス オブジェクトのアドレス</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>0</p></td>
</tr>
</tbody>
</table>

 

パラメーター 1 の意味を特定するには、データを指すを確認します。 このアドレスにある最初の単語 (USHORT) が偶数の場合、パラメーター 1 は、Unicode 文字列の先頭が。 このアドレスにある最初の単語 (USHORT) が 0x3 の場合は、パラメーター 1 がデバイス オブジェクトの最初のフィールド (型) にします。

-   このパラメーターは、デバイス オブジェクトをポイントしている場合、ブート デバイスの読み取りに想定されたファイル システムを初期化できませんでしただけ認識しなかったのか、データ ブート デバイスにファイル システム構造体として。 このような状況では、指定したデバイス オブジェクトは、マウントされていないオブジェクトが。

-   このパラメーターは、Unicode 文字列をポイントしている場合は、このアドレスにある最初の 8 バイトを読み取る必要があります。 これらのバイトは、UNICODE を形成\_が次のように定義されている文字列の構造体。

    ```cpp
    USHORT Length;
    USHORT MaximumLength;
    PWSTR Buffer;
    ```

    **長さ**フィールドでは、文字列の実際の長さ。 **バッファー**フィールドの文字列の先頭を指します (**バッファー**は常に少なくとも 0x80000000 になります)。

    実際の文字列には、デバイスからのブートを試行した中の Advanced RISC コンピューティング (弧) 仕様名が含まれています。 円弧の名前は、円弧環境内のデバイスを識別するために汎用的な方法です。

<a name="cause"></a>原因
-----

アクセス不可能\_ブート\_デバイス バグ チェックがブート デバイス エラーのために頻繁に発生します。 I/O システムの初期化中に、ブート デバイス ドライバーをブート デバイス (通常はハード ディスク) を初期化するために失敗した可能性があります。

ファイル システムの初期化は、ブート デバイスにデータを認識しなかったため、失敗した可能性があります。 また、システム パーティションを再分割、BIOS 構成を変更またはディスク コント ローラーのインストールは、このエラーを誘発可能性があります。

このエラーは、ハードウェアの互換性のないディスクも発生します。 システムの初期セットアップ時にエラーが発生した場合、システムがサポートされていないディスクのコント ローラーにインストールされている可能性があります。 一部のディスク コント ローラーには、Windows の起動時に存在する追加のドライバーが必要です。

<a name="resolution"></a>解決方法
----------

このエラーは、常に、システムの起動中に発生します。 デバッグは、困難になる可能性があるために、デバッガーの接続が確立される前にこのエラー頻繁に発生します。 さらに、OS にアクセスできないし、OS が起動されていない十分にこれらのサブシステムを開始すると、エラー ログを空にすることがあります。

**\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\\***

**Windows を起動できない場合**

**\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\\***

でこの終了コードを受信し、Windows は、OS に前方に起動しない場合は、次の操作を再試行してください。

**最近のハードウェア変更を元に戻す**

最近追加されたハードウェア、特にハード ディスク ドライブや、エラーが解決されたかどうかをコント ローラーを取り外します。 問題のあるハードウェアがハード ディスク ドライブの場合は、ディスク ファームウェアのバージョンが Windows オペレーティング システムのバージョンと互換性ない可能性があります。 更新プログラムの製造元に問い合わせてください。 ハードウェアの別の部分を削除して、エラーが解決、IRQ や I/O ポートの競合があります。 製造元の指示に従って新しいデバイスを再構成します。

AHCI、BIOS で従来からコント ローラー モードを変更するなど、BIOS 設定を変更が加えられた最近の場合は、それらの変更を元に戻します。 詳細については、「<https://en.wikipedia.org/wiki/Advanced_Host_Controller_Interface>」を参照してください。

**記憶域デバイスの互換性のためのチェック**

すべてのハード ディスク ドライバー、ハード ディスク コント ローラー、およびその他のすべての記憶域アダプターがインストールされたバージョンの Windows と互換性があることを確認します。 互換性についての情報を取得するなど、 [Windows 10 の仕様](https://www.microsoft.com/windows/windows-10-specifications)します。

**BIOS およびファームウェアを更新します。**

システムの BIOS と記憶域コント ローラー ファームウェアの更新プログラムの可用性を確認します。

**メディアの作成ツールを使用して、起動可能な USB ドライブまたは DVD を作成するには**

起動可能な USB ドライブまたは DVD を作成する別のコンピューターを使用して、メディアの作成ツールを使用します。 セットアップ ファイルをクリックするか、USB から起動して、クリーン インストールを実行するのにには、これを使用します。

詳細については、次を参照してください。 [Get Windows 10](https://www.microsoft.com/software-download/windows10)します。

クイックの BIOS ブートなどの機能を無効にする必要がありますまたはブート デバイスの優先度 メニューに到達できないことに注意します。 FDD (FlashDiskDrive) または HDD ではなく DVD からブートする BIOS のメニューで、ブート シーケンスの優先順位を変更します。

**一般的なブート メニュー キー**

ブート メニュー キーが製造元によって異なりますので、これらのキーがよく使用されます。 どのようなブート キーの使用を特定する、システムのマニュアルを確認します。

F12 ESC F9 F10 F8**一般的な BIOS セットアップ キー**

BIOS セットアップ キーが製造元によって異なりますので、これらのキーが使用される一般的です。 どのようなセットアップ キーの使用を特定する、システムのマニュアルを確認します。

ESC DEL F2 **\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\\** *

**Windows を起動する場合**

**\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\\***

-   **セーフ モードで起動して、通常どおりにブートし、**

    セーフ モードで起動するには、次の手順を完了します。 セーフ モードで起動する可能性がありますに再びアクセスできる記憶域システムの記憶装置ドライバーのコア セットを読み込みます。

    セーフ モードを入力するを使用して**更新とセキュリティ**で設定します。 選択**Recovery**-&gt;**スタートアップを高度な**メンテナンス モードで起動します。 結果として得られるメニューでは、次のように選択します**トラブルシューティング**- &gt; **オプションの高度な** - &gt; **スタートアップ設定**。 - &gt; **再起動**します。 Windows を再起動した後、**スタートアップ設定**画面で、セーフ モードで起動するには、4、5 または 6 のオプションを選択します。

    Windows がセーフ モードで読み込まれると、適切なストレージ ドライバーが読み込まれるかどうかと、ストレージ デバイスが認識されていることを確認する PC を再起動します。

    セーフ モードは、ブート、f8 キーなどのファンクション キーを押して、使用可能なあります。 特定のスタートアップ オプションのシステムの製造元から情報を参照してください。

-   ないファイル システムのエラーを確認するのにには、スキャンのディスク ユーティリティを使用します。 スキャンを選択するドライブを右クリックして**プロパティ**します。 をクリックして**ツール**します。 をクリックして、**今すぐチェック**ボタンをクリックします。
-   ウイルス検出プログラムを実行します。 ウイルスに感染する可能性、Windows 用にフォーマットされたハード_ディスクのすべての種類と、結果として得られるディスクの破損は、システムのバグ チェックのコードを生成できます。 ウイルス検出プログラムへの感染マスター ブート レコードのチェックを確認します。

-   IDE デバイスは、のみプライマリとしてオンボード IDE ポートを定義します。 適切な各 IDE デバイスの確認も**マスター/下位/スタンド アロン**設定します。 ハード_ディスクを除くすべての IDE デバイスを削除してください。 最後に、デバイスまたはドライバー エラーの原因を識別するのに役立つその他のエラー メッセージをイベント ビューアーのシステム ログを確認します。

-   ハード ドライブに十分な空き領域があることを確認します。 オペレーティング システムと一部のアプリケーションは、スワップ ファイルを作成する十分な空き領域を必要とし、他の機能です。 システム構成に基づきと、正確な要件は異なりますが、通常は 10 ~ 15% 空き領域があることをお勧めします。

-   検索対象**デバイス マネージャー**を任意のデバイスの感嘆符 (!) が付いてを参照してください。 任意のエラーが発生したドライバーのドライバーのプロパティに表示されるイベント ログを確認します。 関連するドライバーを更新してみてください。

-   デバイスまたはエラーの原因となっているドライバーの特定に役立つ可能性がある追加のエラー メッセージをイベント ビューアーのシステム ログを確認します。 詳細については、次を参照してください。[イベント ビューアーを開く](https://support.microsoft.com/hub/4338813/windows-help#1TC=windows-7)します。 ブルー スクリーンに同じ期間に発生したシステム ログの重大なエラーを探します。

-   システム製造元から提供されたハードウェア診断を実行して確認することができます。

-   システム ファイル チェッカー ツールを使用して、欠落または破損システム ファイルを修復します。 システム ファイル チェッカーは、ユーティリティは Windows ユーザーを Windows システム ファイルで破損をスキャンし、復元できるようにするには、ファイルが破損しています。 システム ファイル チェッカー (SFC.exe) ツールを実行するのにには、次のコマンドを使用します。

    ```console
    SFC /scannow
    ```

    詳細については、次を参照してください。[システム ファイル チェッカー ツールを使用してシステム ファイルの欠落または破損の修復](https://support.microsoft.com/help/929833/use-the-system-file-checker-tool-to-repair-missing-or-corrupted-system)します。

-   [オプション] 画面では、自動修復した後、選択**トラブルシューティング&gt;詳細オプション&gt;システムの復元**します。 このオプションは、PC 戻るを以前の時点で、システムの復元ポイントと呼ばれます。 復元ポイントが新しいアプリ、ドライバー、更新プログラムをインストールするときに、または手動で復元ポイントを作成するときに生成されます。 エラーが発生する前に、復元ポイントを選択します。

-   カーネル デバッガーを使用して、システムに接続し、さらに「解説」の説明に従って、エラーを分析します。

<a name="remarks"></a>コメント
-------

**ストレージ システムの構成の調査**

Windows がインストールされているブート デバイスについてできるだけ多くを把握することをお勧めします。 たとえば、次の項目を調査することができます。

-   ブート デバイスが (SATA、IDE など) に接続されているコント ローラーの種類を確認します。 コント ローラーとディスク ドライバーのプロパティを確認し、関連するドライバーを参照してください。 デバイス マネージャーを使用するにはシステムをブートする場合のエラー イベントとファイル。

-   その他のデバイスがブート デバイスが (SSD、DVD、) にある同じコント ローラーに関連付けられているかどうかを示します。

-   通常の NTFS ドライブで使用されるファイル システムに注意してください。

**カーネル デバッガーを使用してこのエラーを分析します。** 実行、 [ **lm (読み込まれたモジュールの一覧)** ](lm--list-loaded-modules-.md)に特定のドライバーを分離しようとするモジュールがロードされているデバッガー コマンド。 次のドライバーが読み込まれたことを確認します。

*disk*

```dbgcmd
           
0: kd> lm m disk
Browse full module list
start             end                 module name
fffff806`bd0b0000 fffff806`bd0cd000   disk       (deferred)
```

*partmgr*

```dbgcmd
0: kd> lm m partmgr
Browse full module list
start             end                 module name
fffff806`bc5a0000 fffff806`bc5c1000   partmgr    (deferred)
```

*NTFS*

```dbgcmd
0: kd> lm m ntfs
Browse full module list
start             end                 module name
fffff806`bd3f0000 fffff806`bd607000   NTFS       (deferred)
```

*classpnp*

```dbgcmd
 0: kd> lm m classpnp
Browse full module list
start             end                 module name
fffff806`bd0d0000 fffff806`bd131000   CLASSPNP   (deferred)
```

*pci*

```dbgcmd
0: kd> lm m pci
Browse full module list
start             end                 module name
fffff806`bc440000 fffff806`bc494000   pci        (deferred) 
```

また、コント ローラー ドライバーが読み込まれることを確認してください。 たとえば、SATA RAID コント ローラーのこの可能性があります、 *iaStorA.Sys*ドライバー、またはその可能性があります、 *EhStorClass*ドライバー。

```dbgcmd
0: kd> lm m EhStorClass
Browse full module list
start             end                 module name
fffff806`bcbb0000 fffff806`bcbcb000   EhStorClass   (deferred) 
```

Storahci"stor"を含めることが、存在する可能性がドライバーの一覧を表示します。

```dbgcmd
0: kd> lm m stor*
Browse full module list
start             end                 module name
fffff806`bcb00000 fffff806`bcb23000   storahci   (deferred)             
fffff806`bcb30000 fffff806`bcbaa000   storport   (deferred)             
fffff806`c0770000 fffff806`c0788000   storqosflt   (deferred)
```

**アタッチされたデバッガーを起動**

発行する場合は、ターゲット システムを起動するには接続されているデバッガーを使用して、 [ **! devnode 0 1** ](-devnode.md)バグチェックが発生します。 デバイスは、ドライバーがないか、開始できませんでしたが表示され、起動しない理由が明らかな可能性があります。

原因の 1 つでその可能性があり、再生は、ブート デバイスにリソースを割り当てることはできません。 この制限は、サービスのエントリを検索して確認できます。 状態フラグが DNF を含める場合\_不十分\_リソース DNF を含めないでくださいまたは\_STARTED または DNF\_が列挙される場合がありますを見つけた問題。 お試しください **! devnode 0 1 storahci**デバイス全体のツリーのダンプの代わりに、いくつかの時間を節約します。

```dbgcmd
0: kd> !devnode 0 1 storahci
Dumping IopRootDeviceNode (= 0xffffb9053d94d850)
DevNode 0xffffb9053e8dea50 for PDO 0xffffb9053e8da060
  InstancePath is "PCI\VEN_8086&DEV_3B22&SUBSYS_304A103C&REV_05\3&21436425&0&FA"
  ServiceName is "storahci"
  State = DeviceNodeStarted (0x308)
  Previous State = DeviceNodeEnumerateCompletion (0x30d)
  DevNode 0xffffb9053e88db30 for PDO 0xffffb9053e890060
    InstancePath is "SCSI\Disk&Ven_&Prod_ST3500418AS\4&23d99fa2&0&000000"
    ServiceName is "disk"
    State = DeviceNodeStarted (0x308)
    Previous State = DeviceNodeEnumerateCompletion (0x30d)
  DevNode 0xffffb9053e88d850 for PDO 0xffffb9053e88e060
    InstancePath is "SCSI\CdRom&Ven_hp&Prod_DVD-RAM_GH60L\4&23d99fa2&0&010000"
    ServiceName is "cdrom"
    TargetDeviceNotify List - f 0xffffdf0ae9bbb0e0  b 0xffffdf0aea874710
    State = DeviceNodeStarted (0x308)
    Previous State = DeviceNodeEnumerateCompletion (0x30d)
```

 

 




