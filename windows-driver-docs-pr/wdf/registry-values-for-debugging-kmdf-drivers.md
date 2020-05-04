---
title: WDF ドライバー (KMDF および UMDF) をデバッグするためのレジストリ値
description: このトピックでは、Windows Driver Framework (WDF) ドライバーで設定できるレジストリ値について説明します。 これは、UMDF version 2 以降のカーネルモードドライバーフレームワーク (KMDF) ドライバーとユーザーモードドライバーフレームワーク (UMDF) ドライバーに適用されます。
ms.assetid: d54bdc6c-b409-4973-9b29-16967a4d83fb
keywords:
- ドライバーのデバッグ WDK KMDF、レジストリ値
- デバッグドライバーのレジストリ値 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8abcfbb2651934f691055f35a9a3cb6a7e3a2f00
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223088"
---
# <a name="registry-values-for-debugging-wdf-drivers-kmdf-and-umdf"></a>WDF ドライバー (KMDF および UMDF) をデバッグするためのレジストリ値


この記事では、Windows Driver Framework (WDF) ドライバーで設定できるレジストリ値について説明します。 これは、UMDF version 2 以降のカーネルモードドライバーフレームワーク (KMDF) ドライバーとユーザーモードドライバーフレームワーク (UMDF) ドライバーに適用されます。

次のレジストリ値は、ドライバーの**Parameters\\Wdf**サブキーの下に存在できます。 KMDF ドライバーの場合、このサブキーは、ドライバーのサービス名の下にある**HKEY\_LOCAL\_MACHINE\\System\\CurrentControlSet\\Services**にあります。 UMDF ドライバーの場合、このサブキーは、 **HKLM\\SOFTWARE\\Microsoft\\Windows NT\\CurrentVersion\\wudf\\Services**のドライバーのサービス名の下にあります。 ドライバーのファイル名とサービス名が異なる場合でも、ドライバーのサブキーは常にドライバーのサービス名を使用します。

## <a name="verifieron"></a>VerifierOn

*REG\_DWORD*

[Kmdf 検証](using-kmdf-verifier.md)を有効にするには、0以外の値を設定します。これにより、ドライバーの状態と関数のパラメーターが広範囲に検証されます。 ドライバーを開発する場合は、 **VerifierOn**と**dbgbreakonerror**を設定する必要があります。 次の例のように、 [Addservice ディレクティブ](../install/inf-addservice-directive.md)と[AddReg ディレクティブ](../install/inf-addreg-directive.md)を使用して、INF ファイルの Services セクションでこれらの値を設定します。

```inf
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

## <a name="verifyon"></a>VerifyOn

*REG\_DWORD*

を0以外の値に設定すると、Wdfverify に定義されている[**Wdfverify**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfverify)マクロが有効になります。または、0に設定すると、マクロが無効になります。 VerifierOn 値が設定されている場合、VerifyOn は暗黙的に0以外に設定されます。

## <a name="dbgbreakonerror"></a>DbgBreakOnError

*REG\_DWORD*

0以外の値に設定すると、ドライバーが[**WdfVerifierDbgBreakPoint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfverifier/nf-wdfverifier-wdfverifierdbgbreakpoint)を呼び出したときに、フレームワークがデバッガーに分割されます。 ( **VerifierOn**値が設定されている場合、 **dbgbreakonerror**の値が存在しない場合でも、フレームワークはデバッガーに中断します。)上記のコード例を参照してください。

## <a name="dbgwaitforsignaltimeoutinsec"></a>DbgWaitForSignalTimeoutInSec

*REG\_DWORD、framework バージョン1.11 以降*

Windows 8 以降では、 **VerifierOn**と**dbgbreakonerror**が0以外の値に設定されている場合、ドライバーは**DbgWaitForSignalTimeoutInSec**を設定することによって、デバッガーを中断する既定のタイムアウト期間を変更できます。


## <a name="verifierallocatefailcount"></a>VerifierAllocateFailCount

*REG\_DWORD*

値*n*に設定し、 **VerifierOn**が設定されている場合、 *n 番目*の割り当ての後、ドライバーのオブジェクトにメモリを割り当てようとするたびに、フレームワークは失敗します。 このエラーは、ドライバーによるメモリ不足状態の処理をテストするのに役立ちます。 たとえば、 **VerifierAllocateFailCount**を2に設定した場合、2番目の割り当て後のすべてのメモリ割り当ては失敗します。 **VerifierAllocateFailCount**の既定値は0xffffffff です。 **VerifierAllocateFailCount**を設定したら、それを (DWORD)-1 に設定するか、値を完全に削除することで、無効にすることができます。

検証ツールは、ドライバーによって要求される割り当てと、ドライバーの代わりにフレームワークが要求する割り当ての両方をカウントすることに注意してください。 また、ドライバーに対して発生する可能性がある割り当ての数は、フレームワークの1つのリリースから次のリリースに変更される可能性があります。

## <a name="trackhandles"></a>TrackHandles

*REG\_マルチ\_SZ*

フレームワークオブジェクトハンドルの1つ以上の型名のリストに設定され、 **VerifierOn**が設定されている場合、フレームワークは、指定されたハンドル型に一致するすべてのオブジェクトハンドルへの参照を追跡します。 たとえば、ハンドルの種類の一覧が "WDFREQUEST WDFREQUEST" という文字列で構成されている場合、フレームワークはすべての要求オブジェクトとキューオブジェクトへの参照を追跡します。 リストにアスタリスク ("\*") が含まれている場合、フレームワークはすべてのオブジェクトハンドルを追跡します。

## <a name="verboseon"></a>VerboseOn

*REG\_DWORD*

0以外の値に設定されている場合、フレームワークの[イベントロガー](using-the-framework-s-event-logger.md)は、ドライバーのデバッグに役立つ追加情報を記録します。たとえば、内部コードパスにエントリを挿入したり、内部コードパスから終了したりすることができます。 この値は、ドライバーの開発中にのみ設定する必要があります。 上記のコード例を参照してください。

## <a name="logpages"></a>LogPages

*REG\_DWORD*

フレームワークによってイベントロガーに割り当てられるメモリページの数をに設定します。 値が定義されていない場合、フレームワークは1ページの既定値を使用します。 設定できる最大値は、4 kb サイズのメモリページ (x86 および amd64 プロセッサ) を搭載したコンピューターの場合は16、8 kb サイズのメモリページ (ia64 プロセッサ) を搭載しているコンピューターの場合は8です。 (大量のページが指定されている場合、オペレーティングシステムでは、ログの内容がクラッシュダンプファイルに書き込まれない可能性があります)。次のように、 [Addservice ディレクティブ](../install/inf-addservice-directive.md)と[AddReg ディレクティブ](../install/inf-addreg-directive.md)を使用して、この値を INF ファイルに設定します。

```inf
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

## <a name="forcelogsinminidump"></a>ForceLogsInMiniDump ダンプ

*REG\_DWORD*

を0以外の値に設定すると、フレームワークによってイベントロガーの情報がクラッシュダンプファイルに含まれます。


## <a name="enhancedverifieroptions"></a>EnhancedVerifierOptions

*REG\_DWORD、framework バージョン1.9 以降*

この値にはビットマップが含まれています。 各ビットは、ユーザーがビットを設定することによって有効にできる、追加の検証オプションを表します。

*ビット値:*

**0x1**: 設定した場合、検証ツールは、各ドライバーのイベントコールバック関数が次の処理を実行するかどうかを確認します。

-   が呼び出されたときと同じ IRQL でを返します。 値が異なる場合は、 [**WDF\_違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0x10d---wdf-violation)のバグチェックがエラーコード0xe と共に発生します。

-   戻る前に、によって入力されたすべての[重要な領域](https://docs.microsoft.com/windows-hardware/drivers/kernel/critical-regions-and-guarded-regions)を終了します。 コールバック関数が、入力されたクリティカルな領域内で戻ると、 [**WDF\_違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0x10d---wdf-violation)のバグチェックが0xf ですのエラーコードと共に発生します。

参照: 設定されている場合、およびドライバーで i/o キューの[転送の保証](guaranteeing-forward-progress-of-i-o-operations.md)が有効になっている場合、フレームワークは、キューの i/o 要求ごとにメモリ不足の状況をシミュレート**します。**

**0x20000**: 設定されている場合、およびドライバーで i/o キューの転送の保証が有効になっている場合は、ランダムに選択された i/o 要求に対してメモリ不足の状況がシミュレートされます。


## <a name="verifydownlevel"></a>VerifyDownLevel レベル

*REG\_DWORD、framework バージョン1.9 以降*

0以外の値に設定されていて、現在のバージョンよりも古いバージョンのフレームワークを使用してドライバーがビルドされている場合、フレームワークの検証ツールには、ドライバーのビルド後に追加されたテストが含まれます。 この値が存在しない場合、または0に設定されている場合、フレームワークの検証ツールには、ドライバーがビルドされたときに存在していたテストのみが含まれます。

たとえば、ドライバーがバージョン1.7 のフレームワークでビルドされ、コンピューターに framework のバージョン1.9 がインストールされている場合、 **Verifydownlevel レベル**を0以外に設定すると、検証ツールは、ドライバーの実行時に、検証ツールのバージョン1.9 に追加されたテストを含むようになります。


## <a name="dbgprinton"></a>DbgPrintOn

*REG\_DWORD*

0以外の値に設定されている場合、フレームワークのローダーは、ドライバーを読み込んで、フレームワークライブラリのバージョンにバインドするとき、またはドライバーのアンロード中に、さまざまなメッセージをカーネルデバッガーに送信します。

KMDF ドライバーの場合は、 **\\HKLM SYSTEM\\CurrentControlSet\\Control\\Wdf\\kmdf\\Diagnostics**レジストリキーの下にこの値を設定します。 UMDF ドライバーの場合は、 **\\HKLM\\System CurrentControlSet\\Control\\Wdf\\UMDF\\Diagnostics**レジストリキーの下にこの値を設定します。 ドライバーは、オプションの**診断**サブキーを作成する必要がある場合があります。


**\\HKLM SOFTWARE\\Microsoft\\Windows NT\\CurrentVersion\\wudf\\Services\\{193a1820-d9ac-4997-8c55-be817523f6aa}** で、次のレジストリ値を設定することもできます。 これらの値は、システム上のすべての UMDF ドライバーに影響します。

## <a name="hostprocessdbgbreakonstart"></a>HostProcessDbgBreakOnStart

*REG\_DWORD、UMDF のみ*

秒単位の遅延値を格納します。 指定された遅延期間中、ホストプロセスはユーザーモードのデバッガーを1回だけ検索し、接続されている場合はを中断します。 この期間内にユーザーモードのデバッガーがアタッチされておらず、 **Hostprocessdbgbreakonstart** (0x80000000) の上位ビットが設定されている場合 (0x80000000)、このフレームワークはカーネルモードのデバッガーの中断を1回試みます。 次に例を示します。

|[値]|結果|
|--- |--- |
|0x00000004|フレームワークは、4秒間に1回、ユーザーモードのデバッガーへの接続を試みます。 このフレームワークは、カーネルモードのデバッガーへの接続を試行しません。|
|0x80000000|フレームワークは、ユーザーモードのデバッガーへの接続を1回試行します。 ユーザーモードのデバッガーがアタッチされていない場合、フレームワークはカーネルモードのデバッガーに接続しようとします。|
|0x80000004|フレームワークは、4秒間に1回、ユーザーモードのデバッガーへの接続を試みます。 ユーザーモードのデバッガーが4秒以内にアタッチされていない場合、フレームワークはカーネルモードのデバッガーに接続しようとします。|


## <a name="hostprocessdbgbreakondriverload"></a>HostProcessDbgBreakOnDriverLoad

*REG\_DWORD、UMDF のみ*

秒単位の遅延値を格納します。 ドライバーが読み込まれてから、指定した秒数が経過するまで、WUDFHost が発生します。 **Hostprocessdbgbreakondriverload**の動作は、 **Hostprocessdbgbreakonstart**に記述されているものと同じです。

**Hostprocessdbgbreakonstart**または**Hostprocessdbgbreakondriverload**を指定すると、フレームワークによって他の UMDF タイムアウト (プラグアンドプレイ操作など) が無効になります。 これは、ドライバーで過剰なタイムアウトが発生した場合に、これらの値を使用すると、ドライバーによってターゲット上で致命的なクラッシュが発生する可能性があることを意味します。

これらのレジストリ値は、WDK に含まれている WDF Verifier ツール (WdfVerifier) を使用して設定することもできます。 このツールと UMDF ドライバーの使用の詳細については、「 [WDF verifier を使用した Umdf 検証機能の設定の管理](https://docs.microsoft.com/windows-hardware/drivers/devtest/global-wdf-settings-tab)」を参照してください。

これらの追加の値は **、\\HKLM\\SOFTWARE\\Microsoft Windows\\NT\\CurrentVersion wudf\\DebugMode**にあります。

## <a name="debugmodeflags"></a>DebugModeFlags

*REG\_DWORD、UMDF のみ*

|値|説明|
|--- |--- |
|0x01|デバッグモードを有効にします。 この設定は、「 [UMDF ドライバーでのデバイスプールの使用](using-device-pooling-in-umdf-drivers.md)」で説明されている自動再起動機能を無効にします。|
|0x02|デバイスプーリングを無効にします。 デバイスプールの詳細については、「 [UMDF ドライバーでのデバイスプールの使用](using-device-pooling-in-umdf-drivers.md)」を参照してください。|
|0x04|タイムアウトを無効にします。|
 

Microsoft Visual Studio で F5 オプションを使用すると、展開されたドライバーに対して3つのフラグがすべて設定されます。

## <a name="debugmodebinaries"></a>DebugModeBinaries

*REG\_マルチ\_SZ、UMDF のみ*

この値は、デバッグモードで読み込まれるドライバーバイナリの名前を指定します。 たとえば、ドライバーバイナリの X .DLL、.dll、および Z .DLL のデバッグモードを有効にするには、この値を「 *x .Dll\\0y」に設定します。DLL\\0Z .dll\\\\0 0*.

**HKLM\\\\SOFTWARE\\Microsoft Windows NT\\CurrentVersion\\wudf**では、次の値を設定することもできます。

## <a name="hostfailkddebugbreak"></a>HostFailKdDebugBreak

*REG\_DWORD、UMDF のみ*

この値がゼロ以外で、カーネルデバッガーがコンピューターに接続されている場合、リフレクタはホストプロセスを終了する前にカーネルデバッガーに中断します。 **HostFailKdDebugBreak**は、Windows 7 以前のオペレーティングシステムでは既定で無効になっています。 Windows 8 以降では、 **HostFailKdDebugBreak**は既定で有効になっています。

リフレクターは、ホストプロセスが予期せず終了した場合 (たとえば、非 UMDF コンポーネントまたはハンドルされない例外が原因で)、カーネルデバッガーにも中断します。 終了しようとしているホストプロセスに複数のデバイススタックがプールされている場合、リフレクタは、ホストプロセスで読み込まれたデバイススタックごとに1回、デバッガーに複数回中断します。

UMDF レジストリ値の変更を有効にするには、コンピューターを再起動する必要があります。
 
