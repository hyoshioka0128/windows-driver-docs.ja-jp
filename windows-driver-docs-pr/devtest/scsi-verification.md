---
title: SCSI 検証
description: SCSI 検証
ms.assetid: dba63137-ff92-480a-bca4-ab651a6bda85
keywords:
- SCSI 検証機能 WDK Driver Verifier
- ミニポート ドライバー WDK Driver Verifier
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e39ca269b03754af4270ab9f1ef2eb2f2c159c1a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373599"
---
# <a name="scsi-verification"></a>SCSI 検証


## <span id="ddk_scsi_verification_tools"></span><span id="DDK_SCSI_VERIFICATION_TOOLS"></span>


Driver Verifier の SCSI 検証機能では、SCSI ミニポート ドライバー、ポート ドライバーとの対話を監視します。 ルーチン、ミニポート ドライバー誤っていない正しくまたは応答する要求をポート ドライバーから、過剰な要求に応答する時間のかかるバグ チェックが発行されます。

このドライバーの検証ツールのオプションは、Windows XP で使用できる以降のみです。

### <a name="span-idviolationsdetectedbyscsiverificationspanspan-idviolationsdetectedbyscsiverificationspanviolations-detected-by-scsi-verification"></a><span id="violations_detected_by_scsi_verification"></span><span id="VIOLATIONS_DETECTED_BY_SCSI_VERIFICATION"></span>SCSI 検証によって検出された違反

SCSI の確認オプションには、SCSI ルーチンのいくつか誤ってを検出できます。 これらのチェックの特定を個別に無効にすることもできます。

SCSI ミニポート ドライバー コミットすると、次の違反のいずれかの Driver Verifier 0xF1 のバグ チェックが発行されます。

-   ミニポート ドライバーに無効な引数を渡す**ScsiPortInitialize**します。

-   ミニポート ドライバー呼び出し**ScsiPortStallExecution**失速プロセッサ時間の過度の長さを 0.1 秒より長い遅延を指定します。

-   ポート ドライバーは、ミニポート ドライバーのルーチンを呼び出すし、ミニポート ドライバーを実行するために 0.5 秒より長くかかります。 (、 **FindAdapter**ルーチンは、除外、 **HwInitialize**ルーチンには、5 秒間は許可されています)。

-   ミニポート ドライバーでは、複数回の要求を完了します。

-   ミニポート ドライバーでは、無効な SRB 状態のルーチンを完了します。

-   ミニポート ドライバー呼び出し**ScsiPortNotification**を求める**NextLuRequest**、タグなしの要求にアクティブなままですが。

-   ミニポート ドライバーに無効な仮想アドレスを渡す**ScsiPortGetPhysicalAddress**します。 (つまり、通常、一般的なバッファー領域に指定されたアドレスがマップされない。)

-   バスのリセットの保持期間の終了が、ミニポート ドライバーにはまだ未処理の要求。

参照してください[**バグ チェック 0xF1** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xf1--scsi-verifier-detected-violation) (SCSI\_VERIFIER\_検出\_違反) バグの完全な一覧については、パラメーターを確認します。

だけでなく、これらの違反、SCSI 検証は、不適切な使用のミニポート ドライバーのメモリへのアクセスを監視します。 ミニポート ドライバーによって行われた 2 つの一般的なメモリ違反が、要求が完了した後 SRB の拡張機能へのアクセスと SRB へのアクセス**DataBuffer**ミニポート ドライバーが指定されていない場合**MapBuffers**.

この種のメモリの違反は通常のなる[ **0xD1 のバグ チェック**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xd1--driver-irql-not-less-or-equal) (ドライバー\_IRQL\_いない\_少ない\_または\_と等しい)発行されています。

### <a name="span-idactivatingthisoptionspanspan-idactivatingthisoptionspanactivating-this-option"></a><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>このオプションをアクティブ化します。

SCSI の確認オプションをアクティブ化するための手順では、その他の Driver Verifier のオプションがアクティブ化するためのプロシージャから異なります。

**SCSI 検証をアクティブ化するには**

1.  ドライバー検証マネージャーまたは Verifier.exe コマンドラインを使用して、ミニポート ドライバーの検証が起動します。 SCSI 検証はオプションとして利用できない、ため、他の Driver Verifier の少なくとも 1 つのオプションを選択します。 参照してください[ドライバー検証ツールのオプションの選択](selecting-driver-verifier-options.md)と[検証するドライバーを選択すると](selecting-drivers-to-be-verified.md)詳細についてはします。

2.  Regedit.exe を使用してレジストリを開きます。 **HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\コントロール\\ScsiPort**キーを追加するという名前のサブキー**検証ツール**. そのキーを追加、REG\_という名前の DWORD エントリ**VerifyLevel**します。 このエントリに割り当てられた値は、SCSI 検証テストがアクティブになりますが決まります。 0x1 の値では、最大の検証を提供します。

3.  コンピューターを再起動します。

場合、 **VerifyLevel**値が存在しないか 0 xffffffff と等しく、SCSI 検証が無効になります。

個々 のビットで、 **VerifyLevel**値を正確にテストが実行されるコントロールを使用できます。 ビットが 0 (0x1) により、特定のテスト28、29、30、31 ビットは、特定のテストを無効にします。 そのため、最大の検証は、値 0x00000001 を使用して取得できます。

ビットごとの影響は次のとおりです。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ビット</th>
<th align="left">Value</th>
<th align="left">効果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>0x1</p></td>
<td align="left"><p>Driver Verifier は、ミニポート ドライバーのメモリ アクセスを監視し、メモリ バッファーの不適切な使用を確認します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>28</p></td>
<td align="left"><p>0x10000000</p></td>
<td align="left"><p>ドライバー検証ツールは問題するときにバグ チェックではありません、 <strong>HwAdapterControl</strong>ルーチンは、複数の 0.5 秒です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>29</p></td>
<td align="left"><p>0x20000000</p></td>
<td align="left"><p>Driver Verifier では、リセット保留期間が終了し、論理ユニット上にまだ保留中の要求があるときのバグ チェックは発行されません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>30</p></td>
<td align="left"><p>0x40000000</p></td>
<td align="left"><p>Driver Verifier は、ミニポート ドライバーを呼び出すときのバグ チェックが発行されません<strong>ScsiPortNotification</strong>で<strong>NextLuRequest</strong>タグなしの要求がアクティブな状態です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>31</p></td>
<td align="left"><p>0x80000000</p></td>
<td align="left"><p>ドライバー検証ツールは問題するときにバグ チェックではありません、 <strong>HwInitialize</strong>ルーチンは、完了に 5 秒以上。</p></td>
</tr>
</tbody>
</table>

 

ほとんどの場合、推奨設定値は 0xD0000001 します。 これにより、すべて**SCSI Verifier**上での制限時間を除くテスト**HwAdapterControl**、時間の制限**HwInitialize**、および複数の要求を論理の禁止単位です。 これら 3 つのテストが厳しすぎるではよくあります。

カーネル デバッガーがアタッチされている場合は、ブート サイクルの後に SCSI 検証レベルを変更することはできます。 これを行うには、デバッガー コマンドを使用します。

```
kd> ed scsiport!SpVrfyLevel Level 
```

このコマンドでは、新しい値を設定できます。*レベル*します。 このメソッドを使用して、いつでも、上位ビット (0x10000000 0x8000000 経由) を変更できます。 ただし、下位ビット (0x1) を変更する場合 (カーネル デバッガーの最初のブレークポイント) でブート プロセス中にはする必要があります。

同様に、SCSI 検証を完全に非アクティブ化する場合は、設定する必要*レベル*を最初のブレークポイントで 0 xffffffff にします。

**注**   0xF0000000 値は、すべてのテストを無効になりますが、SCSI 検証モジュールがまだ読み込まれます。 検証を無効にするには後で、高ビット テストを有効にしようとする場合は、この値を使用します。 その一方で、値が 0 xffffffff モジュールが読み込まれなく完全;この値は、ブート時に使用されます場合、を再起動しなくても SCSI 検証を有効にすることはできません。

 

### <a name="span-idactivatingwithoutrebootingspanspan-idactivatingwithoutrebootingspanactivating-without-rebooting"></a><span id="activating_without_rebooting"></span><span id="ACTIVATING_WITHOUT_REBOOTING"></span>再起動しなくてもアクティブ化します。

(「再起動」) を再起動しなくても SCSI 検証をアクティブまたはアクティブ化することはできません一般に、任意の Windows オペレーティング システム上のコンピューター。 ScsiPort.sys ドライバーの読み込み、 **VerifyLevel**これは、通常ブート時にレジストリ エントリ、読み込み時にのみです。 ただし、レジストリ エントリを追加すると、ScsiPort.sys ドライバーが読み込まれていない場合、またはアンロードされ、再読み込みする場合は、コンピューターを再起動しなくても Windows XP と Windows の以降のバージョンで SCSI の検証を有効にできます。

 

 





