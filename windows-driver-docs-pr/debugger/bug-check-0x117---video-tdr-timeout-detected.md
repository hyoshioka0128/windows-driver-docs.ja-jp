---
title: バグ チェック 0x117 VIDEO_TDR_TIMEOUT_DETECTED
description: VIDEO_TDR_TIMEOUT_DETECTED のバグ チェックでは、0x00000117 の値を持ちます。 これは、ディスプレイ ドライバーが適切な時間内に応答が失敗したことを示します。
ms.assetid: 70e24a97-f695-4d35-b52f-69dfddecd9b5
keywords:
- バグ チェック 0x117 VIDEO_TDR_TIMEOUT_DETECTED
- VIDEO_TDR_TIMEOUT_DETECTED
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- VIDEO_TDR_TIMEOUT_DETECTED
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5da4bdadf296005f496d0957899df646e755e489
ms.sourcegitcommit: fb8b1d2e18dd727e8a479b04c9e6051e7e9fa484
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/18/2019
ms.locfileid: "59238537"
---
# <a name="bug-check-0x117-videotdrtimeoutdetected"></a>バグ チェック 0x117:ビデオ\_TDR\_タイムアウト\_検出


ビデオ\_TDR\_タイムアウト\_検出されたバグ チェックが 0x00000117 の値を持ちます。 これは、ディスプレイ ドライバーが適切な時間内に応答が失敗したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="videotdrtimeoutdetected-parameters"></a>ビデオ\_TDR\_タイムアウト\_検出パラメーター


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
<td align="left"><p>セカンダリ ドライバー固有のバケット キー。</p></td>
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

[ **! 分析**](-analyze.md)バグ チェックに関する情報を表示拡張機能をデバッグおよび根本原因を突き止めるに役に立ちます。

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

エラーが発生したモジュールの名前になりますも表示されます。

```dbgcmd
MODULE_NAME: atikmpag

IMAGE_NAME:  atikmpag.sys
```

Lmv コマンドを使用するには、タイムスタンプを含む、エラーが発生したドライバーに関する情報を表示します。

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

パラメーター 1 が、TDR へのポインターを含む\_RECOVERY\_コンテキスト。

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

2 番目のパラメーターは、担当するデバイス ドライバー モジュール (所有者タグなど) に、ポインターを格納します。

```dbgcmd
BUGCHECK_P2: ffffffff9a02381e
```

使用して、スタック トレースを調べることができます、 [ **k、kb、kc、kd、kp、kP、kv (Display Stack Backtrace)** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)コマンド。

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

 

 




