---
title: ドライバーの検証ツールのコマンド構文
description: 次の構文は、コマンド プロンプト ウィンドウで検証ユーティリティを実行しているときに使用されます。同じ 1 つの行にいくつかのオプションを入力することができます。
ms.assetid: 7cdf5277-7187-4e90-b22a-6f828f06e2fb
keywords:
- Driver Verifier のコマンド構文ドライバー開発ツール
topic_type:
- apiref
api_name:
- Driver Verifier Command Syntax
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 463b13e77e3ed54609b1c733f9b18593c28d93c7
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350371"
---
# <a name="driver-verifier-command-syntax"></a>ドライバーの検証ツールのコマンド構文


次の構文は、コマンド プロンプト ウィンドウで検証ユーティリティを実行しているときに使用されます。

同じ 1 つの行にいくつかのオプションを入力することができます。 例:

```
verifier /flags 7 /driver beep.sys flpydisk.sys
```

**Windows 10**

使用することができます、 **/volatile**パラメーターをいくつかの Driver Verifier **/flags**オプションを使用して**標準/**。 使用することはできません **/volatile**で、 **/flags**オプション[DDI 準拠の検査](ddi-compliance-checking.md)、 [Power Framework 遅延ファジー テスト](concurrency-stress-test.md)、 [Storport 検証](dv-storport-verification.md)、または[SCSI 検証](scsi-verification.md)です。 詳細については、次を参照してください。[揮発性の設定を使用する](using-volatile-settings.md)します。

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

使用することができます、 **/volatile**パラメーターをいくつかの Driver Verifier **/flags**オプションを使用して**標準/**。 使用することはできません **/volatile**で、 **/flags**オプション[DDI 準拠の検査](ddi-compliance-checking.md)、 [Power Framework 遅延ファジー テスト](concurrency-stress-test.md)、 [Storport 検証](dv-storport-verification.md)、または[SCSI 検証](scsi-verification.md)です。 詳細については、次を参照してください。[揮発性の設定を使用する](using-volatile-settings.md)します。

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

**Windows 8、Windows 7、Windows Vista の構文**

使用することができます、 **/volatile**パラメーターをいくつかの Driver Verifier **/flags**オプションを使用して**標準/**。 使用することはできません **/volatile** 、/flags オプションを付けて[DDI 準拠の検査](ddi-compliance-checking.md)、 [Power Framework 遅延ファジー テスト](concurrency-stress-test.md)、 [Storport 検証](dv-storport-verification.md)、 [SCSI 検証](scsi-verification.md)または **/ディスク**します。 詳細については、次を参照してください。[揮発性の設定を使用する](using-volatile-settings.md)します。

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

## <a name="span-idddkverifiercommandlinetoolsspanspan-idddkverifiercommandlinetoolsspanparameters"></a><span id="ddk_verifier_command_line_tools"></span><span id="DDK_VERIFIER_COMMAND_LINE_TOOLS"></span>パラメーター


### <a name="span-idverifiercommandlinesyntaxspanspan-idverifiercommandlinesyntaxspanverifier-command-line-syntax"></a><span id="verifier_command_line_syntax"></span><span id="VERIFIER_COMMAND_LINE_SYNTAX"></span>コマンドライン構文の検証方法

<span id="________all______"></span><span id="________ALL______"></span> **/all**   
[次へ] の起動後にインストールされているすべてのドライバーを確認する Driver Verifier に指示します。

<span id="________bootmode_mode______"></span><span id="________BOOTMODE_MODE______"></span> **/bootmode** *mode*   
Driver Verifier の設定は、再起動後に有効になっているかどうかを制御します。 を設定またはこのオプションを変更するのには、コンピューターを再起動する必要があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ブート<em>モード</em></th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="persistent"></span><span id="PERSISTENT"></span><strong>永続的です</strong></p></td>
<td align="left"><p>Driver Verifier の設定が何回も再起動経由で (影響の維持) を保持するようにします。 これが既定の設定です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="disableafterfail"></span><span id="DISABLEAFTERFAIL"></span><strong>disableafterfail</strong></p></td>
<td align="left"><p>Windows では、開始に失敗した場合、この設定には以降の再起動の Driver Verifier が無効にします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="oneboot"></span><span id="ONEBOOT"></span><strong>oneboot</strong></p></td>
<td align="left"><p>のみ、ドライバーの検証の設定を次回コンピューターを起動できます。 Driver Verifier は、その後再起動に対して無効です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="resetonunusualshutdown"></span><span id="RESETONUNUSUALSHUTDOWN"></span><strong>resetonunusualshutdown</strong></p></td>
<td align="left"><p>(Windows 10 1709 ビルドで導入されました)Driver Verifier は、異常なシャット ダウンが発生するまで保持されます。 その略称、 <strong>'rous'</strong>、使用することができます。
</p></td>
</tr>
</tbody>
</table>



<span id="________disk______"></span><span id="________DISK______"></span> **/disk**   
(Windows Server 2003 で導入されました。 不可能では、Windows 7 および Windows の以降のバージョン)。アクティブ化、[ディスクの整合性チェック](disk-integrity-checking.md)オプション、[次へ] の起動後にします。 使用することはできません **/ディスク**で **/volatile** Windows のバージョンにします。

<span id="________driver________DriverList______"></span><span id="________driver________driverlist______"></span><span id="________DRIVER________DRIVERLIST______"></span> **/driver** *DriverList*   
検証が 1 つまたは複数のドライバーを指定します。 *DriverList*ルートなどのバイナリの名前でドライバーの一覧を示します。 スペースを使用して、各ドライバーの名前を区切ります。 N などのワイルドカード値\*.sys はサポートされていません。

<span id="________driver.exclude________driverlist______"></span><span id="________DRIVER.EXCLUDE________DRIVERLIST______"></span> **/driver.exclude** *DriverList*   
検証から除外する 1 つまたは複数のドライバーを指定します。 このパラメーターは、検証のためのすべてのドライバーが選択されている場合にのみ適用されます。 *DriverList*ルートなどのバイナリの名前でドライバーの一覧を示します。 スペースを使用して、各ドライバーの名前を区切ります。 N などのワイルドカード値\*.sys はサポートされていません。

<span id="________faults______"></span><span id="________FAULTS______"></span> **/faults**   
(Windows Vista 以降)Driver Verifier の低リソース シミュレーション機能を有効にします。 使用することができます**フォールト/** の代わりに **/flags 0x4**します。 ただし、使用することはできません **/flags 0x4**で、 **フォールト/** サブパラ メーターです。

次のサブパラ メーターを使用することができます、 **フォールト/** 低リソース シミュレーションを構成するパラメーター。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">サブパラメータ</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><em>確率</em></p></td>
<td align="left"><p>Driver Verifier の特定の割り当てが失敗する確率を指定します。 (10 進数または 16 進数) で 10,000 件の Driver Verifier の割り当てが失敗する可能性の数を表す数値を入力します。 既定値は 600 では、600/10000 または 6% を意味します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>プール タグ</em></p></td>
<td align="left"><p>Driver Verifier を指定したプール タグの割り当てに失敗できる割り当てを制限します。 ワイルドカード文字を使用することができます (<strong>*</strong>) を複数のプール タグを表します。 複数のプール タグを一覧表示するには、空白で、タグを区切ります。 既定では、すべての割り当てが失敗することができます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>アプリケーション</em></p></td>
<td align="left"><p>Driver Verifier は、指定したプログラムの割り当てに失敗できる割り当てを制限します。 実行可能ファイルの名前を入力します。 プログラムの一覧を表示するには、プログラムを区切るスペースを含む名前を付けます。 既定では、すべての割り当てが失敗することができます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>DelayMins</em></p></td>
<td align="left"><p>起動後の分の間 Driver Verifier が意図的に失敗しない割り当て数を指定します。 この遅延により、ドライバーがロードされ、システム テストの前に安定化が開始されます。 (10 進数または 16 進数) 内の数値を入力します。 既定値は、7 (分です)。</p></td>
</tr>
</tbody>
</table>



<span id="_faultssystematic"></span><span id="_FAULTSSYSTEMATIC"></span>**/faultssystematic**  
オプションを指定します[体系的な低リソース シミュレーション](systematic-low-resource-simulation.md)します。 使用して、 **0x40000** Systematic を選択するフラグの低リソース シミュレーション オプション。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">オプション</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>enableboottime</p></td>
<td align="left"><p>有効では、コンピューターの再起動後にインジェクションをフォールトします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>disableboottime</p></td>
<td align="left"><p>無効にします (これは既定の設定) コンピューターの再起動後にインジェクションを障害。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>recordboottime</p></td>
<td align="left"><p>によりフォールト インジェクションで<em>what-if</em>モードにコンピューターを再起動します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>resetboottime</p></td>
<td align="left"><p>コンピューターの再起動後に、フォールト インジェクションを無効にし、スタックの除外リストをクリアします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>enableruntime</p></td>
<td align="left"><p>フォールト インジェクションを動的に有効です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>disableruntime</p></td>
<td align="left"><p>フォールト インジェクションを動的に無効にします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>recordruntime</p></td>
<td align="left"><p>動的に有効の障害でインジェクション<em>what-if</em>モード。</p></td>
</tr>
<tr class="even">
<td align="left"><p>resetruntime</p></td>
<td align="left"><p>動的にフォールト インジェクションを無効にし、以前にエラーが発生したスタックの一覧をクリアします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>querystatistics</p></td>
<td align="left"><p>フォールト インジェクションの現在の統計情報を示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>incrementcounter</p></td>
<td align="left"><p>単位テストは、障害が挿入されたときに識別するために使用するカウンターを渡します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>getstackid<em>カウンター</em></p></td>
<td align="left"><p>識別子のスタックを取得しますが、指定された挿入します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>excludestack<em>超えて</em></p></td>
<td align="left"><p>フォールト インジェクションからのスタックを除外します。</p></td>
</tr>
</tbody>
</table>



<span id="________flags________Options______"></span><span id="________flags________options______"></span><span id="________FLAGS________OPTIONS______"></span> **/flags** *オプション*   
次の再起動後、指定したオプションがアクティブにします。 Windows 2000 では、この数を 10 進数形式で入力してください。 この数を 10 進数または 16 進数で入力できる Windows XP 以降では、(で、 **0 x**プレフィックス) 形式。 次の値の任意の組み合わせは許可されています。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">10 進数</th>
<th align="left">16 進数</th>
<th align="left">標準の設定</th>
<th align="left">オプション</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>0x1 (ビット 0)</p></td>
<td align="left"><p>x</p></td>
<td align="left"><p><a href="special-pool.md" data-raw-source="[Special Pool](special-pool.md)">特別なプール</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>0x2 (ビット 1)</p></td>
<td align="left"><p>x</p></td>
<td align="left"><p><a href="force-irql-checking.md" data-raw-source="[Force IRQL Checking](force-irql-checking.md)">強制 IRQL 検査</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>4</p></td>
<td align="left"><p>0x4 (ビット 2)</p></td>
<td align="left"></td>
<td align="left"><p><a href="low-resources-simulation.md" data-raw-source="[Low Resources Simulation](low-resources-simulation.md)">低リソース シミュレーション</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>8</p></td>
<td align="left"><p>0x8 (ビット 3)</p></td>
<td align="left"><p>x</p></td>
<td align="left"><p><a href="pool-tracking.md" data-raw-source="[Pool Tracking](pool-tracking.md)">プールの追跡</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>16</p></td>
<td align="left"><p>0x10 (4 ビット)</p></td>
<td align="left"><p>x</p></td>
<td align="left"><p><a href="i-o-verification.md" data-raw-source="[I/O Verification](i-o-verification.md)">I/O の検証</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>32</p></td>
<td align="left"><p>0x20 (bit 5)</p></td>
<td align="left"><p>x</p></td>
<td align="left"><p><a href="deadlock-detection.md" data-raw-source="[Deadlock Detection](deadlock-detection.md)">デッドロックの検出</a>(Windows XP 以降)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>64</p></td>
<td align="left"><p>0x40 (ビット 6)</p></td>
<td align="left"></td>
<td align="left"><p><a href="enhanced-i-o-verification.md" data-raw-source="[Enhanced I/O Verification](enhanced-i-o-verification.md)">I/O の検証の強化</a>(Windows XP 以降) (Windows 7 以降、このオプションは自動的にアクティブ化 I/O の検証を選択すると)</p></td>
</tr>
<tr class="even">
<td align="left"><p>128</p></td>
<td align="left"><p>0x80 (7 ビット)</p></td>
<td align="left"><p>x</p></td>
<td align="left"><p><a href="dma-verification.md" data-raw-source="[DMA Verification](dma-verification.md)">DMA の検証</a>(Windows XP 以降)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>256</p></td>
<td align="left"><p>0x100 (8 ビット)</p></td>
<td align="left"><p>x</p></td>
<td align="left"><p><a href="security-checks.md" data-raw-source="[Security Checks](security-checks.md)">セキュリティ チェック</a>(Windows XP 以降)</p></td>
</tr>
<tr class="even">
<td align="left"><p>512</p></td>
<td align="left"><p>0x200 (ビット 9)</p></td>
<td align="left"></td>
<td align="left"><p><a href="force-pending-i-o-requests.md" data-raw-source="[Force Pending I/O Requests](force-pending-i-o-requests.md)">保留中の I/O 要求を強制</a>(Windows Vista 以降)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>1024</p></td>
<td align="left"><p>0x400 (10 ビット)</p></td>
<td align="left"></td>
<td align="left"><p><a href="irp-logging.md" data-raw-source="[IRP Logging](irp-logging.md)">IRP のログ記録</a>(Windows Server 2003 以降)</p></td>
</tr>
<tr class="even">
<td align="left"><p>2048</p></td>
<td align="left"><p>0x800 (bit 11)</p></td>
<td align="left"><p>x</p></td>
<td align="left"><p><a href="miscellaneous-checks.md" data-raw-source="[Miscellaneous Checks](miscellaneous-checks.md)">その他の検査</a>(Windows Vista 以降)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>8192</p></td>
<td align="left"><p>0x2000 (13 ビット)</p></td>
<td align="left"></td>
<td align="left"><p><a href="invariant-mdl-checking-for-stack.md" data-raw-source="[Invariant MDL Checking for Stack](invariant-mdl-checking-for-stack.md)">不変な Mdl のスタックの</a>(Windows 8 以降)</p></td>
</tr>
<tr class="even">
<td align="left"><p>16384</p></td>
<td align="left"><p>0x4000 (ビット 14)</p></td>
<td align="left"></td>
<td align="left"><p><a href="invariant-mdl-checking-for-driver.md" data-raw-source="[Invariant MDL Checking for Driver](invariant-mdl-checking-for-driver.md)">不変な Mdl のドライバーの</a>(Windows 8 以降)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>32768</p></td>
<td align="left"><p>0x8000 (15 ビット)</p></td>
<td align="left"></td>
<td align="left"><p><a href="concurrency-stress-test.md" data-raw-source="[Power Framework Delay Fuzzing](concurrency-stress-test.md)">Power Framework 遅延ファジー テスト</a>(Windows 8 以降)</p></td>
</tr>
<tr class="even">
<td align="left"><p>65536</p></td>
<td align="left"><p>0x10000 (16 ビット)</p></td>
<td align="left"></td>
<td align="left"><p>チェック (Windows 10 以降) ポート/ミニポート インターフェイス</p></td>
</tr>
<tr class="odd">
<td align="left"><p>131072</p></td>
<td align="left"><p>0x20000 (ビット 17)</p></td>
<td align="left"><p>x</p></td>
<td align="left"><p><a href="ddi-compliance-checking.md" data-raw-source="[DDI compliance checking](ddi-compliance-checking.md)">DDI 準拠の検査</a>(Windows 8 以降)</p></td>
</tr>
<tr class="even">
<td align="left"><p>262144</p></td>
<td align="left"><p>0x40000 (18 ビット)</p></td>
<td align="left"></td>
<td align="left"><p><a href="systematic-low-resource-simulation.md" data-raw-source="[Systematic low resources simulation](systematic-low-resource-simulation.md)">体系的な低リソース シミュレーション</a>(Windows 8.1 以降)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>524288</p></td>
<td align="left"><p>これに対して、0x80000 (ビット 19)</p></td>
<td align="left"></td>
<td align="left"><p><a href="ddi-compliance-checking.md#ddi_compliance_checking_additional" data-raw-source="[DDI compliance checking (additional)](ddi-compliance-checking.md#ddi_compliance_checking_additional)">DDI 準拠の確認 (追加)</a> (Windows 8.1 以降)</p></td>
</tr>
<tr class="even">
<td align="left"><p>2097152</p></td>
<td align="left"><p>0x200000 (21 ビット)</p></td>
<td align="left"></td>
<td align="left"><p><a href="ndis-wifi-verification.md" data-raw-source="[NDIS/WIFI verification](ndis-wifi-verification.md)">NDIS/WIFI 検証</a>(Windows 8.1 以降)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>8388608</p></td>
<td align="left"><p>0x800000 (23 ビット)</p></td>
<td align="left"></td>
<td align="left"><p><a href="kernel-synchronization-delay-fuzzing.md" data-raw-source="[Kernel synchronization delay fuzzing](kernel-synchronization-delay-fuzzing.md)">カーネル同期遅延ファジー テスト</a>(Windows 8.1 以降)</p></td>
</tr>
<tr class="even">
<td align="left"><p>16777216</p></td>
<td align="left"><p>0x1000000 (24 ビット)</p></td>
<td align="left"></td>
<td align="left"><p><a href="vm-switch-verification.md" data-raw-source="[VM switch verification](vm-switch-verification.md)">VM は、検証を切り替える</a>(Windows 8.1 以降)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>33554432</p></td>
<td align="left"><p>0x2000000 (ビット 25)</p></td>
<td align="left"></td>
<td align="left"><p>コードの整合性チェック (Windows 10 以降)</p></td>
</tr>
</tbody>
</table>



このメソッドを使用して、SCSI の検証または Storport 検証オプションをアクティブ化することはできません。 詳しくは、次を参照してください。 [SCSI 検証](scsi-verification.md)と[Storport 検証](dv-storport-verification.md)です。

<span id="________flags________VolatileOptions______"></span><span id="________flags________volatileoptions______"></span><span id="________FLAGS________VOLATILEOPTIONS______"></span> **/flags** *VolatileOptions*   
Windows 2000、Windows XP、および Windows Server 2003 を再起動しなくてもすぐに変更される Driver Verifier のオプションを指定します。 (Windows Vista で使用することができます、 **/volatile**パラメーターすべて **/flags**値)。

Windows 2000 では、10 進数形式で数値を入力します。 Windows XP および Windows 2003 では、10 進数または 16 進形式で数値を入力します (使用、 **0 x**プレフィックス)。

次の値の任意の組み合わせが許可されます。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">10 進数</th>
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



<span id="________iolevel________Level______"></span><span id="________iolevel________level______"></span><span id="________IOLEVEL________LEVEL______"></span> **/iolevel** *レベル*   
(Windows 2000 のみ)レベルを指定します[I/O の検証](i-o-verification.md)です。

値*レベル*できる**1**または**2**します。 既定値は**1**します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">レベル値</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>1</strong></p></td>
<td align="left"><p>により、レベル 1 の I/O の検証 (既定値)</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>2</strong></p></td>
<td align="left"><p>第 1 レベルの I/O の検証によって、第 2 レベルの I/O の検証</p></td>
</tr>
</tbody>
</table>



I/O の検証が有効でない場合 (を使用して **/flags 0x10**)、 **/iolevel**は無視されます。

<span id="________log________LogFileName_______interval_Seconds_______"></span><span id="________log________logfilename_______interval_seconds_______"></span><span id="________LOG________LOGFILENAME_______INTERVAL_SECONDS_______"></span> **/log** *LogFileName* \[**/interval**|*Seconds*\]   
名前のログ ファイルが作成*LogFileName*します。 Driver Verifier は、このファイルに、統計情報を定期的に書き込みます。 詳細については、次を参照してください。[ログ ファイルの作成](creating-log-files.md)です。

場合、 **verifier/log**コマンドラインでコマンドを入力すると、コマンド プロンプトは返されません。 ログ ファイルを閉じるし、プロンプトを返すするには、ctrl キーを押しながら C キーを使用します。 再起動後、ログを作成する必要がありますを送信する、 **verifier/log**コマンドを再実行します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">オプション</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="________interval________Seconds______"></span><span id="________interval________seconds______"></span><span id="________INTERVAL________SECONDS______"></span> <strong>/interval</strong> <em>秒</em></p></td>
<td align="left"><p>ログ ファイルの更新間隔を指定します。 既定は 30 秒です。</p></td>
</tr>
</tbody>
</table>



<span id="_rules_Option"></span><span id="_rules_option"></span><span id="_RULES_OPTION"></span>**ルール/** *オプション*  
無効にすることができます (詳細) ルールのオプションです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">オプション</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>query</strong></p></td>
<td align="left"><p>制御可能な規則の現在の状態を示しています。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>reset</strong></p></td>
<td align="left"><p>すべてのルールを既定の状態にリセットします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>既定</strong> <em>ID</em></p></td>
<td align="left"><p>ルールのセット<em>ID</em>既定の状態にします。 サポートされている規則、ルールの<em>ID</em>は、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff560187" data-raw-source="[&lt;strong&gt;Bug Check 0xC4&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560187)"><strong>バグ チェック 0xC4</strong> </a> (DRIVER_VERIFIER_DETECTED_VIOLATION) パラメーター 1 の値。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>無効にする</strong> <em>ID</em></p></td>
<td align="left"><p>指定されたルールを無効にします<em>ID</em>します。 サポートされている規則、ルールの<em>ID</em>は、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff560187" data-raw-source="[&lt;strong&gt;Bug Check 0xC4&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560187)"><strong>バグ チェック 0xC4</strong> </a> (DRIVER_VERIFIER_DETECTED_VIOLATION) パラメーター 1 の値。</p></td>
</tr>
</tbody>
</table>



<span id="________standard"></span><span id="________STANDARD"></span> **標準/**  
(Windows XP 以降)[次へ] の起動後に"standard"または既定の Driver Verifier のオプションがアクティブにします。 Windows XP の標準的なオプションは[特別なプール](special-pool.md)、[強制 IRQL 検査](force-irql-checking.md)、[プール追跡](pool-tracking.md)、 [I/O の検証](i-o-verification.md)、 [デッドロックの検出](deadlock-detection.md)、および[DMA の検証](dma-verification.md)です。 これに相当 **/flags 0 xbb です**します。 Windows Vista 以降、標準のオプションも含まれます[セキュリティ チェック](security-checks.md)と[(その他) を確認します](miscellaneous-checks.md)します。 これに相当 **/flags 0x9BB**します。 Windows 8 以降、標準のオプションはそのも含める[DDI 準拠の検査](ddi-compliance-checking.md)します。 これに相当 **/flags 0x209BB**します。

> [!NOTE]
> Windows 10 のバージョンを使用して、1803 後以降 **/flags 0x209BB** WDF の検証を有効に自動的に行われなくなります。 使用して、 **標準/** WDF の検証に含まれる標準のオプションを有効にする構文。 参照してください[Driver Verifier のコマンド構文](https://docs.microsoft.com/windows-hardware/drivers/devtest/verifier-command-line)詳細についてはします。

<span id="________volatile______"></span><span id="________VOLATILE______"></span> **/volatile**   
コンピューターを再起動しなくても、設定を変更します。 揮発性の設定は、すぐに反映します。

Windows Vista と Windows の以降のバージョンで使用することができます、 **/volatile**パラメーター、 **/flags**パラメーターを有効にし、再起動しなくてもいくつかのオプションを無効にします。 使用することも **/volatile**で、 **/adddriver**と **/removedriver**パラメーター開始または再起動せずに、ドライバーの検証を停止する場合でもドライバー検証ツールが既に実行されていません。

Windows Vista では、前に Windows のバージョンで、 **/volatile**パラメーターのオプションでのみ使用できます*VolatileOptions*開始または停止することがなく、ドライバーの検証するために使用することができますドライバーの検証ツールが既に実行されていると、コンピューターが再起動された場合にのみ再起動しています。

詳細については、次を参照してください。[揮発性の設定を使用する](using-volatile-settings.md)します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">オプション</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="__adddriver_VolatileDriverList"></span><span id="__adddriver_volatiledriverlist"></span><span id="__ADDDRIVER_VOLATILEDRIVERLIST"></span> <strong>/adddriver</strong> <em>VolatileDriverList</em></p></td>
<td align="left"><p>(Windows XP 以降)揮発性の設定に指定されたドライバーを追加します。 複数のドライバーを指定するには、スペースで区切られた、名前を一覧表示します。 N などのワイルドカード値<em>.sys はサポートされていません。 参照してください<a href="using-volatile-settings.md" data-raw-source="[Using Volatile Settings](using-volatile-settings.md)">揮発性の設定を使用する</a>詳細についてはします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="_removedriver_VolatileDriverList"></span><span id="_removedriver_volatiledriverlist"></span><span id="_REMOVEDRIVER_VOLATILEDRIVERLIST"></span><strong>/removedriver</strong> <em>VolatileDriverList</em></p></td>
<td align="left"><p>(Windows XP 以降)揮発性の設定から指定されたドライバーを削除します。 複数のドライバーを指定するには、スペースで区切られた、名前を一覧表示します。 N などのワイルドカード値</em>.sys はサポートされていません。 参照してください<a href="using-volatile-settings.md" data-raw-source="[Using Volatile Settings](using-volatile-settings.md)">揮発性の設定を使用する</a>詳細についてはします。</p></td>
</tr>
</tbody>
</table>



<span></span>  

<span id="________reset______"></span><span id="________RESET______"></span> **/reset**   
すべてのドライバーの検証設定をクリアします。 [次へ] の起動後に、ドライバーが検証なし。

<span id="________querysettings______"></span><span id="________QUERYSETTINGS______"></span> **/querysettings**   
(Windows XP 以降)オプションが有効にして、[次へ] の起動後に確認されるドライバーの概要を表示します。 ドライバーとオプションを使用して追加、表示は含まれません、 **/volatile**パラメーター。 これらの設定を表示するその他の方法では、次を参照してください。[ドライバー検証ツールの設定を表示する](viewing-driver-verifier-settings.md)します。

<span id="________query______"></span><span id="________QUERY______"></span> **/query**   
Driver Verifier の現在のアクティビティの概要を表示します。 **レベル**表示のフィールドはオプションと設定の 16 進数の値、 **/volatile**パラメーター。 参照してください[グローバル カウンターの監視](monitoring-global-counters.md)と[カウンターを個別に監視](monitoring-individual-counters.md)の各統計情報の説明。

<span id="________domain_Types_Options_______"></span><span id="________domain_types_options_______"></span><span id="________DOMAIN_TYPES_OPTIONS_______"></span> **/domain** *型* **** *オプション*   
検証拡張機能の設定を制御します。 次の検証拡張機能の種類がサポートされています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><em>型</em></th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="wdm"></span><span id="WDM"></span><strong>wdm</strong></p></td>
<td align="left"><p>WDM ドライバー検証ツールの拡張機能を有効にします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="ndis"></span><span id="NDIS"></span><strong>ndis</strong></p></td>
<td align="left"><p>ネットワークのドライバーの検証ツールの拡張機能を有効にします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="ks"></span><span id="KS"></span><strong>ks</strong></p></td>
<td align="left"><p>カーネル モードのドライバーをストリーミング用の検証ツールの拡張機能を有効にします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="audio"></span><span id="AUDIO"></span><strong>オーディオ</strong></p></td>
<td align="left"><p>オーディオ ドライバーの検証ツールの拡張機能を有効にします。</p></td>
</tr>
</tbody>
</table>



次の拡張機能オプションがサポートされています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><em>[オプション]</em></th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="rules.default"></span><span id="RULES.DEFAULT"></span><strong>rules.default</strong></p></td>
<td align="left"><p>選択されている検証拡張機能の既定の検証規則を有効にします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="rules.all"></span><span id="RULES.ALL"></span><strong>rules.all</strong></p></td>
<td align="left"><p>選択されている検証拡張機能のすべての検証規則を有効にします。</p></td>
</tr>
</tbody>
</table>

<span id="________logging_______"></span><span id="________LOGGING_______"></span> **/logging**   
ログを有効には、選択されている検証拡張機能によって検出されたルールに違反します。

<span id="________livedump_______"></span><span id="________LIVEDUMP_______"></span> **/livedump**   
有効では、選択されている検証拡張機能によって検出された規則違反のメモリ ダンプの収集を live です。

<span id="_______________"></span> **/?**   
コマンドラインのヘルプを表示します。

これらのコマンドの使用に関する詳細については、次を参照してください。 [Driver Verifier を制御する](controlling-driver-verifier.md)と[Driver Verifier の監視](monitoring-driver-verifier.md)します。

<span id="________help______"></span><span id="________HELP______"></span> **/help**   
コマンドラインのヘルプを表示します。

これらのコマンドの使用に関する詳細については、次を参照してください。 [Driver Verifier を制御する](controlling-driver-verifier.md)と[Driver Verifier の監視](monitoring-driver-verifier.md)します。

## <a name="span-idreturncodesspanspan-idreturncodesspanspan-idreturncodesspanreturn-codes"></a><span id="Return_Codes"></span><span id="return_codes"></span><span id="RETURN_CODES"></span>リターン コード


ドライバーの検証を実行した後、次の値が返されます。

|     |                            |
|-----|----------------------------|
| 0   | 終了\_コード\_成功        |
| 1   | 終了\_コード\_エラー          |
| 2   | 終了\_コード\_再起動\_が必要 |











