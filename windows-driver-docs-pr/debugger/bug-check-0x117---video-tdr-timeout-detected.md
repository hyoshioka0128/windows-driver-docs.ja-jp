---
title: バグチェック 0x117 VIDEO_TDR_TIMEOUT_DETECTED
description: VIDEO_TDR_TIMEOUT_DETECTED のバグチェックの値は0x00000117 です。 これは、ディスプレイドライバーが時間内に応答できなかったことを示します。
ms.assetid: 70e24a97-f695-4d35-b52f-69dfddecd9b5
keywords:
- バグチェック 0x117 VIDEO_TDR_TIMEOUT_DETECTED
- VIDEO_TDR_TIMEOUT_DETECTED
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- VIDEO_TDR_TIMEOUT_DETECTED
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8990b57cc000d03a572f9a5a21af56483a042e9d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837637"
---
# <a name="bug-check-0x117-video_tdr_timeout_detected"></a>バグチェック 0x117: VIDEO\_TDR\_TIMEOUT\_検出されました


ビデオ\_TDR\_TIMEOUT\_検出されたバグチェックの値は0x00000117 です。 これは、ディスプレイドライバーが時間内に応答できなかったことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


## <a name="video_tdr_timeout_detected-parameters"></a>ビデオ\_TDR\_TIMEOUT\_検出されたパラメーター


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
<td align="left"><p>セカンダリドライバー固有のバケットキー。</p></td>
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
3: kd> !analyze -v
*******************************************************************************
*                                                                             *
*                        Bugcheck Analysis                                    *
*                                                                             *
*******************************************************************************

VIDEO_TDR_TIMEOUT_DETECTED (117)
The display driver failed to respond in timely fashion.
(This code can never be used for a real bugcheck.)
Arguments:
Arg1: 8975d500, Optional pointer to internal TDR recovery context (TDR_RECOVERY_CONTEXT).
Arg2: 9a02381e, The pointer into responsible device driver module (e.g owner tag).
Arg3: 00000000, The secondary driver specific bucketing key.
Arg4: 00000000, Optional internal context dependent data.

...
```

また、エラーが発生したモジュール名も表示されます

```dbgcmd
MODULE_NAME: atikmpag

IMAGE_NAME:  atikmpag.sys
```

Lmv コマンドを使用すると、タイムスタンプを含む、エラーが発生しているドライバーに関する情報を表示できます。

```dbgcmd
3: kd> lmvm atikmpag
Browse full module list
start    end        module name
9a01a000 9a09a000   atikmpag T (no symbols)           
    Loaded symbol image file: atikmpag.sys
    Image path: atikmpag.sys
    Image name: atikmpag.sys
    Browse all global symbols  functions  data
    Timestamp:        Fri Dec  6 12:20:32 2013 (52A23190)
    CheckSum:         0007E58A
    ImageSize:        00080000
    Translations:     0000.04b0 0000.04e4 0409.04b0 0409.04e4
```

パラメーター1には、TDR\_RECOVERY\_コンテキストへのポインターが含まれています。

```dbgcmd
3: kd> dt dxgkrnl!_TDR_RECOVERY_CONTEXT fffffa8010041010
   +0x000 Signature        : ??
   +0x004 pState           : ???? 
   +0x008 TimeoutReason    : ??
   +0x010 Tick             : _ULARGE_INTEGER
   +0x018 pAdapter         : ???? 
   +0x01c pVidSchContext   : ???? 
   +0x020 GPUTimeoutData   : _TDR_RECOVERY_GPU_DATA
   +0x038 CrtcTimeoutData  : _TDR_RECOVERY_CONTEXT::<unnamed-type-CrtcTimeoutData>
   +0x040 DbgOwnerTag      : ??
   +0x048 PrivateDbgInfo   : _TDR_DEBUG_REPORT_PRIVATE_INFO
   +0xae0 pDbgReport       : ???? 
   +0xae4 pDbgBuffer       : ???? 
   +0xae8 DbgBufferSize    : ??
   +0xaec pDumpBufferHelper : ???? 
   +0xaf0 pDbgInfoExtension : ???? 
   +0xaf4 pDbgBufferUpdatePrivateInfo : ???? 
   +0xaf8 ReferenceCount   : ??
Memory read error 10041b08
```

パラメーター2には、担当デバイスドライバーモジュール (所有者タグなど) へのポインターが含まれています。

```dbgcmd
BUGCHECK_P2: ffffffff9a02381e
```

[**K、kb、kc、kd、kp、kp、kv (スタックバックトレースの表示)** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)コマンドを使用して、スタックトレースを調べることができます。

```dbgcmd
3: kd> k
 # ChildEBP RetAddr  
00 81d9ace0 976e605e dxgkrnl!TdrUpdateDbgReport+0x93 [d:\blue_gdr\windows\core\dxkernel\dxgkrnl\core\dxgtdr.cxx @ 944]
01 81d9acfc 976ddead dxgkrnl!TdrCollectDbgInfoStage2+0x195 [d:\blue_gdr\windows\core\dxkernel\dxgkrnl\core\dxgtdr.cxx @ 1759]
02 81d9ad24 976e664f dxgkrnl!DXGADAPTER::Reset+0x23f [d:\blue_gdr\windows\core\dxkernel\dxgkrnl\core\adapter.cxx @ 14972]
03 81d9ad3c 977be9e0 dxgkrnl!TdrResetFromTimeout+0x16 [d:\blue_gdr\windows\core\dxkernel\dxgkrnl\core\dxgtdr.cxx @ 2465]
04 81d9ad50 977b7518 dxgmms1!VidSchiRecoverFromTDR+0x13 [d:\blue_gdr\windows\core\dxkernel\dxgkrnl\dxgmms1\vidsch\vidscher.cxx @ 1018]
05 (Inline) -------- dxgmms1!VidSchiRun_PriorityTable+0xfa71
06 81d9ad70 812c01d4 dxgmms1!VidSchiWorkerThread+0xfaf2 [d:\blue_gdr\windows\core\dxkernel\dxgkrnl\dxgmms1\vidsch\vidschi.cxx @ 424]
07 81d9adb0 81325fb1 nt!PspSystemThreadStartup+0x58 [d:\blue_gdr\minkernel\ntos\ps\psexec.c @ 5884]
08 81d9adbc 00000000 nt!KiThreadStartup+0x15 [d:\blue_gdr\minkernel\ntos\ke\i386\threadbg.asm @ 81]
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

 

 




