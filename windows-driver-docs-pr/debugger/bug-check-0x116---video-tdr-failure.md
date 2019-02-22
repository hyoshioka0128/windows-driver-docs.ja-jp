---
title: バグ チェック 0x116 VIDEO_TDR_FAILURE
description: VIDEO_TDR_FAILURE のバグ チェックでは、0x00000116 の値を持ちます。 これは、ディスプレイ ドライバーをリセットするか、タイムアウトから復旧試行が失敗したことを示します。
ms.assetid: 06fe312a-e2d3-479f-b0fb-06c0ac79be32
keywords:
- バグ チェック 0x116 VIDEO_TDR_FAILURE
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
ms.openlocfilehash: 33cde2e3f298313c96183ad19dbf43c8a7ee4cfe
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558011"
---
# <a name="bug-check-0x116-videotdrfailure"></a>バグ チェック 0x116 の。ビデオ\_TDR\_エラー


ビデオ\_TDR\_エラーのバグ チェックが 0x00000116 の値を持ちます。 これは、ディスプレイ ドライバーをリセットするか、タイムアウトから復旧試行が失敗したことを示します。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

## <a name="videotdrfailure-parameters"></a>ビデオ\_TDR\_エラー パラメーター


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
<td align="left"><p>内部 TDR リカバリ コンテキストで使用可能な場合へのポインター。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>担当のデバイス ドライバー モジュール (所有者タグなど) へのポインター。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>使用可能な場合の最後の失敗した操作のエラー コード。</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>内部のコンテキスト依存データは、使用可能な場合。</p></td>
</tr>
</tbody>
</table>



<a name="cause"></a>原因
-----

一般的な安定性問題をグラフィックスでは、システムが完全にフリーズやハングした、エンドユーザーのコマンドまたは操作の処理中に表示されたらに発生します。 通常、GPU は、ゲーム プレイ中に、負荷の高いグラフィックスの操作を通常処理でビジー状態です。 画面の更新が発生しないと、ユーザーは、システムが固定されていることを想定します。 ユーザーは、通常は数秒待ってからして、電源ボタンを押して、システムを再起動します。 Windows は、この問題のある状況がハングし、応答性の高いデスクトップを動的に回復を検出しようとします。

この検出と回復のプロセスは、タイムアウト検出と復旧 (TDR) と呼びます。 既定のタイムアウトは 2 秒です。 ビデオ カードの TDR プロセスで、オペレーティング システムの GPU のスケジューラを呼び出すディスプレイ ミニポート ドライバーの[ *DxgkDdiResetFromTimeout* ](https://msdn.microsoft.com/library/windows/hardware/ff559815)ドライバーを再初期化し、GPU をリセットする関数。

このプロセス中には、オペレーティング システムは、ドライバーがハードウェアまたはメモリにアクセスしないように指示し、現在実行中のスレッドが完了する短い形式の時刻を示します。 スレッドが、タイムアウト以内に完了しなかったかどうかは、0x116 によるチェックのシステムのバグ ビデオ\_TDR\_失敗します。 詳細については、次を参照してください。[スレッドの同期と TDR](https://msdn.microsoft.com/library/windows/hardware/ff570082)します。

ビデオをチェックできますもバグのシステム\_TDR\_エラー TDR イベントの数が短時間で発生した場合既定で 5 つを超える TDRs 1 分以内にします。

回復プロセスが成功した場合、メッセージが表示されます、ことを示す、「ディスプレイ ドライバー応答を停止したし、が回復します」。

詳細については、タイムアウト検出と復旧 (TDR) を参照してください[TDR レジストリ キー](https://msdn.microsoft.com/library/windows/hardware/ff569918)と[Windows 8 での TDR 変更](https://msdn.microsoft.com/library/windows/hardware/jj676805)に存在する[Windows Display Driver Model (のデバッグのヒントWDDM)](https://msdn.microsoft.com/library/windows/hardware/ff551790)します。

<a name="resolution"></a>解決方法
----------

GPU には、モニターにグラフィックスを表示する許可より多くの時間がかかっています。 この動作は、次の理由の 1 つ以上発生します。

-   TDR の処理を正しくサポートできるように、ディスプレイ ドライバー、最新の更新プログラムをインストールする必要があります。
-   ハードウェアに関する問題影響を与える、適切に動作するビデオ カードの機能を含みます。
    -   マザーボードなどの集中的なコンポーネント
    -   不正なコンポーネントの互換性と設定 (特にメモリ構成とタイミング)
    -   不足しているシステムの冷却
    -   不足しているシステムの電源
    -   欠陥のある部分 (メモリ モジュール、マザーボードなど。)
-   視覚効果、またはバック グラウンドで実行されているプログラムが多すぎる遅らせることができる PC できるように、必要に応じて、ビデオ カードが応答しないことができます。

[ **! 分析**](-analyze.md)バグ チェックに関する情報を表示拡張機能をデバッグおよび根本原因を突き止めるには非常に役に立ちます。

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

エラーが発生したモジュールの名前になりますも表示されます。

```dbgcmd
MODULE_NAME: nvlddmkm

IMAGE_NAME:  nvlddmkm.sys
```

使用することができます、 [ **lm (読み込まれたモジュールの一覧)**](lm--list-loaded-modules-.md)タイムスタンプを含む、エラーが発生したドライバーに関する情報を表示するコマンド。

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

パラメーター 1 が、TDR へのポインターを含む\_RECOVERY\_コンテキスト。 ように、!、出力を分析して、関連付けられているコードのシンボルがあれば、このデータを表示する dt コマンドを使用することができます。

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

2 番目のパラメーターは、担当するデバイス ドライバー モジュール (所有者タグなど) に、ポインターを格納します。

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

使用して、スタック トレースを調べることができます、 [ **k、kb、kc、kd、kp、kP、kv (Display Stack Backtrace)** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)コマンド。

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

この停止コードに至るまで、コードにブレークポイントを設定したり、停止コードを一貫して再現できる場合、シングル ステップ転送エラーが発生したコードをしようし、することができますも。

詳細については、以下のトピックを参照してください。

[クラッシュ ダンプ分析の Windows デバッガー (WinDbg) の使用方法](crash-dump-files.md)

Windows デバッガーを使用してこの問題に取り組むを備えていない場合は、基本的なトラブルシューティングの手法を使用できます。

-   デバイスまたはこのバグ チェックが原因となっているドライバーの特定に役立つ可能性がある追加のエラー メッセージをイベント ビューアーのシステム ログを確認します。

-   バグ チェックのメッセージでドライバーが特定された場合は、そのドライバーを無効にするか、ドライバーの更新状況を製造元に確認します。

-   すべてのグラフィック関連の DirectX や OpenGL などのソフトウェアが最新の状態、および (ゲーム) など、あらゆるグラフィックス処理を要するアプリケーションの修正プログラムが完全に適用することを確認します。
-   インストールされている新しいハードウェアが Windows のインストールされているバージョンと互換性があることを確認します。 たとえばに必要なハードウェアに関する情報を取得できます[Windows 10 の仕様](https://www.microsoft.com/windows/windows-10-specifications)します。

-   **セーフ モードを使用します。**

    この問題を特定しやすくセーフ モードを使用してください。 セーフ モードを使用して、Windows の起動中に、最低限必要なドライバーとシステム サービスのみを読み込みます。 セーフ モードを入力するを使用して**更新とセキュリティ**で設定します。 選択**Recovery**-&gt;**スタートアップを高度な**メンテナンス モードで起動します。 結果として得られるメニューでは、次のように選択します**トラブルシューティング**- &gt; **オプションの高度な** - &gt; **スタートアップ設定**。 - &gt; **再起動**します。 Windows を再起動した後、**スタートアップ設定**画面で、セーフ モードで起動するには、4、5 または 6 のオプションを選択します。

    ブート、f8 キーなどのファンクション キーを押して、セーフ モードを利用できます。 特定のスタートアップ オプションの製造元から情報を参照してください。

-   メモリをテストする、Windows メモリ診断ツールを実行します。 コントロール パネルの検索ボックスには、メモリを入力し、クリックして **、コンピューターのメモリの問題を診断**します。テストの実行後は、イベント ビューアーを使用して、システム ログで結果を表示します。 探して、 *MemoryDiagnostics 結果*結果を表示するエントリ。

-   システム製造元から提供されたハードウェア診断を実行して確認することができます。

-   その他の一般的なトラブルシューティング情報を参照してください。 [**青い画面データ**](blue-screen-data.md)します。

<a name="remarks"></a>注釈
-------

**ハードウェア認定要件**

TDR を実装するときにハードウェア デバイスが満たす必要のある要件については、ドキュメントを参照して、WHCK の*Device.Graphics.TDRResiliency*します。








