---
title: ドライバーの検証ツールのコマンド構文
description: コマンドプロンプトウィンドウで検証ユーティリティを実行する場合は、次の構文を使用します。同じ1行に複数のオプションを入力できます。
ms.assetid: 7cdf5277-7187-4e90-b22a-6f828f06e2fb
keywords:
- Driver Verifier コマンド構文ドライバー開発ツール
topic_type:
- apiref
api_name:
- Driver Verifier Command Syntax
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: de0aac9d36bcc563fd999fcb33c95ef347ba0873
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968583"
---
# <a name="driver-verifier-command-syntax"></a>ドライバーの検証ツールのコマンド構文


コマンドプロンプトウィンドウで検証ユーティリティを実行する場合は、次の構文を使用します。

同じ1行に複数のオプションを入力できます。 次に例を示します。

```
verifier /flags 7 /driver beep.sys flpydisk.sys
```

**Windows 10**

**/Volatile**パラメーターは、一部の Driver Verifier **/flags**オプションと、 **/標準**で使用できます。 **/Flags**オプションと共に **/volatile**を使用して、 [DDI 準拠の確認](ddi-compliance-checking.md)、[電源フレームワーク遅延ファジー](concurrency-stress-test.md)化、 [Storport 検証](dv-storport-verification.md)、または[SCSI 検証](scsi-verification.md)を行うことはできません。 詳細については、「 [Volatile 設定の使用](using-volatile-settings.md)」を参照してください。

```
  verifier /standard /all
  verifier /standard /driver NAME [NAME ...]
  verifier /flags <options> /all
  verifier /flags <options> /driver NAME [NAME ...]
  verifier /rules [OPTION ...]
  verifier /query
  verifier /querysettings
  verifier /bootmode [persistent | disableafterfail | oneboot]
  verifier /reset
  verifier /faults [Probability] [PoolTags] [Applications] [DelayMins]
  verifier /faultssystematic [OPTION ...] 
  verifier /log LOG_FILE_NAME [/interval SECONDS]
  verifier /volatile /flags <options>
  verifier /volatile /adddriver NAME [NAME ...]
  verifier /volatile /removedriver NAME [NAME ...]
  verifier /volatile /faults [Probability] [PoolTags] [Applications] [DelayMins]
  verifier /domain <types> <options> /driver ... [/logging | /livedump]
  verifier /logging
  verifier /livedump
  verifier /?
  verifier /help
```

**Windows 8.1**

**/Volatile**パラメーターは、一部の Driver Verifier **/flags**オプションと、 **/標準**で使用できます。 **/Flags**オプションと共に **/volatile**を使用して、 [DDI 準拠の確認](ddi-compliance-checking.md)、[電源フレームワーク遅延ファジー](concurrency-stress-test.md)化、 [Storport 検証](dv-storport-verification.md)、または[SCSI 検証](scsi-verification.md)を行うことはできません。 詳細については、「 [Volatile 設定の使用](using-volatile-settings.md)」を参照してください。

```
  verifier /standard /all
  verifier /standard /driver NAME [NAME ...]
  verifier /flags <options> /all
  verifier /flags <options> /driver NAME [NAME ...]
  verifier /rules [OPTION ...]
  verifier /faults [Probability] [PoolTags] [Applications] [DelayMins]
  verifier /faultssystematic [OPTION ...]  
  verifier /log LOG_FILE_NAME [/interval SECONDS]
  verifier /query
  verifier /querysettings
  verifier /bootmode [persistent | disableafterfail | oneboot]
  verifier /reset
  verifier /volatile /flags <options>
  verifier /volatile /adddriver NAME [NAME ...]
  verifier /volatile /removedriver NAME [NAME ...]
  verifier /volatile /faults [Probability] [PoolTags] [Applications] [DelayMins]
  verifier /?
```

**Windows 8、Windows 7、Windows Vista 構文**

**/Volatile**パラメーターは、一部の Driver Verifier **/flags**オプションと、 **/標準**で使用できます。 **/Volatile**は、 [DDI 準拠の確認](ddi-compliance-checking.md)、[電源フレームワーク遅延ファジー](concurrency-stress-test.md)、 [Storport 検証](dv-storport-verification.md)、 [SCSI 検証](scsi-verification.md)、または **/ディスク**に対する/flags オプションと共に使用することはできません。 詳細については、「 [Volatile 設定の使用](using-volatile-settings.md)」を参照してください。

```
verifier [/volatile] [/standard | /flags Options ] [ /all | /driver DriverList ]
verifier /volatile /faults [Probability PoolTags Applications DelayMins] /driver DriverList
verifier /volatile {/adddriver | /removedriver} DriverList
verifier /reset 
verifier /querysettings 
verifier /query 
verifier /log LogFileName [/interval Seconds] 
verifier /? 
```

**Windows Server 2003 の構文**

```
verifier [/disk] [ /standard | /flags Options ] [ /all | /driver DriverList ] 
verifier /volatile /flags VolatileOptions 
verifier /volatile {/adddriver | /removedriver} DriverList
verifier /reset 
verifier /querysettings 
verifier /query 
verifier /log LogFileName [/interval Seconds] 
verifier /? 
```

## <a name="span-idddk_verifier_command_line_toolsspanspan-idddk_verifier_command_line_toolsspanparameters"></a><span id="ddk_verifier_command_line_tools"></span><span id="DDK_VERIFIER_COMMAND_LINE_TOOLS"></span>パラメータ


### <a name="span-idverifier_command_line_syntaxspanspan-idverifier_command_line_syntaxspanverifier-command-line-syntax"></a><span id="verifier_command_line_syntax"></span><span id="VERIFIER_COMMAND_LINE_SYNTAX"></span>検証ツールのコマンドライン構文

<span id="________all______"></span><span id="________ALL______"></span>**/all**   
次回の起動時にインストールされたすべてのドライバーを検証するようにドライバーの検証ツールに指示します。

<span id="________bootmode_mode______"></span><span id="________BOOTMODE_MODE______"></span>**/bootmode** *モード*   
再起動後にドライバーの検証機能の設定を有効にするかどうかを制御します。 このオプションを設定または変更するには、コンピューターを再起動する必要があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ブート<em>モード</em></th>
<th align="left">[説明]</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="persistent"></span><span id="PERSISTENT"></span><strong>一貫</strong></p></td>
<td align="left"><p>多くの再起動に対して、ドライバーの検証ツールの設定が保持される (有効になっている) ことを保証します。 これは、既定の設定です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="disableafterfail"></span><span id="DISABLEAFTERFAIL"></span><strong>disableafterfail</strong></p></td>
<td align="left"><p>Windows の起動に失敗した場合、この設定により、以降の再起動でドライバーの検証ツールが無効になります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="oneboot"></span><span id="ONEBOOT"></span><strong>oneboot</strong></p></td>
<td align="left"><p>では、次回コンピューターを起動するときにのみ、ドライバーの検証ツールの設定が有効になります。 後続の再起動では、ドライバーの検証ツールは無効になっています。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="resetonunusualshutdown"></span><span id="RESETONUNUSUALSHUTDOWN"></span><strong>resetonunusualshutdown</strong></p></td>
<td align="left"><p>(Windows 10、ビルド1709で導入)ドライバーの検証ツールは、異常なシャットダウンが発生するまで保持されます。 Abbrevation <strong>' rous '</strong>を使用できます。
</p></td>
</tr>
</tbody>
</table>



<span id="________disk______"></span><span id="________DISK______"></span>**/ディスク**   
(Windows Server 2003 で導入されました。 Windows 7 以降のバージョンの Windows では使用できません。)次回の起動時に、[ディスクの整合性チェック](disk-integrity-checking.md)オプションをアクティブにします。 どのバージョンの Windows でも、 **/volatile**で **/ディスク**を使用することはできません。

<span id="________driver________DriverList______"></span><span id="________driver________driverlist______"></span><span id="________DRIVER________DRIVERLIST______"></span>**/Driver** *driverlist*   
検証される1つ以上のドライバーを指定します。 *Driverlist*は、Driver.sys など、バイナリ名別のドライバーの一覧です。 各ドライバー名を区切るにはスペースを使用します。 N .sys などのワイルドカード値はサポートされて \* いません。

<span id="________driver.exclude________driverlist______"></span><span id="________DRIVER.EXCLUDE________DRIVERLIST______"></span>**/ドライバーの除外** *driverlist*   
検証から除外する1つ以上のドライバーを指定します。 このパラメーターは、すべてのドライバーが検証対象として選択されている場合にのみ適用されます。 *Driverlist*は、Driver.sys など、バイナリ名別のドライバーの一覧です。 各ドライバー名を区切るにはスペースを使用します。 N .sys などのワイルドカード値はサポートされて \* いません。

<span id="________faults______"></span><span id="________FAULTS______"></span>**/障害**   
(Windows Vista 以降)ドライバー検証ツールの低リソースシミュレーション機能を有効にします。 **/Flags 0x4**の代わりに **/障害**を使用できます。 ただし、 **/flags 0x4**を **/fault**サブパラメーターと共に使用することはできません。

**/障害**パラメーターの次のサブパラメーターを使用して、低リソースシミュレーションを構成できます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">サブパラメーター</th>
<th align="left">[説明]</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><em>確率</em></p></td>
<td align="left"><p>ドライバーの検証ツールが特定の割り当てに失敗する確率を指定します。 1万での確率を表す数値 (10 進数または16進数) を入力します。この値を指定すると、ドライバー検証ツールが割り当てに失敗します。 既定値は600で、600/10000 または6% を意味します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>プールタグ</em></p></td>
<td align="left"><p>指定されたプールタグを使用して、ドライバーの検証で失敗する可能性がある割り当てを制限します。 ワイルドカード文字 () を使用して、複数のプールタグを表すことができ <strong>*</strong> ます。 複数のプールタグを一覧表示するには、タグをスペースで区切ります。 既定では、すべての割り当てが失敗する可能性があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>アプリケーション</em></p></td>
<td align="left"><p>指定したプログラムのドライバーの割り当てに失敗する可能性がある割り当てを制限します。 実行可能ファイルの名前を入力します。 プログラムを一覧表示するには、プログラム名をスペースで区切ります。 既定では、すべての割り当てが失敗する可能性があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>DelayMins</em></p></td>
<td align="left"><p>ドライバー検証ツールが意図的に割り当てを失敗させない、起動後の時間 (分単位) を指定します。 この遅延により、ドライバーが読み込まれ、テストが開始される前にシステムが安定化されます。 数値 (10 進数または16進数) を入力します。 既定値は 7 (分) です。</p></td>
</tr>
</tbody>
</table>



<span id="_faultssystematic"></span><span id="_FAULTSSYSTEMATIC"></span>**/faultssystematic**  
[体系的な低リソースシミュレーション](systematic-low-resource-simulation.md)のオプションを指定します。 **0x40000**フラグを使用して、系統的な低リソースシミュレーションオプションを選択します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">OPTION</th>
<th align="left">[説明]</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>enableboottime</p></td>
<td align="left"><p>コンピューターを再起動する間、フォールトインジェクションを有効にします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>disableboottime</p></td>
<td align="left"><p>コンピューターの再起動によるエラーの挿入を無効にします (これは既定の設定です)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>recordboottime</p></td>
<td align="left"><p>コンピューターが再起動するときに、<em>どのような場合</em>にエラーが挿入されるかを有効にします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>resetboottime</p></td>
<td align="left"><p>コンピューターの再起動によるエラー挿入を無効にし、スタック除外リストをクリアします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>enableruntime</p></td>
<td align="left"><p>フォールトインジェクションを動的に有効にします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>disableruntime</p></td>
<td align="left"><p>フォールトインジェクションを動的に無効にします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>recordruntime</p></td>
<td align="left"><p><em>What-if</em>モードでのフォールトインジェクションを動的に有効にします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>resetruntime</p></td>
<td align="left"><p>フォールトインジェクションを動的に無効にし、以前にエラーが発生したスタックリストをクリアします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>querystatistics</p></td>
<td align="left"><p>現在のフォールトインジェクションの統計情報を表示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>incrementcounter</p></td>
<td align="left"><p>エラーが挿入されたことを識別するために使用されるテストパスカウンターをインクリメントします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>getstackid<em>カウンター</em></p></td>
<td align="left"><p>指定された挿入スタック識別子を取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>excludestack <em>STACKID</em></p></td>
<td align="left"><p>フォールト挿入からスタックを除外します。</p></td>
</tr>
</tbody>
</table>



<span id="________flags________Options______"></span><span id="________flags________options______"></span><span id="________FLAGS________OPTIONS______"></span>**/Flags** *オプション*   
次回の再起動後に、指定したオプションをアクティブにします。 Windows 2000 では、この数値は10進数形式で入力する必要があります。 Windows XP 以降では、この数値は10進数で入力することも、16進形式 ( **0x**プレフィックス) で入力することもできます。 次の値の任意の組み合わせを使用できます。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Decimal (10 進数型)</th>
<th align="left">16 進数</th>
<th align="left">標準設定</th>
<th align="left">オプション</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>0x1 (ビット 0)</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p><a href="special-pool.md" data-raw-source="[Special Pool](special-pool.md)">Special Pool</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>0x2 (ビット 1)</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p><a href="force-irql-checking.md" data-raw-source="[Force IRQL Checking](force-irql-checking.md)">強制 IRQL チェック</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>4</p></td>
<td align="left"><p>0x4 (ビット 2)</p></td>
<td align="left"></td>
<td align="left"><p><a href="low-resources-simulation.md" data-raw-source="[Low Resources Simulation](low-resources-simulation.md)">低リソースシミュレーション</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>8</p></td>
<td align="left"><p>0x8 (ビット 3)</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p><a href="pool-tracking.md" data-raw-source="[Pool Tracking](pool-tracking.md)">プールの追跡</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>16</p></td>
<td align="left"><p>0x10 (ビット 4)</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p><a href="i-o-verification.md" data-raw-source="[I/O Verification](i-o-verification.md)">I/o の検証</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>32</p></td>
<td align="left"><p>0x20 (ビット 5)</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p><a href="deadlock-detection.md" data-raw-source="[Deadlock Detection](deadlock-detection.md)">デッドロック検出</a>(Windows XP 以降)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>64</p></td>
<td align="left"><p>0x40 (ビット 6)</p></td>
<td align="left"></td>
<td align="left"><p>強化された<a href="enhanced-i-o-verification.md" data-raw-source="[Enhanced I/O Verification](enhanced-i-o-verification.md)">I/o 検証</a>(windows XP 以降) (windows 7 以降では、i/o 検証を選択すると、このオプションは自動的にアクティブになります)</p></td>
</tr>
<tr class="even">
<td align="left"><p>128</p></td>
<td align="left"><p>0x80 (ビット 7)</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p><a href="dma-verification.md" data-raw-source="[DMA Verification](dma-verification.md)">DMA の検証</a>(Windows XP 以降)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>256</p></td>
<td align="left"><p>0x100 (ビット 8)</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p><a href="security-checks.md" data-raw-source="[Security Checks](security-checks.md)">セキュリティチェック</a>(Windows XP 以降)</p></td>
</tr>
<tr class="even">
<td align="left"><p>512</p></td>
<td align="left"><p>0x200 (ビット 9)</p></td>
<td align="left"></td>
<td align="left"><p><a href="force-pending-i-o-requests.md" data-raw-source="[Force Pending I/O Requests](force-pending-i-o-requests.md)">強制的に保留中の I/o 要求</a>を実行する (Windows Vista 以降)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>1024</p></td>
<td align="left"><p>0x400 (ビット 10)</p></td>
<td align="left"></td>
<td align="left"><p><a href="irp-logging.md" data-raw-source="[IRP Logging](irp-logging.md)">IRP ログ記録</a>(Windows Server 2003 以降)</p></td>
</tr>
<tr class="even">
<td align="left"><p>2048</p></td>
<td align="left"><p>0x800 (ビット 11)</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p><a href="miscellaneous-checks.md" data-raw-source="[Miscellaneous Checks](miscellaneous-checks.md)">その他のチェック</a>(Windows Vista 以降)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>8192</p></td>
<td align="left"><p>0x2000 (ビット 13)</p></td>
<td align="left"></td>
<td align="left"><p><a href="invariant-mdl-checking-for-stack.md" data-raw-source="[Invariant MDL Checking for Stack](invariant-mdl-checking-for-stack.md)">インバリアントな MDL のスタックチェック</a>(Windows 8 以降)</p></td>
</tr>
<tr class="even">
<td align="left"><p>16384</p></td>
<td align="left"><p>0x4000 (ビット 14)</p></td>
<td align="left"></td>
<td align="left"><p><a href="invariant-mdl-checking-for-driver.md" data-raw-source="[Invariant MDL Checking for Driver](invariant-mdl-checking-for-driver.md)">ドライバーの不変の MDL チェック</a>(Windows 8 以降)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>32768</p></td>
<td align="left"><p>0x8000 (ビット 15)</p></td>
<td align="left"></td>
<td align="left"><p><a href="concurrency-stress-test.md" data-raw-source="[Power Framework Delay Fuzzing](concurrency-stress-test.md)">Power Framework 遅延ファジー</a> (Windows 8 以降)</p></td>
</tr>
<tr class="even">
<td align="left"><p>65536</p></td>
<td align="left"><p>全月 (ビット 16)</p></td>
<td align="left"></td>
<td align="left"><p>ポート/ミニポートインターフェイスの確認 (Windows 10 以降)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>131072</p></td>
<td align="left"><p>0x20000 (ビット 17)</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p><a href="ddi-compliance-checking.md" data-raw-source="[DDI compliance checking](ddi-compliance-checking.md)">DDI 準拠の確認</a>(Windows 8 以降)</p></td>
</tr>
<tr class="even">
<td align="left"><p>262144</p></td>
<td align="left"><p>0x40000 (bit 18)</p></td>
<td align="left"></td>
<td align="left"><p><a href="systematic-low-resource-simulation.md" data-raw-source="[Systematic low resources simulation](systematic-low-resource-simulation.md)">体系的な低リソースシミュレーション</a>(Windows 8.1 から開始)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>524288</p></td>
<td align="left"><p>0x80000 (ビット 19)</p></td>
<td align="left"></td>
<td align="left"><p><a href="ddi-compliance-checking.md#ddi_compliance_checking_additional" data-raw-source="[DDI compliance checking (additional)](ddi-compliance-checking.md#ddi_compliance_checking_additional)">DDI 準拠の確認 (追加)</a> (Windows 8.1 から開始)</p></td>
</tr>
<tr class="even">
<td align="left"><p>2097152</p></td>
<td align="left"><p>0x200000 (ビット 21)</p></td>
<td align="left"></td>
<td align="left"><p><a href="ndis-wifi-verification.md" data-raw-source="[NDIS/WIFI verification](ndis-wifi-verification.md)">NDIS/WIFI 検証</a>(Windows 8.1 以降)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>8388608</p></td>
<td align="left"><p>0x800000 (ビット 23)</p></td>
<td align="left"></td>
<td align="left"><p><a href="kernel-synchronization-delay-fuzzing.md" data-raw-source="[Kernel synchronization delay fuzzing](kernel-synchronization-delay-fuzzing.md)">カーネル同期遅延ファジー</a> (Windows 8.1 から開始)</p></td>
</tr>
<tr class="even">
<td align="left"><p>16777216</p></td>
<td align="left"><p>0x1000000 (ビット 24)</p></td>
<td align="left"></td>
<td align="left"><p><a href="vm-switch-verification.md" data-raw-source="[VM switch verification](vm-switch-verification.md)">VM スイッチの検証</a>(Windows 8.1 から開始)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>33554432</p></td>
<td align="left"><p>0x2000000 (ビット 25)</p></td>
<td align="left"></td>
<td align="left"><p>コードの整合性チェック (Windows 10 以降)</p></td>
</tr>
</tbody>
</table>



この方法を使用して、SCSI 検証オプションまたは Storport 検証オプションをアクティブ化することはできません。 詳細については、「 [SCSI 検証](scsi-verification.md)と[Storport 検証](dv-storport-verification.md)」を参照してください。

<span id="________flags________VolatileOptions______"></span><span id="________flags________volatileoptions______"></span><span id="________FLAGS________VOLATILEOPTIONS______"></span>**/Flags** *VolatileOptions*   
Windows 2000、Windows XP、および Windows Server 2003 で再起動せずに、直ちに変更されるドライバーの検証ツールオプションを指定します。 (Windows Vista では、 **/volatile**パラメーターをすべての **/flags**値と共に使用できます)。

Windows 2000 では、10進数形式で数値を入力します。 Windows XP および Windows 2003 では、10進数または16進数形式 ( **0x**プレフィックス) で数値を入力します。

次の値の任意の組み合わせが許可されます。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Decimal (10 進数型)</th>
<th align="left">16 進数</th>
<th align="left">オプション</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>0x1 (ビット 0)</p></td>
<td align="left"><p>Special Pool</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>0x2 (ビット 1)</p></td>
<td align="left"><p>強制 IRQL 検査</p></td>
</tr>
<tr class="odd">
<td align="left"><p>4</p></td>
<td align="left"><p>0x4 (ビット 2)</p></td>
<td align="left"><p>低リソースのシミュレーション</p></td>
</tr>
</tbody>
</table>



<span id="________iolevel________Level______"></span><span id="________iolevel________level______"></span><span id="________IOLEVEL________LEVEL______"></span>**/Iolevel** *レベル*   
(Windows 2000 のみ)[I/o 検証](i-o-verification.md)のレベルを指定します。

*Level*の値には、 **1**または**2**を指定できます。 既定値は **1**です。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">レベルの値</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>1</strong></p></td>
<td align="left"><p>レベル 1 i/o 検証を有効にします (既定)。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>2</strong></p></td>
<td align="left"><p>レベル 1 i/o 検証とレベル 2 i/o 検証を有効にします。</p></td>
</tr>
</tbody>
</table>



**/Flags 0x10**を使用して I/o の検証が有効になっていない場合、 **/iolevel**は無視されます。

<span id="________log________LogFileName_______interval_Seconds_______"></span><span id="________log________logfilename_______interval_seconds_______"></span><span id="________LOG________LOGFILENAME_______INTERVAL_SECONDS_______"></span>**/log** *LogFileName* \[ **/interval** | *Seconds*\]   
*LogFileName*という名前のログファイルを作成します。 ドライバーの検証ツールは、このファイルに統計を定期的に書き込みます。 詳細については、「[ログファイルの作成](creating-log-files.md)」を参照してください。

コマンドラインで**検証ツール/log**コマンドを入力しても、コマンドプロンプトからは返されません。 ログファイルを閉じてプロンプトを返すには、CTRL + C キーを使用します。 再起動後にログを作成するには、もう一度**ベリファイア/log**コマンドを送信する必要があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">オプション</th>
<th align="left">[説明]</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="________interval________Seconds______"></span><span id="________interval________seconds______"></span><span id="________INTERVAL________SECONDS______"></span><strong>/Interval</strong> <em>秒</em></p></td>
<td align="left"><p>ログファイルの更新間隔を指定します。 既定値は 30 秒です。</p></td>
</tr>
</tbody>
</table>



<span id="_rules_Option"></span><span id="_rules_option"></span><span id="_RULES_OPTION"></span>**/ルール***オプション*  
無効にできるルールのオプション ([詳細設定])。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">オプション</th>
<th align="left">[説明]</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>query</strong></p></td>
<td align="left"><p>制御可能なルールの現在の状態を表示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>reset</strong></p></td>
<td align="left"><p>すべてのルールを既定の状態にリセットします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>既定</strong>の<em>ID</em></p></td>
<td align="left"><p>ルール<em>ID</em>を既定の状態に設定します。 サポートされているルールの場合、ルール<em>ID</em>は、<a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation" data-raw-source="[&lt;strong&gt;Bug Check 0xC4&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)"><strong>バグチェック 0xc4</strong></a> (DRIVER_VERIFIER_DETECTED_VIOLATION) パラメーター1の値です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>disable</strong> <em>ID</em>の無効化</p></td>
<td align="left"><p>指定された規則<em>ID</em>を無効にします。 サポートされているルールの場合、ルール<em>ID</em>は、<a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation" data-raw-source="[&lt;strong&gt;Bug Check 0xC4&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)"><strong>バグチェック 0xc4</strong></a> (DRIVER_VERIFIER_DETECTED_VIOLATION) パラメーター1の値です。</p></td>
</tr>
</tbody>
</table>



<span id="________standard"></span><span id="________STANDARD"></span>**/標準**  
(Windows XP 以降)次回の起動時に、"standard" または既定のドライバー検証ツールオプションをアクティブにします。 Windows XP の標準オプションは、[特別なプール](special-pool.md)、[強制 IRQL チェック](force-irql-checking.md)、[プールの追跡](pool-tracking.md)、 [i/o 検証](i-o-verification.md)、[デッドロック検出](deadlock-detection.md)、および[DMA 検証](dma-verification.md)です。 これは、 **/Flags 0xBB**と同じです。 Windows Vista 以降、標準オプションには、[セキュリティチェック](security-checks.md)と[その他のチェック](miscellaneous-checks.md)も含まれています。 これは、 **/Flags 0x9BB**と同じです。 Windows 8 以降、標準オプションには、 [DDI 準拠の確認](ddi-compliance-checking.md)も含まれています。 これは、 **/Flags 0x209BB**と同じです。

> [!NOTE]
> 1803より後のバージョンの Windows 10 以降では、 **/Flags 0x209BB**を使用すると、WDF 検証が自動的に有効になりなくなります。 標準のオプションを有効にするには **、標準の構文を**使用します。 WDF の検証が含まれています。 詳細については、「 [Driver Verifier コマンド構文](https://docs.microsoft.com/windows-hardware/drivers/devtest/verifier-command-line)」を参照してください。

<span id="________volatile______"></span><span id="________VOLATILE______"></span>**/volatile**   
コンピューターを再起動せずに設定を変更します。 揮発性の設定は直ちに有効になります。

Windows Vista 以降のバージョンの Windows では、 **/volatile**パラメーターと **/flags**パラメーターを使用して、再起動せずに一部のオプションを有効または無効にすることができます。 また、ドライバーの検証ツールがまだ実行されていない場合でも、 **/adddriver**パラメーターと **/removedriver**パラメーターを指定して **/volatile**を使用して、再起動せずにドライバーの検証を開始または停止することもできます。

Windows Vista より前のバージョンの Windows では、 **/volatile**パラメーターは*VolatileOptions*に記載されているオプションと共にのみ使用できます。また、ドライバー検証ツールが既に実行されていて、コンピューターが再起動された場合にのみ、再起動せずにドライバーの検証を開始または停止するために使用できます。

詳細については、「 [Volatile 設定の使用](using-volatile-settings.md)」を参照してください。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">オプション</th>
<th align="left">[説明]</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="__adddriver_VolatileDriverList"></span><span id="__adddriver_volatiledriverlist"></span><span id="__ADDDRIVER_VOLATILEDRIVERLIST"></span><strong>/Adddriver</strong> <em>VolatileDriverList</em></p></td>
<td align="left"><p>(Windows XP 以降)指定されたドライバーを揮発性の設定に追加します。 複数のドライバーを指定するには、名前をスペースで区切って指定します。 N .sys などのワイルドカード値はサポートされて <em> いません。 詳細については、「 <a href="using-volatile-settings.md" data-raw-source="[Using Volatile Settings](using-volatile-settings.md)">Volatile 設定の使用」を</a>参照してください。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="_removedriver_VolatileDriverList"></span><span id="_removedriver_volatiledriverlist"></span><span id="_REMOVEDRIVER_VOLATILEDRIVERLIST"></span><strong>/Removedriver</strong> <em>VolatileDriverList</em></p></td>
<td align="left"><p>(Windows XP 以降)指定されたドライバーを揮発性の設定から削除します。 複数のドライバーを指定するには、名前をスペースで区切って指定します。 N .sys などのワイルドカード値はサポートされて </em> いません。 詳細については、「 <a href="using-volatile-settings.md" data-raw-source="[Using Volatile Settings](using-volatile-settings.md)">Volatile 設定の使用」を</a>参照してください。</p></td>
</tr>
</tbody>
</table>



<span></span>  

<span id="________reset______"></span><span id="________RESET______"></span>**/リセット**   
すべてのドライバー検証機能の設定をクリアします。 次回の起動時に、ドライバーは検証されません。

<span id="________querysettings______"></span><span id="________QUERYSETTINGS______"></span>**/querysettings**   
(Windows XP 以降)アクティブ化されるオプションの概要と、次回の起動時に検証されるドライバーが表示されます。 表示には、 **/volatile**パラメーターを使用して追加されたドライバーとオプションは含まれません。 これらの設定を表示する他の方法については、「[ドライバーの検証の設定](viewing-driver-verifier-settings.md)を表示する」を参照してください。

<span id="________query______"></span><span id="________QUERY______"></span>**/query**   
ドライバー検証ツールの現在の利用状況の概要が表示されます。 表示の**Level**フィールドは、 **/volatile**パラメーターで設定されたオプションの16進数の値です。 各統計の説明については、「[グローバルカウンターの監視](monitoring-global-counters.md)と[個々のカウンターの監視](monitoring-individual-counters.md)」を参照してください。

<span id="________domain_Types_Options_______"></span><span id="________domain_types_options_______"></span><span id="________DOMAIN_TYPES_OPTIONS_______"></span>**/domain**の*種類*の  ****  *オプション*   
検証ツールの拡張機能の設定を制御します。 次の種類の検証拡張機能がサポートされています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><em>型</em></th>
<th align="left">[説明]</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="wdm"></span><span id="WDM"></span><strong>wdm</strong></p></td>
<td align="left"><p>WDM ドライバーの検証拡張機能を有効にします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="ndis"></span><span id="NDIS"></span><strong>ndis</strong></p></td>
<td align="left"><p>ネットワークドライバーの検証ツール拡張を有効にします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="ks"></span><span id="KS"></span><strong>ks</strong></p></td>
<td align="left"><p>カーネルモードストリーミングドライバーの検証拡張機能を有効にします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="audio"></span><span id="AUDIO"></span><strong>音源</strong></p></td>
<td align="left"><p>オーディオドライバーの検証拡張機能を有効にします。</p></td>
</tr>
</tbody>
</table>



次の拡張オプションがサポートされています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><em>[オプション]</em></th>
<th align="left">[説明]</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="rules.default"></span><span id="RULES.DEFAULT"></span><strong>rules. 既定</strong></p></td>
<td align="left"><p>選択された検証拡張機能の既定の検証規則を有効にします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="rules.all"></span><span id="RULES.ALL"></span><strong>rules. all</strong></p></td>
<td align="left"><p>選択した検証機能拡張のすべての検証規則を有効にします。</p></td>
</tr>
</tbody>
</table>

<span id="________logging_______"></span><span id="________LOGGING_______"></span>**/ログ**   
選択した検証機能拡張によって検出された、違反したルールのログ記録を有効にします。

<span id="________livedump_______"></span><span id="________LIVEDUMP_______"></span>**/livedump**   
選択した検証機能拡張によって検出された規則に違反した場合に、ライブメモリダンプの収集を有効にします。

<span id="_______________"></span> **/?**   
コマンドラインのヘルプを表示します。

これらのコマンドの使用方法の詳細については、「[ドライバー検証](controlling-driver-verifier.md)機能の制御」および「[ドライバー検証ツールの監視](monitoring-driver-verifier.md)」を参照してください。

<span id="________help______"></span><span id="________HELP______"></span>**/help**   
コマンドラインのヘルプを表示します。

これらのコマンドの使用方法の詳細については、「[ドライバー検証](controlling-driver-verifier.md)機能の制御」および「[ドライバー検証ツールの監視](monitoring-driver-verifier.md)」を参照してください。

## <a name="span-idreturn_codesspanspan-idreturn_codesspanspan-idreturn_codesspanreturn-codes"></a><span id="Return_Codes"></span><span id="return_codes"></span><span id="RETURN_CODES"></span>リターンコード


ドライバーの検証ツールを実行した後に返される値は次のとおりです。

**0**: 終了 \_ コードの \_ 成功

**1**: コードの終了 \_ \_ エラー

**2**: 終了 \_ コードの \_ 再起動が \_ 必要です












