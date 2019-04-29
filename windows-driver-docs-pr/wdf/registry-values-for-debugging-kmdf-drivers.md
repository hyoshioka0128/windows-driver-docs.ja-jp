---
title: WDF ドライバー (KMDF および UMDF) をデバッグするためのレジストリ値
description: このトピックでは、Windows Driver Frameworks (WDF) ドライバーを設定できるレジストリ値について説明します。 カーネル モード ドライバー フレームワーク (KMDF) ドライバーおよび UMDF バージョン 2 で始まるユーザー モード ドライバー フレームワーク (UMDF) ドライバーに適用されます。
ms.assetid: d54bdc6c-b409-4973-9b29-16967a4d83fb
keywords:
- ドライバー WDK KMDF、レジストリ値のデバッグ
- WDK KMDF ドライバーをデバッグするためのレジストリ値
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 490cfdc7456c00562bbc3105e595e2c3b852c675
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390036"
---
# <a name="registry-values-for-debugging-wdf-drivers-kmdf-and-umdf"></a>WDF ドライバー (KMDF および UMDF) をデバッグするためのレジストリ値


この記事では、Windows Driver Frameworks (WDF) ドライバーを設定できるレジストリ値について説明します。 カーネル モード ドライバー フレームワーク (KMDF) ドライバーおよび UMDF バージョン 2 で始まるユーザー モード ドライバー フレームワーク (UMDF) ドライバーに適用されます。

ドライバーの下に次のレジストリ値が存在できます**パラメーター\\Wdf**サブキー。 KMDF ドライバーでは、このサブキーにある**HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\サービス**ドライバーのサービス名の下。 UMDF ドライバーの場合、このサブキーが内にある**HKLM\\ソフトウェア\\Microsoft\\Windows NT\\CurrentVersion\\WUDF\\サービス**下で、ドライバーのサービスの名前。 ドライバーのサブキーは、ドライバーのバイナリ ファイルのファイル名は、サービス名と異なる場合でも常に、ドライバーのサービスの名前を使用します。

<a href="" id="verifieron-----------------reg-dword-"></a>**VerifierOn** (**REG\_DWORD**)  
0 以外の値に設定を有効に[KMDF Verifier](using-kmdf-verifier.md)、広範なドライバーの状態と関数のパラメーターを検証します。 設定する必要があります**VerifierOn**と**DbgBreakOnError**ドライバーを開発するとき。 使用して、 [AddService ディレクティブ](../install/inf-addservice-directive.md)と[AddReg ディレクティブ](../install/inf-addreg-directive.md)など、INF ファイルの Services セクションでこれらの値を設定します。

```
[xxx_Inst.NT.Services]
AddService = xxx,%SPSVCINST_ASSOCSERVICE%,xxx_Service_Inst

[xxx_Service_Inst]
ServiceType   = %SERVICE_KERNEL_DRIVER%
StartType     = %SERVICE_BOOT_START%
ErrorControl  = %SERVICE_ERROR_NORMAL%
LoadOrderGroup = "Base"
ServiceBinary = %12%\xxx.sys
AddReg         = KMDFVerifierAddReg

[KMDFVerifierAddReg]
HKR, Parameters\Wdf,VerifierOn,0x00010001,1
HKR, Parameters\Wdf,VerboseOn,0x00010001,1
HKR, Parameters\Wdf,DbgBreakOnError,0x00010001,1
```

<a href="" id="verifyon-----------------reg-dword-"></a>**VerifyOn** (**REG\_DWORD**)  
0 以外の値に設定を有効に、 [ **WDFVERIFY** ](https://msdn.microsoft.com/library/windows/hardware/ff551167)マクロですが、Wdfassert.h で定義されているか、マクロを無効にする場合は 0 に設定します。 VerifierOn 値が設定されている場合 VerifyOn は暗黙的 0 以外に設定します。

<a href="" id="dbgbreakonerror--reg-dword-"></a>**DbgBreakOnError** (**REG\_DWORD**)  
かどうか 0 以外の値に設定すると、フレームワーク デバッガーを中断するドライバーを呼び出すと[ **WdfVerifierDbgBreakPoint**](https://msdn.microsoft.com/library/windows/hardware/ff551164)します。 (場合、 **VerifierOn**値の設定、フレームワークがあっても、デバッガーに分割、 **DbgBreakOnError**値が存在しません)。上記のコード例を参照してください。

<a href="" id="dbgwaitforsignaltimeoutinsec--reg-dword-"></a>**DbgWaitForSignalTimeoutInSec** (**REG\_DWORD**)  
以降では、Windows 8、ときに**VerifierOn**と**DbgBreakOnError**設定は、ドライバー、0 以外の値を設定して、デバッガーの中断の既定のタイムアウト期間を変更できます**DbgWaitForSignalTimeoutInSec**します。

この値は、以降のバージョン 1.11 のフレームワークで使用できます。

<a href="" id="verifierallocatefailcount-----------------reg-dword-"></a>**VerifierAllocateFailCount** (**REG\_DWORD**)  
場合の値に設定*n*、場合**VerifierOn**が設定された場合、フレームワークには、後で、ドライバーのオブジェクトのメモリを割り当てるすべての試行が失敗した、 *n 番目*割り当て。 このエラーでは、メモリ不足の状態のドライバーの処理をテストできます。 たとえば、設定した場合**VerifierAllocateFailCount** 2、2 つ目の割り当て後にすべてのメモリ割り当ては失敗します。 既定値**VerifierAllocateFailCount** 0 xffffffff です。 設定後**VerifierAllocateFailCount**、(DWORD)-1 に設定することで無効にできますまたは値を完全に削除します。

割り当てには、ドライバーを要求して、フレームワークは、ドライバーに代わって要求を割り当て、検証機能がカウントされるに注意してください。 また、framework の 1 つのリリースから次に、ドライバーで発生する可能性の割り当ての数が変更できることに注意してください。

<a href="" id="trackhandles--reg-multi-sz-"></a>**TrackHandles** (**REG\_マルチ\_SZ**)  
場合、framework のオブジェクトのハンドルの 1 つまたは複数の型名の一覧に設定されて場合**VerifierOn**が設定された場合、フレームワークは、指定したハンドル型に一致するすべてのオブジェクト ハンドルへの参照を追跡します。 たとえば、ハンドルの種類の一覧は、"WDFREQUEST WDFQUEUE"文字列で構成され、フレームワークはすべての要求オブジェクトとキュー オブジェクトへの参照を追跡します。 一覧には、アスタリスクが含まれている場合 ("\*")、フレームワークは、すべてのオブジェクト ハンドルを追跡します。

<a href="" id="verboseon-----------------reg-dword-"></a>**VerboseOn** (**REG\_DWORD**)  
場合に 0 以外の値、フレームワークの設定[イベント ロガー](using-the-framework-s-event-logger.md)へのエントリまたは内部のコード パスからの終了など、ドライバーをデバッグするのに役立つ追加情報を記録します。 ドライバーの開発中にのみ、この値を設定する必要があります。 上記のコード例を参照してください。

<a href="" id="logpages--reg-dword-"></a>**ログ ページ**(**REG\_DWORD**)  
フレームワークは、そのイベント ロガーに割り当てるメモリ ページの数に設定します。 値が定義されていない場合、フレームワークは、1 つのページの既定値を使用します。 設定できる最大値は、16 (x86 および amd64 プロセッサ) の 4 キロバイト サイズのメモリ ページがあるコンピューター、および 8 キロバイト サイズのメモリのページ (ia64 プロセッサ) があるコンピューターの 8 には。 (オペレーティング システム可能性がありますいない書き込みページの数が多い場合、クラッシュ ダンプ ファイルにログの内容を指定)使用して、 [AddService ディレクティブ](../install/inf-addservice-directive.md)と[AddReg ディレクティブ](../install/inf-addreg-directive.md)INF ファイルで次のようにこの値を設定します。

```
[xxx.NT.Services]
AddService = yyy, 2, zzz.AddService

[zzz.AddService]
DisplayName   = %aaa\bbb%
ServiceType   = 1
StartType     = 3
ErrorControl  = 1
ServiceBinary = %12%\ddd.SYS
AddReg         = eee.AddReg

[eee.AddReg]
HKR, Parameters\Wdf, LogPages,   0x00010001, 3 ; KMDF IFR size
```

<a href="" id="forcelogsinminidump--reg-dword-"></a>**ForceLogsInMiniDump** (**REG\_DWORD**)  
発生するクラッシュ ダンプ ファイルにそのイベント ロガーからの情報を含めるために、フレームワークに 0 以外の値に設定します。

<a href="" id="tracedelaytime--reg-dword-"></a>**TraceDelayTime** (**REG\_DWORD**)  
Microsoft Windows 2000 はのみ、0 以外の値の初期化中に遅延を導入するセットの[WPP ソフトウェア トレース](https://msdn.microsoft.com/library/windows/hardware/ff556204)します。 値がミリ秒単位で指定してに有効な値は 1000 (1 秒)。 この待機時間、WPP トレースの最初の部分が欠落する可能性があります。

<a href="" id="enhancedverifieroptions-----------------reg-dword-"></a>**EnhancedVerifierOptions** (**REG\_DWORD**)  
この値には、ビットマップが含まれています。 各ビットは、ビットを設定してユーザーが可能にする追加の検証オプションを表します。

*ビット値。*

**0x1**:設定すると、検証チェックのドライバーのイベントのコールバック関数は次の処理かどうか。

-   呼び出された同じ IRQL で返します。 値が異なる場合、 [ **WDF\_違反**](https://msdn.microsoft.com/library/windows/hardware/ff557235) 0xE のエラー コードでのバグ チェックが発生します。

-   、戻る前にすべての操作を終了する[クリティカル領域](https://msdn.microsoft.com/library/windows/hardware/ff542925)それが入力します。 コールバック関数がクリティカル領域内で入力すると、その it を返す場合、 [ **WDF\_違反**](https://msdn.microsoft.com/library/windows/hardware/ff557235)バグ チェックがエラー コード 0 xf で発生します。

**0x10000**:場合設定すると、ドライバーが有効にした場合と[進行を保証](guaranteeing-forward-progress-of-i-o-operations.md)の I/O キューでは、フレームワークは各キューの I/O 要求のメモリ不足の状況をシミュレートします。

**0x20000**:場合設定すると、フレームワークがいくつかランダムに選択された I/O 要求のメモリ不足状況をシミュレートして、ドライバーが I/O キューの保証された処理を進行を有効な場合があるとします。

この値は、以降のバージョン 1.9 のフレームワークで使用できます。

<a href="" id="verifydownlevel--reg-dword-"></a>**VerifyDownLevel** (**REG\_DWORD**)  
場合は 0 以外の値に設定され、フレームワークの検証にドライバーがビルドされた後に追加されたテストが含まれています、ドライバーが現在のバージョンより古いフレームワークのバージョンでビルドされている場合。 この値が存在しないか、0 に設定されているの場合、フレームワークの検証には、ドライバーのビルド時に存在していたテストのみが含まれます。

たとえばには、ドライバーは、framework の version 1.7 で作成した場合、およびフレームワークのバージョン 1.9 がコンピューターにインストールされている場合は、設定**VerifyDownLevel**に 0 以外の場合と、検証機能に追加されたテストを含めるドライバーの実行時に検証ツールのバージョン 1.9 にします。

この値は、以降のバージョン 1.9 のフレームワークで使用できます。

## <a name="kmdf"></a>KMDF


KMDF ドライバーでは、次のレジストリ値は下に存在できる、 **HKLM\\システム\\CurrentControlSet\\コントロール\\Wdf\\Kmdf\\診断**レジストリ キー。 UMDF ドライバーでは、次のレジストリ値が存在できる、 **HKLM\\システム\\CurrentControlSet\\コントロール\\Wdf\\Umdf\\診断**レジストリ キー。 ドライバーは、省略可能なを作成する必要があります**診断**サブキー。

<a href="" id="dbgprinton--reg-dword-"></a>**DbgPrintOn** (**REG\_DWORD**)  
かどうかは 0 以外の値に設定すると、フレームワークのローダーを送信メッセージのさまざまなカーネル デバッガーに、ドライバーの読み込みされ、framework ライブラリのバージョンへのバインド時、あるいは、ドライバーをアンロードしています。

## <a name="umdf"></a>UMDF


次のレジストリ値を設定することもできます**HKLM\\ソフトウェア\\Microsoft\\Windows NT\\CurrentVersion\\WUDF\\サービス\\{。193a1820-d9ac-4997-8c55-be817523f6aa}** します。 これらの値では、システム上のすべての UMDF ドライバーに影響します。

<a href="" id="hostprocessdbgbreakonstart--reg-dword-"></a>**HostProcessDbgBreakOnStart** (**REG\_DWORD**)  
秒単位では、遅延の値が含まれています。 指定された遅延の期間中は、ホスト プロセスは、1 秒に 1 回をユーザー モード デバッガーを検索しが接続されている場合中断します。 この期間、高ビット内でユーザー モード デバッガーがアタッチされていない場合**HostProcessDbgBreakOnStart** (0x80000000) が設定されているフレームワークは、カーネル モードのデバッガーを中断する 1 回の試行を使用します。 次に、例を示します。

|            |                                                                                                                                                                                                                  |
|------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Value      | 結果                                                                                                                                                                                                           |
| 0x00000004 | フレームワークは、4 秒の 1 秒に 1 回のユーザー モード デバッガーに接続しようとします。 フレームワークは、決してカーネル モードのデバッガーに接続しようとします。                                                       |
| 0x80000000 | フレームワークは、ユーザー モード デバッガーへの接続に 1 回の試行を使用します。 ユーザー モード デバッガーがアタッチされていない場合、フレームワークは、カーネル モードのデバッガーに接続しようとします。                                |
| 0x80000004 | フレームワークは、4 秒の 1 秒に 1 回のユーザー モード デバッガーに接続しようとします。 4 秒以内に、ユーザー モード デバッガーがアタッチされていません、フレームワークは、カーネル モードのデバッガーに接続しようとします。 |

 

<a href="" id="hostprocessdbgbreakondriverload--reg-dword-"></a>**HostProcessDbgBreakOnDriverLoad** (**REG\_DWORD**)  
秒単位では、遅延の値が含まれています。 指定したドライバーが読み込まれた後の秒数を遅延する WUDFHost をによりします。 動作は、 **HostProcessDbgBreakOnDriverLoad**はそれ以外の場合と同じ**HostProcessDbgBreakOnStart**します。

指定する**HostProcessDbgBreakOnStart**または**HostProcessDbgBreakOnDriverLoad**とその他の UMDF タイムアウト (たとえば、プラグ アンド プレイ操作) を無効にするフレームワークです。 つまりには、ドライバーでは、過剰にタイムアウトが発生する場合は、これらの値を使用して可能性があります、ターゲット上で致命的なクラッシュの原因は、ドライバー。

WDK に含まれている WDF Verifier ツール (WdfVerifier.exe) を使用して、これらのレジストリ値を設定することもできます。 UMDF ドライバーでこのツールの使用方法の詳細については、次を参照してください。 [WDF Verifier による UMDF 検証設定の管理](https://msdn.microsoft.com/library/windows/hardware/ff548422)します。

次の値にある**HKLM\\ソフトウェア\\Microsoft\\Windows NT\\CurrentVersion\\WUDF\\DebugMode**:

<a href="" id="debugmodeflags--reg-dword-"></a>**DebugModeFlags** (**REG\_DWORD**)  
<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Value</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x01</p></td>
<td align="left"><p>デバッグ モードを有効にします。 この設定で説明されている自動再起動機能をオフに<a href="using-device-pooling-in-umdf-drivers.md" data-raw-source="[Using Device Pooling in UMDF Drivers](using-device-pooling-in-umdf-drivers.md)">デバイスの UMDF ドライバーでプールを使用して</a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x02</p></td>
<td align="left"><p>デバイスのプールを無効にします。 デバイスのプールに関する詳細については、次を参照してください。<a href="using-device-pooling-in-umdf-drivers.md" data-raw-source="[Using Device Pooling in UMDF Drivers](using-device-pooling-in-umdf-drivers.md)">デバイスの UMDF ドライバーでプールを使用して</a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x04</p></td>
<td align="left"><p>タイムアウトを無効にします。</p></td>
</tr>
</tbody>
</table>

 

Microsoft Visual Studio で f5 キーを押してオプションを使用すると、展開済みのドライバーの 3 つすべてのフラグが設定されます。

<a href="" id="debugmodebinaries--reg-sz-"></a>**DebugModeBinaries** (**REG\_マルチ\_SZ**)  
この値は、デバッグ モードで読み込まれるドライバー バイナリの名前を指定します。 X.DLL、Y.DLL および Z.DLL のドライバー バイナリのデバッグ モードを有効にするなど、この値は設定されます*X.DLL\\0 Y です。DLL\\0Z.DLL\\0\\0*します。

次の値を設定することもできます**HKLM\\ソフトウェア\\Microsoft\\Windows NT\\CurrentVersion\\WUDF**:。

<a href="" id="hostfailkddebugbreak--reg-dword-"></a>**HostFailKdDebugBreak** (**REG\_DWORD**)  
この値は 0 以外、カーネル デバッガーがマシンに接続されている場合は、reflector は、ホスト プロセスを終了する前にカーネル デバッガーを中断します。 **HostFailKdDebugBreak**は Windows 7 と以前のオペレーティング システムで既定で無効になります。 Windows 8 で始まる**HostFailKdDebugBreak**既定で有効です。

Reflector は、ホスト プロセス (例: 非 UMDF コンポーネントまたはハンドルされない例外が原因) の予期しない終了がある場合、カーネル デバッガーを中断もします。 プールが終了しているホスト プロセスで複数のデバイス スタックがある場合、reflector デバッガーを中断複数回、1 回、ホスト プロセスに読み込まれている各デバイス スタック。

UMDF レジストリ値を有効にする変更は、コンピューターを再起動する必要があります。

 

 





