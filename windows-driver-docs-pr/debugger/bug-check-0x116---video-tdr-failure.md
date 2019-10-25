---
title: バグチェック 0x116 VIDEO_TDR_FAILURE
description: VIDEO_TDR_FAILURE のバグチェックの値は0x00000116 です。 これは、ディスプレイドライバーをリセットしようとして、タイムアウトから回復できなかったことを示します。
ms.assetid: 06fe312a-e2d3-479f-b0fb-06c0ac79be32
keywords:
- バグチェック 0x116 VIDEO_TDR_FAILURE
- VIDEO_TDR_FAILURE
- VIDEO_TDR_ERROR
ms.date: 01/17/2019
topic_type:
- apiref
api_name:
- VIDEO_TDR_FAILURE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5185ee6fcef882195a09f614c941edadc5aab276
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837835"
---
# <a name="bug-check-0x116-video_tdr_failure"></a>バグチェック 0x116: VIDEO\_TDR\_エラー


VIDEO\_TDR\_エラーのバグチェックには、0x00000116 の値が指定されています。 これは、ディスプレイドライバーをリセットしようとして、タイムアウトから回復できなかったことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


## <a name="video_tdr_failure-parameters"></a>ビデオ\_TDR\_エラーパラメーター


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
<td align="left"><p>内部 TDR 復旧コンテキストへのポインター (使用可能な場合)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>担当デバイスドライバーモジュール (所有者タグなど) へのポインター。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>失敗した最後の操作のエラーコード (使用可能な場合)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ホーム フォルダーが置かれているコンピューターにアクセスできない</p></td>
<td align="left"><p>内部コンテキスト依存データ (使用可能な場合)。</p></td>
</tr>
</tbody>
</table>



<a name="cause"></a>原因
-----

グラフィックスでの一般的な安定性の問題は、エンドユーザーのコマンドまたは操作の処理中にシステムが完全にフリーズまたはハングしたときに発生します。 通常、GPU は通常はゲームプレイ中に大量のグラフィックス操作を処理することがビジー状態です。 画面の更新は行われず、ユーザーのシステムがフリーズしていると想定されます。 通常、ユーザーは数秒待ってから、電源ボタンを押してシステムを再起動します。 Windows は、これらの問題のあるハング状態を検出し、応答性の高いデスクトップを動的に回復しようとします。

この検出と復旧のプロセスは、タイムアウトの検出と復旧 (TDR) と呼ばれています。 既定のタイムアウトは2秒です。 ビデオカードの TDR プロセスでは、オペレーティングシステムの GPU スケジューラがディスプレイミニポートドライバーの[*DxgkDdiResetFromTimeout*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_resetfromtimeout)関数を呼び出して、ドライバーを再初期化し、GPU をリセットします。

このプロセスでは、オペレーティングシステムは、ハードウェアまたはメモリにアクセスしないようにドライバーに指示し、現在実行中のスレッドが完了するまでの時間を短縮します。 スレッドがタイムアウト内に完了しない場合は、システムバグによって 0x116 VIDEO\_TDR\_エラーがチェックされます。 詳細については、「[スレッドの同期と TDR](https://docs.microsoft.com/windows-hardware/drivers/display/thread-synchronization-and-tdr)」を参照してください。

また、TDR イベントが短時間に発生した場合は、ビデオ\_\_TDR のバグチェックを行うこともできます。既定では、1分で5つを超える TDRs が発生します。

回復プロセスが成功すると、"表示ドライバーが応答を停止し、回復しました。" というメッセージが表示されます。

詳細については、 [Windows Display Driver Model (WDDM) のデバッグのヒント](https://docs.microsoft.com/windows-hardware/drivers/display/debugging-tips-for-the-windows-vista-display-driver-model)に記載されている「タイムアウトの検出と回復」 (TDR)、「 [TDR レジストリキー](https://docs.microsoft.com/windows-hardware/drivers/display/tdr-registry-keys) 」、および「 [windows 8 の TDR の変更点](https://docs.microsoft.com/windows-hardware/drivers/display/tdr-changes-in-windows-8)」を参照してください。

<a name="resolution"></a>解像度
----------

GPU のモニターへのグラフィックスの表示が許可されている時間を超えています。 この動作は、次の1つまたは複数の理由で発生する可能性があります。

-   TDR プロセスが正しくサポートされるように、表示ドライバーの最新の更新プログラムをインストールすることが必要になる場合があります。
-   次のような、ビデオカードが正しく動作することに影響するハードウェアの問題。
    -   オーバークロックコンポーネント (マザーボードなど)
    -   コンポーネントの互換性と設定が正しくない (特にメモリの構成とタイミング)
    -   システムの冷却が不十分
    -   システム電源が不足しています
    -   欠陥のあるパーツ (メモリモジュール、マザーボードなど)
-   視覚効果、またはバックグラウンドで実行されているプログラムが多すぎると、ビデオカードが必要に応じて応答しないように、PC の速度が低下する可能性があります。

! [デバッグ拡張機能の[**分析**](-analyze.md)] には、バグチェックに関する情報が表示され、根本原因を特定するのに役立ちます。

```dbgcmd
1: kd> !analyze -v
*******************************************************************************
*                                                                             *
*                        Bugcheck Analysis                                    *
*                                                                             *
*******************************************************************************

VIDEO_TDR_FAILURE (116)
Attempt to reset the display driver and recover from timeout failed.
Arguments:
Arg1: ffffe000c2c404c0, Optional pointer to internal TDR recovery context (TDR_RECOVERY_CONTEXT).
Arg2: fffff8016470c14c, The pointer into responsible device driver module (e.g. owner tag).
Arg3: ffffffffc000009a, Optional error code (NTSTATUS) of the last failed operation.
Arg4: 0000000000000004, Optional internal context dependent data.

...
```

また、エラーが発生したモジュール名も表示されます

```dbgcmd
MODULE_NAME: nvlddmkm

IMAGE_NAME:  nvlddmkm.sys
```

[**Lm (List Loaded Modules)** ](lm--list-loaded-modules-.md)コマンドを使用して、タイムスタンプを含む、エラーが発生しているドライバーに関する情報を表示できます。

```dbgcmd
1: kd> lmvm nvlddmkm
Browse full module list
start             end                 module name
fffff801`63ec0000 fffff801`649a7000   nvlddmkm T (no symbols)           
    Loaded symbol image file: nvlddmkm.sys
    Image path: \SystemRoot\system32\DRIVERS\nvlddmkm.sys
    Image name: nvlddmkm.sys
    Browse all global symbols  functions  data
    Timestamp:        Wed Jul  8 15:43:44 2015 (559DA7A0)
    CheckSum:         00AA7491
    ImageSize:        00AE7000
    Translations:     0000.04b0 0000.04e4 0409.04b0 0409.04e4
```

パラメーター1には、TDR\_RECOVERY\_コンテキストへのポインターが含まれています。 ! Analyze 出力に示されているように、関連付けられているコードのシンボルがある場合は、dt コマンドを使用してこのデータを表示できます。

```dbgcmd
1: kd> dt dxgkrnl!_TDR_RECOVERY_CONTEXT ffffe000c2c404c0
   +0x000 Signature        : 0x52445476
   +0x008 pState           : 0xffffe000`c2b12a40 ??
   +0x010 TimeoutReason    : 9 ( TdrEngineTimeoutPromotedToAdapterReset )
   +0x018 Tick             : _ULARGE_INTEGER 0xb2
   +0x020 pAdapter         : 0xffffe000`c2a89010 DXGADAPTER
   +0x028 pVidSchContext   : (null) 
   +0x030 GPUTimeoutData   : _TDR_RECOVERY_GPU_DATA
   +0x048 CrtcTimeoutData  : _TDR_RECOVERY_CONTEXT::<unnamed-type-CrtcTimeoutData>
   +0x050 pProcessName     : (null) 
   +0x058 DbgOwnerTag      : 0xfffff801`6470c14c
   +0x060 PrivateDbgInfo   : _TDR_DEBUG_REPORT_PRIVATE_INFO
   +0xb00 pDbgReport       : 0xffffe000`c2c3f750 _WD_DEBUG_REPORT
   +0xb08 pDbgBuffer       : 0xffffc000`bd000000 Void
   +0xb10 DbgBufferSize    : 0x37515
   +0xb18 pDumpBufferHelper : (null) 
   +0xb20 pDbgInfoExtension : 0xffffc000`ba7e47a0 _DXGKARG_COLLECTDBGINFO_EXT
   +0xb28 pDbgBufferUpdatePrivateInfo : 0xffffc000`bd000140 Void
   +0xb30 ReferenceCount   : 0n1
   +0xb38 pResetCompletedEvent : (null) 
```

パラメーター2には、担当デバイスドライバーモジュール (所有者タグなど) へのポインターが含まれています。

```dbgcmd
1: kd> ub fffff8016470c14c
nvlddmkm+0x84c132:
fffff801`6470c132 cc              int     3
fffff801`6470c133 cc              int     3
fffff801`6470c134 48ff254d2deaff  jmp     qword ptr [nvlddmkm+0x6eee88 (fffff801`645aee88)]
fffff801`6470c13b cc              int     3
fffff801`6470c13c 48ff252d2eeaff  jmp     qword ptr [nvlddmkm+0x6eef70 (fffff801`645aef70)]
fffff801`6470c143 cc              int     3
fffff801`6470c144 48ff257d2deaff  jmp     qword ptr [nvlddmkm+0x6eeec8 (fffff801`645aeec8)]
fffff801`6470c14b cc              int     3
```

[**K、kb、kc、kd、kp、kp、kv (スタックバックトレースの表示)** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)コマンドを使用して、スタックトレースを調べることができます。

```dbgcmd
1: kd> k
 # Child-SP          RetAddr           Call Site
00 ffffd001`7d53d918 fffff801`61ba2b4c nt!KeBugCheckEx [d:\th\minkernel\ntos\ke\amd64\procstat.asm @ 122]
01 ffffd001`7d53d920 fffff801`61b8da0e dxgkrnl!TdrBugcheckOnTimeout+0xec [d:\th\windows\core\dxkernel\dxgkrnl\core\dxgtdr.cxx @ 2731]
02 ffffd001`7d53d960 fffff801`61b8dd7f dxgkrnl!ADAPTER_RENDER::Reset+0x15e [d:\th\windows\core\dxkernel\dxgkrnl\core\adapter.cxx @ 19443]
03 ffffd001`7d53d990 fffff801`61ba2385 dxgkrnl!DXGADAPTER::Reset+0x177 [d:\th\windows\core\dxkernel\dxgkrnl\core\adapter.cxx @ 19316]
04 ffffd001`7d53d9e0 fffff801`63c5fba7 dxgkrnl!TdrResetFromTimeout+0x15 [d:\th\windows\core\dxkernel\dxgkrnl\core\dxgtdr.cxx @ 2554]
05 ffffd001`7d53da10 fffff801`63c47e5d dxgmms1!VidSchiRecoverFromTDR+0x11b [d:\th\windows\core\dxkernel\dxgkrnl\dxgmms1\vidsch\vidscher.cxx @ 1055]
06 ffffd001`7d53dbc0 fffff801`aa55c698 dxgmms1!VidSchiWorkerThread+0x8d [d:\th\windows\core\dxkernel\dxgkrnl\dxgmms1\vidsch\vidschi.cxx @ 426]
07 ffffd001`7d53dc00 fffff801`aa5c9306 nt!PspSystemThreadStartup+0x58 [d:\th\minkernel\ntos\ps\psexec.c @ 6845]
08 ffffd001`7d53dc60 00000000`00000000 nt!KxStartSystemThread+0x16 [d:\th\minkernel\ntos\ke\amd64\threadbg.asm @ 80]
```

また、停止コードを一貫して再現できる場合は、この stop コードまでのコードの先頭にブレークポイントを設定し、エラーが発生したコードへのシングルステップフォワードを試行することもできます。

詳細については、以下のトピックを参照してください。

[Windows デバッガー (WinDbg) を使用したクラッシュダンプ分析](crash-dump-files.md)

Windows デバッガーを使用してこの問題に対処することができない場合は、いくつかの基本的なトラブルシューティング手法を使用できます。

-   このバグチェックの原因となっているデバイスまたはドライバーの特定に役立つ可能性のある追加のエラーメッセージについては、イベントビューアーのシステムログを確認してください。

-   バグ チェックのメッセージでドライバーが特定された場合は、そのドライバーを無効にするか、ドライバーの更新状況を製造元に確認します。

-   DirectX や OpenGL などのすべてのグラフィックス関連ソフトウェアが最新であること、およびグラフィックス集中型アプリケーション (ゲームなど) に完全にパッチが適用されていることを確認します。
-   インストールされている新しいハードウェアに、インストールされている Windows のバージョンとの互換性があることを確認します。 たとえば、 [Windows 10 の仕様](https://www.microsoft.com/windows/windows-10-specifications)では、必要なハードウェアに関する情報を取得できます。

-   **セーフモードの使用**

    この問題を特定するには、セーフモードを使用することを検討してください。 セーフモードを使用すると、Windows の起動時に最小限必要なドライバーとシステムサービスのみが読み込まれます。 セーフモードに移行するには、設定 で **更新とセキュリティ** を使用します。 **回復**- を選択して、メンテナンスモードで起動する&gt;**詳細なスタートアップ** を選択します。 生成されたメニューで **トラブルシューティング** を選択し、-&gt;**詳細オプション** -&gt;**スタートアップ設定** -&gt;**再起動** を選択します。 Windows が**起動設定**画面に再起動したら、オプション、4、5、または6を選択してセーフモードで起動します。

    セーフモードは、起動時にファンクションキーを押すと (例 F8)、使用できる場合があります。 特定のスタートアップオプションについては、製造元の情報を参照してください。

-   Windows メモリ診断ツールを実行して、メモリをテストします。 コントロールパネルの検索ボックスに「Memory」と入力し、 **[コンピューターのメモリの問題を診断する]** をクリックします。テストの実行後、イベントビューアーを使用して、システムログの下に結果を表示します。 結果を表示するには、 *Memorydiagnostics-results*エントリを探します。

-   システムの製造元から提供されているハードウェア診断を実行できます。

-   一般的なトラブルシューティング情報については、「 [**Blue Screen Data**](blue-screen-data.md)」を参照してください。

<a name="remarks"></a>注釈
-------

**ハードウェア認定の要件**

TDR を実装するときにハードウェアデバイスが満たす必要のある要件の詳細については、「*デバイス...TDRResiliency*。








