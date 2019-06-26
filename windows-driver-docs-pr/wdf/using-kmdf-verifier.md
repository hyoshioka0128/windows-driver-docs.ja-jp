---
title: KMDF 検証ツールの使用
description: KMDF 検証ツールの使用
ms.assetid: ab6a0149-9341-435b-b7e7-9c5d6520ebd8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec59065bdb69273a44fb6f0effc01f8abac13766
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372238"
---
# <a name="using-kmdf-verifier"></a>KMDF 検証ツールの使用


フレームワークは、実行中の KMDF ドライバーをテストに使用できる組み込みの検証機能を提供します。 KMDF 検証機能と呼ばれる、この機能は、広範囲にドライバーの状態と、ドライバーが framework オブジェクトのメソッドに渡される引数を検証します。 フレームワークの検証ツールを使用するには、単独または汎用と共に[Driver Verifier (Verifier.exe)](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)ツール。

フレームワークがロックの取得と階層を確認します。 によってフレームワークへの呼び出し、適切な IRQL で発生する、適切な I/O キャンセル機能とキューの使用率を確認しますをドライバーとフレームワークに従って、文書化されていること、KMDF 検証機能が有効になっている場合コントラクト。 ドライバー開発者は、クラッシュ、ハング、またはアンロードに失敗することがなく、ドライバーが適切に応答かどうかをテストできるようににメモリ不足の条件をシミュレーションすることもできます。

KMDF 検証機能が有効にすると、フレームワークは、60 秒間の既定タイムアウト期間が終了する前に、いくつかのイベントについて説明した完了した場合、デバッガーに分割します。 この時点で、問題をデバッグしたり、タイムアウト期間を再起動するデバッガーで"g"を入力できます。 使用して既定のタイムアウト期間を変更することができます、 **DbgWaitForSignalTimeoutInSec**で説明されているレジストリ値[検証ツールの動作を制御する](#controlling-the-verifiers-behavior)します。

お勧め Driver Verifier (Verifier.exe) を実行中にテスト、および独自のドライバーと wdf01000.sys を確認してください ボックスの一覧に追加します。

ドライバーは、KMDF バージョン 1.9 以降でビルドされました、Verifier.exe を実行すると、KMDF 検証ツールが自動的に有効にします。

使用することも、 [WDF Verifier コントロール アプリケーション (WdfVerifier.exe)](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdf-verifier-control-application) KMDF 検証を無効にします。

## <a name="enabling-and-disabling-the-frameworks-built-in-verification"></a>有効にして、フレームワークの組み込みの検証を無効化


この手順を使用して、KMDF Verifier を手動で有効にできます。

1.  ドライバーは既に読み込まれている場合は、デバイス マネージャーを使用してデバイスを無効にします。 デバイスを無効にすると、ロードするドライバーと。
2.  RegEdit を使用して設定を**VerifierOn** 0 以外の場合、ドライバーの値に**パラメーター\\Wdf**のサブキー、 **HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\サービス**Windows レジストリのキー。 0 以外の値は、KMDF 検証機能が有効になっていることを示します。

    追加する必要があります**VerifierOn**サブキーが存在しない場合に手動でします。

3.  これにより、ドライバーの読み込み、デバイスを再度有効にするのにには、デバイス マネージャーを使用します。
4.  ドライバーを呼び出すと[ **WdfDriverCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nf-wdfdriver-wdfdrivercreate)、フレームワークは、レジストリを検査し、場合、フレームワークの検証を有効に**VerifierOn** 0 以外の値。

フレームワークの検証を無効にする、同じ手順しますが、の値を設定**VerifierOn**をゼロにします。

フレームワークの検証が有効になっているかどうかを確認するには、ドライバーの呼び出しの後の場所にブレークポイントを設定します[ **WdfDriverCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nf-wdfdriver-wdfdrivercreate)を使用すると、 [ **! wdfdriverinfo。** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdriverinfo)デバッガー拡張機能コマンド。

**!wdfkd.wdfdriverinfo** *&lt;your drivername&gt;*  **** **0x1**

デバッガーの拡張機能コマンドの詳細については、次を参照してください。 [Framework ベースのドライバーの拡張機能をデバッガー](debugger-extensions-for-kmdf-drivers.md)します。

## <a name="controlling-the-verifiers-behavior"></a>検証の動作を制御します。


使用することをお勧め、 [WDF Verifier コントロール アプリケーション](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdf-verifier-control-application)を以下のオプションを制御します。 ただし、レジストリで次の値を直接変更することができます。

関連する値が下にある、**パラメーター\\Wdf**のサブキー、 **HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\サービス**キー。

<a href="" id="verifyon-----------------reg-dword-"></a>**VerifyOn** (**REG\_DWORD**)  
この値を有効にするのには 0 以外の値を設定、 [ **WDFVERIFY** ](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfverify)マクロ。

<a href="" id="dbgbreakonerror-----------------------------reg-dword-"></a>**DbgBreakOnError** (**REG\_DWORD**)  
(該当する場合) に、フレームワークがデバッガーに割り込むはこの値が 0 以外の値に設定されている場合、ドライバーを呼び出すたびに[ **WdfVerifierDbgBreakPoint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfverifier/nf-wdfverifier-wdfverifierdbgbreakpoint)します。

<a href="" id="dbgwaitforsignaltimeoutinsec---------------reg-dword-"></a>**DbgWaitForSignalTimeoutInSec** (**REG\_DWORD**)  
以降では、Windows 8、ときに**VerifierOn**と**DbgBreakOnError**設定は、0 以外の値をドライバーは、設定して既定のタイムアウト期間を変更できます**DbgWaitForSignalTimeoutInSec**.

<a href="" id="verifierallocatefailcount------------------------------reg-dword-"></a>**VerifierAllocateFailCount** (**REG\_DWORD**)  
この値が値に設定されている場合*n*、フレームワークには、後で、ドライバーのオブジェクトのメモリを割り当てるすべての試行が失敗した、 *n 番目*割り当て。

<a href="" id="trackhandles---------------reg-multi-sz-"></a>**TrackHandles** (**REG\_マルチ\_SZ**)  
この値が framework オブジェクトのハンドルの 1 つまたは複数の型名のリストに設定されている場合、フレームワークは、指定したハンドル型に一致するすべてのオブジェクト ハンドルへの参照を追跡します。

<a href="" id="enhancedverifieroptions-----------------------------reg-dword-"></a>**EnhancedVerifierOptions** (**REG\_DWORD**)  
**KMDF のみ**

フレームワークの検証の省略可能な機能を有効に使用できるビットマップが含まれています。

<a href="" id="verifydownlevel--------------reg-dword-"></a>**VerifyDownLevel** (**REG\_DWORD**)  
場合は 0 以外の値に設定され、フレームワークの検証にドライバーがビルドされた後に追加されたテストが含まれています、ドライバーが現在のバージョンより古いフレームワークのバージョンでビルドされている場合。

一般的な規則として、上記のレジストリ値を設定すると、削除不要になったとき。

これらのレジストリ値の完全な説明については、次を参照してください。[デバッグ フレームワーク ベースのドライバーのレジストリ値](registry-values-for-debugging-kmdf-drivers.md)します。

 

 





