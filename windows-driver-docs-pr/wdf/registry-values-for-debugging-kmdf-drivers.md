---
title: WDF ドライバー (KMDF および UMDF) をデバッグするためのレジストリ値
description: このトピックでは、Windows Driver Framework (WDF) ドライバーで設定できるレジストリ値について説明します。 これは、UMDF version 2 以降のカーネルモードドライバーフレームワーク (KMDF) ドライバーとユーザーモードドライバーフレームワーク (UMDF) ドライバーに適用されます。
ms.assetid: d54bdc6c-b409-4973-9b29-16967a4d83fb
keywords:
- ドライバーのデバッグ WDK KMDF、レジストリ値
- デバッグドライバーのレジストリ値 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c58dec7f6527beb033a7ccb929a835f4abc0b369
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842216"
---
# <a name="registry-values-for-debugging-wdf-drivers-kmdf-and-umdf"></a>WDF ドライバー (KMDF および UMDF) をデバッグするためのレジストリ値


この記事では、Windows Driver Framework (WDF) ドライバーで設定できるレジストリ値について説明します。 これは、UMDF version 2 以降のカーネルモードドライバーフレームワーク (KMDF) ドライバーとユーザーモードドライバーフレームワーク (UMDF) ドライバーに適用されます。

次のレジストリ値は、ドライバーの**パラメーター\\Wdf**サブキーの下に存在できます。 KMDF ドライバーの場合、このサブキーは、ドライバーのサービス名の下にある**HKEY\_LOCAL\_MACHINE\\System\\CurrentControlSet\\Services**にあります。 UMDF ドライバーの場合、このサブキーは、 **HKLM\\SOFTWARE\\Microsoft\\WINDOWS NT\\CurrentVersion\\WUDF\\Services**のドライバーのサービス名の下にあります。 ドライバーのファイル名とサービス名が異なる場合でも、ドライバーのサブキーは常にドライバーのサービス名を使用します。

<a href="" id="verifieron-----------------reg-dword-"></a>**VerifierOn** (**REG\_DWORD**)  
[Kmdf 検証](using-kmdf-verifier.md)を有効にするには、0以外の値を設定します。これにより、ドライバーの状態と関数のパラメーターが広範囲に検証されます。 ドライバーを開発する場合は、 **VerifierOn**と**dbgbreakonerror**を設定する必要があります。 次の例のように、 [Addservice ディレクティブ](../install/inf-addservice-directive.md)と[AddReg ディレクティブ](../install/inf-addreg-directive.md)を使用して、INF ファイルの Services セクションでこれらの値を設定します。

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

<a href="" id="verifyon-----------------reg-dword-"></a>**Verifyon** (**REG\_DWORD**)  
を0以外の値に設定すると、Wdfverify に定義されている[**Wdfverify**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfverify)マクロが有効になります。または、0に設定すると、マクロが無効になります。 VerifierOn 値が設定されている場合、VerifyOn は暗黙的に0以外に設定されます。

<a href="" id="dbgbreakonerror--reg-dword-"></a>**Dbgbreakonerror** (**REG\_DWORD**)  
0以外の値に設定すると、ドライバーが[**WdfVerifierDbgBreakPoint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfverifier/nf-wdfverifier-wdfverifierdbgbreakpoint)を呼び出したときに、フレームワークがデバッガーに分割されます。 ( **VerifierOn**値が設定されている場合、 **dbgbreakonerror**の値が存在しない場合でも、フレームワークはデバッガーに中断します。)上記のコード例を参照してください。

<a href="" id="dbgwaitforsignaltimeoutinsec--reg-dword-"></a>**DbgWaitForSignalTimeoutInSec** (**REG\_DWORD**)  
Windows 8 以降では、 **VerifierOn**と**dbgbreakonerror**が0以外の値に設定されている場合、ドライバーは**DbgWaitForSignalTimeoutInSec**を設定することによって、デバッガーを中断する既定のタイムアウト期間を変更できます。

この値は、framework バージョン1.11 以降で使用できます。

<a href="" id="verifierallocatefailcount-----------------reg-dword-"></a>**VerifierAllocateFailCount** (**REG\_DWORD**)  
値*n*に設定し、 **VerifierOn**が設定されている場合、 *n 番目*の割り当ての後、ドライバーのオブジェクトにメモリを割り当てようとするたびに、フレームワークは失敗します。 このエラーは、ドライバーによるメモリ不足状態の処理をテストするのに役立ちます。 たとえば、 **VerifierAllocateFailCount**を2に設定した場合、2番目の割り当て後のすべてのメモリ割り当ては失敗します。 **VerifierAllocateFailCount**の既定値は0xffffffff です。 **VerifierAllocateFailCount**を設定したら、それを (DWORD)-1 に設定するか、値を完全に削除することで、無効にすることができます。

検証ツールは、ドライバーによって要求される割り当てと、ドライバーの代わりにフレームワークが要求する割り当ての両方をカウントすることに注意してください。 また、ドライバーに対して発生する可能性がある割り当ての数は、フレームワークの1つのリリースから次のリリースに変更される可能性があります。

<a href="" id="trackhandles--reg-multi-sz-"></a>**Trackhandles** (**REG\_複数\_SZ**)  
フレームワークオブジェクトハンドルの1つ以上の型名のリストに設定され、 **VerifierOn**が設定されている場合、フレームワークは、指定されたハンドル型に一致するすべてのオブジェクトハンドルへの参照を追跡します。 たとえば、ハンドルの種類の一覧が "WDFREQUEST WDFREQUEST" という文字列で構成されている場合、フレームワークはすべての要求オブジェクトとキューオブジェクトへの参照を追跡します。 リストにアスタリスク ("\*") が含まれている場合、フレームワークはすべてのオブジェクトハンドルを追跡します。

<a href="" id="verboseon-----------------reg-dword-"></a>**VerboseOn** (**REG\_DWORD**)  
0以外の値に設定されている場合、フレームワークの[イベントロガー](using-the-framework-s-event-logger.md)は、ドライバーのデバッグに役立つ追加情報を記録します。たとえば、内部コードパスにエントリを挿入したり、内部コードパスから終了したりすることができます。 この値は、ドライバーの開発中にのみ設定する必要があります。 上記のコード例を参照してください。

<a href="" id="logpages--reg-dword-"></a>**Logpages** (**REG\_DWORD**)  
フレームワークによってイベントロガーに割り当てられるメモリページの数をに設定します。 値が定義されていない場合、フレームワークは1ページの既定値を使用します。 設定できる最大値は、4 kb サイズのメモリページ (x86 および amd64 プロセッサ) を搭載したコンピューターの場合は16、8 kb サイズのメモリページ (ia64 プロセッサ) を搭載しているコンピューターの場合は8です。 (大量のページが指定されている場合、オペレーティングシステムでは、ログの内容がクラッシュダンプファイルに書き込まれない可能性があります)。次のように、 [Addservice ディレクティブ](../install/inf-addservice-directive.md)と[AddReg ディレクティブ](../install/inf-addreg-directive.md)を使用して、この値を INF ファイルに設定します。

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

<a href="" id="forcelogsinminidump--reg-dword-"></a>**Forcelogsinminidump ダンプ**(**REG\_DWORD**)  
を0以外の値に設定すると、フレームワークによってイベントロガーの情報がクラッシュダンプファイルに含まれます。

<a href="" id="tracedelaytime--reg-dword-"></a>**Tracedelaytime** (**REG\_DWORD**)  
Microsoft Windows 2000 のみの場合は、を0以外の値に設定して、 [WPP ソフトウェアトレース](https://docs.microsoft.com/windows-hardware/drivers/devtest/wpp-software-tracing)の初期化中に遅延を発生させることができます。 値はミリ秒単位で指定し、有効な値は 1000 (1 秒) です。 この遅延がなければ、WPP トレースの最初の部分が失われる可能性があります。

<a href="" id="enhancedverifieroptions-----------------reg-dword-"></a>**EnhancedVerifierOptions** (**REG\_DWORD**)  
この値にはビットマップが含まれています。 各ビットは、ユーザーがビットを設定することによって有効にできる、追加の検証オプションを表します。

*ビット値:*

**0x1**: 設定した場合、検証ツールは、各ドライバーのイベントコールバック関数が次の処理を実行するかどうかを確認します。

-   が呼び出されたときと同じ IRQL でを返します。 値が異なる場合、 [**WDF\_違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0x10d---wdf-violation)バグチェックがエラーコード0xe と共に発生します。

-   戻る前に、によって入力されたすべての[重要な領域](https://docs.microsoft.com/windows-hardware/drivers/kernel/critical-regions-and-guarded-regions)を終了します。 コールバック関数が、入力されたクリティカルな領域内で戻ると、 [**WDF\_違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0x10d---wdf-violation)のバグチェックが0xf ですのエラーコードと共に発生します。

参照: 設定されている場合、およびドライバーで i/o キューの[転送の保証](guaranteeing-forward-progress-of-i-o-operations.md)が有効になっている場合、フレームワークは、キューの i/o 要求ごとにメモリ不足の状況をシミュレート**します。**

**0x20000**: 設定されている場合、およびドライバーで i/o キューの転送の保証が有効になっている場合は、ランダムに選択された i/o 要求に対してメモリ不足の状況がシミュレートされます。

この値は、framework バージョン1.9 以降で使用できます。

<a href="" id="verifydownlevel--reg-dword-"></a>**Verifydownlevel レベル**(**REG\_DWORD**)  
0以外の値に設定されていて、現在のバージョンよりも古いバージョンのフレームワークを使用してドライバーがビルドされている場合、フレームワークの検証ツールには、ドライバーのビルド後に追加されたテストが含まれます。 この値が存在しない場合、または0に設定されている場合、フレームワークの検証ツールには、ドライバーがビルドされたときに存在していたテストのみが含まれます。

たとえば、ドライバーがバージョン1.7 のフレームワークでビルドされ、コンピューターに framework のバージョン1.9 がインストールされている場合、 **Verifydownlevel レベル**を0以外に設定すると、検証ツールのバージョン1.9 に追加されたテストが検証ツールに含まれるようになります。ドライバーの実行時。

この値は、framework バージョン1.9 以降で使用できます。

## <a name="kmdf"></a>KMDF


KMDF ドライバーの場合、次のレジストリ値が**HKLM\\システム\\CurrentControlSet\\Control\\Wdf\\Kmdf\\Diagnostics**レジストリキーの下に存在する可能性があります。 UMDF ドライバーの場合、次のレジストリ値は**HKLM\\システム\\CurrentControlSet\\Control\\Wdf\\UMDF\\Diagnostics**レジストリキーの下に存在することができます。 ドライバーは、オプションの**診断**サブキーを作成する必要がある場合があります。

<a href="" id="dbgprinton--reg-dword-"></a>**Dbgprinton** (**REG\_DWORD**)  
0以外の値に設定されている場合、フレームワークのローダーは、ドライバーを読み込んで、フレームワークライブラリのバージョンにバインドするとき、またはドライバーのアンロード中に、さまざまなメッセージをカーネルデバッガーに送信します。

## <a name="umdf"></a>UMDF


また、 **HKLM\\SOFTWARE\\Microsoft\\WINDOWS NT\\CurrentVersion\\WUDF\\Services\\{193a1820-d9ac-4997-8c55-be817523f6aa}** で、次のレジストリ値を設定することもできます。 これらの値は、システム上のすべての UMDF ドライバーに影響します。

<a href="" id="hostprocessdbgbreakonstart--reg-dword-"></a>**Hostprocessdbgbreakonstart** (**REG\_DWORD**)  
秒単位の遅延値を格納します。 指定された遅延期間中、ホストプロセスはユーザーモードのデバッガーを1回だけ検索し、接続されている場合はを中断します。 この期間内にユーザーモードのデバッガーがアタッチされておらず、 **Hostprocessdbgbreakonstart** (0x80000000) の上位ビットが設定されている場合 (0x80000000)、このフレームワークはカーネルモードのデバッガーの中断を1回試みます。 次に、例を示します。

|            |                                                                                                                                                                                                                  |
|------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Value      | 結果                                                                                                                                                                                                           |
| 0x00000004 | フレームワークは、4秒間に1回、ユーザーモードのデバッガーへの接続を試みます。 このフレームワークは、カーネルモードのデバッガーへの接続を試行しません。                                                       |
| 0x80000000 です | フレームワークは、ユーザーモードのデバッガーへの接続を1回試行します。 ユーザーモードのデバッガーがアタッチされていない場合、フレームワークはカーネルモードのデバッガーに接続しようとします。                                |
| 0x80000004 | フレームワークは、4秒間に1回、ユーザーモードのデバッガーへの接続を試みます。 ユーザーモードのデバッガーが4秒以内にアタッチされていない場合、フレームワークはカーネルモードのデバッガーに接続しようとします。 |

 

<a href="" id="hostprocessdbgbreakondriverload--reg-dword-"></a>**Hostprocessdbgbreakondriverload** (**REG\_DWORD**)  
秒単位の遅延値を格納します。 ドライバーが読み込まれてから、指定した秒数が経過するまで、WUDFHost が発生します。 **Hostprocessdbgbreakondriverload**の動作は、 **Hostprocessdbgbreakonstart**に記述されているものと同じです。

**Hostprocessdbgbreakonstart**または**Hostprocessdbgbreakondriverload**を指定すると、フレームワークによって他の UMDF タイムアウト (プラグアンドプレイ操作など) が無効になります。 これは、ドライバーで過剰なタイムアウトが発生した場合に、これらの値を使用すると、ドライバーによってターゲット上で致命的なクラッシュが発生する可能性があることを意味します。

これらのレジストリ値は、WDK に含まれている WDF Verifier ツール (WdfVerifier) を使用して設定することもできます。 このツールと UMDF ドライバーの使用の詳細については、「 [WDF verifier を使用した Umdf 検証機能の設定の管理](https://docs.microsoft.com/windows-hardware/drivers/devtest/global-wdf-settings-tab)」を参照してください。

これらの追加の値は、 **HKLM\\ソフトウェア\\Microsoft\\WINDOWS NT\\CurrentVersion\\WUDF\\DebugMode**にあります。

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
<td align="left"><p>デバッグモードを有効にします。 この設定は、「 <a href="using-device-pooling-in-umdf-drivers.md" data-raw-source="[Using Device Pooling in UMDF Drivers](using-device-pooling-in-umdf-drivers.md)">UMDF ドライバーでのデバイスプールの使用</a>」で説明されている自動再起動機能を無効にします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x02</p></td>
<td align="left"><p>デバイスプーリングを無効にします。 デバイスプールの詳細については、「 <a href="using-device-pooling-in-umdf-drivers.md" data-raw-source="[Using Device Pooling in UMDF Drivers](using-device-pooling-in-umdf-drivers.md)">UMDF ドライバーでのデバイスプールの使用</a>」を参照してください。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x04</p></td>
<td align="left"><p>タイムアウトを無効にします。</p></td>
</tr>
</tbody>
</table>

 

Microsoft Visual Studio で F5 オプションを使用すると、展開されたドライバーに対して3つのフラグがすべて設定されます。

<a href="" id="debugmodebinaries--reg-sz-"></a>**Debugmodebinaries** (**REG\_複数\_SZ**)  
この値は、デバッグモードで読み込まれるドライバーバイナリの名前を指定します。 たとえば、ドライバーバイナリの X .DLL、.dll、および Z .DLL のデバッグモードを有効にするには、この値を「 *x .dll\\0Y」に設定します。DLL\\0Z。DLL\\0\\0*です。

また、 **HKLM\\ソフトウェア\\Microsoft\\WINDOWS NT\\CurrentVersion\\WUDF**で次の値を設定することもできます。

<a href="" id="hostfailkddebugbreak--reg-dword-"></a>**HostFailKdDebugBreak** (**REG\_DWORD**)  
この値がゼロ以外で、カーネルデバッガーがコンピューターに接続されている場合、リフレクタはホストプロセスを終了する前にカーネルデバッガーに中断します。 **HostFailKdDebugBreak**は、Windows 7 以前のオペレーティングシステムでは既定で無効になっています。 Windows 8 以降では、 **HostFailKdDebugBreak**は既定で有効になっています。

リフレクターは、ホストプロセスが予期せず終了した場合 (たとえば、非 UMDF コンポーネントまたはハンドルされない例外が原因で)、カーネルデバッガーにも中断します。 終了しようとしているホストプロセスに複数のデバイススタックがプールされている場合、リフレクタは、ホストプロセスで読み込まれたデバイススタックごとに1回、デバッガーに複数回中断します。

UMDF レジストリ値の変更を有効にするには、コンピューターを再起動する必要があります。

 

 





