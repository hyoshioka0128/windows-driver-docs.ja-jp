---
title: KMDF 検証ツールの使用
description: KMDF 検証ツールの使用
ms.assetid: ab6a0149-9341-435b-b7e7-9c5d6520ebd8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac1e0d92cd2cc0ffd5f502e38eb6a962741a9347
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842128"
---
# <a name="using-kmdf-verifier"></a>KMDF 検証ツールの使用


フレームワークには、実行中の KMDF ドライバーのテストに使用できる組み込みの検証機能が用意されています。 KMDF Verifier と呼ばれるこの機能は、ドライバーの状態と、ドライバーがフレームワークオブジェクトメソッドに渡す引数を広範囲にわたって検証します。 フレームワークの検証機能は、単独で使用することも、汎用[ドライバー検証ツール (verifier)](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)ツールと共に使用することもできます。

KMDF 検証機能が有効になっている場合、フレームワークはロックの取得と階層を確認し、フレームワークの呼び出しが正しい IRQL で実行されることを確認し、正しい i/o のキャンセルとキューの使用を確認し、ドライバーとフレームワークがドキュメントに従っていることを確認します。関する. また、ドライバー開発者が、クラッシュ、ハング、またはアンロードに失敗しないで適切に応答するかどうかをテストできるように、メモリ不足の状態をシミュレートすることもできます。

KMDF 検証ツールが有効になっている場合、前に説明したイベントの一部が完了する前に、既定のタイムアウト時間60秒が経過すると、フレームワークはデバッガーに中断します。 この時点で、問題をデバッグしたり、デバッガーで「g」と入力してタイムアウト期間を再起動したりできます。 既定のタイムアウト期間を変更するには、「[検証ツールの動作の制御](#controlling-the-verifiers-behavior)」で説明されている**DbgWaitForSignalTimeoutInSec**レジストリ値を使用します。

テスト中にドライバー検証ツール (ngen.exe) を実行し、独自のドライバーと wdf01000 を [確認] 一覧に追加することをお勧めします。

ドライバーが KMDF バージョン1.9 以降を使用してビルドされている場合に、Verifier を実行すると、KMDF 検証ツールが自動的に有効になります。

また、 [WDF Verifier コントロールアプリケーション (WdfVerifier)](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdf-verifier-control-application)を使用して、Kmdf 検証機能を有効または無効にすることもできます。

## <a name="enabling-and-disabling-the-frameworks-built-in-verification"></a>フレームワークの組み込み検証を有効または無効にする


次の手順に従って、KMDF 検証を手動で有効にすることができます。

1.  ドライバーが既に読み込まれている場合は、デバイスマネージャーを使用してデバイスを無効にします。 デバイスを無効にすると、ドライバーがアンロードされます。
2.  RegEdit **\_ローカル\_コンピューター\\システム\\CurrentControlSet\\サービス**キーの **\\** 、ドライバーのパラメーターの0以外の値**に設定する**には、RegEdit を使用します。登録. 0以外の値は、KMDF 検証機能が有効になっていることを示します。

    **VerifierOn**がまだ存在しない場合は、サブキーに手動で追加する必要があります。

3.  デバイスマネージャーを使用してデバイスを再度有効にし、その結果、ドライバーを読み込みます。
4.  ドライバーが[**Wdfdrivercreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdrivercreate)を呼び出すと、フレームワークはレジストリを調べ、0以外の値に**VerifierOn**した場合にフレームワークの検証ツールを有効にします。

フレームワークの検証を無効にするには、同じ手順を実行しますが、 **VerifierOn**の値を0に設定します。

フレームワークの検証機能が有効になっているかどうかを判断するには、ドライバーが[**Wdfdrivercreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdrivercreate)を呼び出した後、場所にブレークポイントを設定し、 [ **! wdfdrivercreate**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdriverinfo)デバッガー拡張コマンドを使用します。

*&lt;ドライバー&gt;*  **** **0x1**の場合は、 **! wdfkd. wdfdriverinfo を使用します。**

デバッガー拡張機能のコマンドの詳細については、「[フレームワークベースのドライバーのデバッガー拡張](debugger-extensions-for-kmdf-drivers.md)」を参照してください。

## <a name="controlling-the-verifiers-behavior"></a>検証機能の動作の制御


以下のオプションを制御するには、 [WDF Verifier コントロールアプリケーション](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdf-verifier-control-application)を使用することをお勧めします。 ただし、レジストリ内の次の値を直接変更することができます。

関連する値は、 **HKEY\_ローカル\_コンピューター\\System\\CurrentControlSet\\Services**キーの**パラメーター\\Wdf**サブキーの下にあります。

<a href="" id="verifyon-----------------reg-dword-"></a>**Verifyon** (**REG\_DWORD**)  
[**Wdfverify**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfverify)マクロを有効にするには、この値を0以外の値に設定します。

<a href="" id="dbgbreakonerror-----------------------------reg-dword-"></a>**Dbgbreakonerror** (**REG\_DWORD**)  
この値が0以外の値に設定されている場合、ドライバーが[**WdfVerifierDbgBreakPoint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfverifier/nf-wdfverifier-wdfverifierdbgbreakpoint)を呼び出すたびに、フレームワークはデバッガーを中断します (使用可能な場合)。

<a href="" id="dbgwaitforsignaltimeoutinsec---------------reg-dword-"></a>**DbgWaitForSignalTimeoutInSec** (**REG\_DWORD**)  
Windows 8 以降では、 **VerifierOn**と**dbgbreakonerror**が0以外の値に設定されている場合、ドライバーは**DbgWaitForSignalTimeoutInSec**を設定して既定のタイムアウト期間を変更できます。

<a href="" id="verifierallocatefailcount------------------------------reg-dword-"></a>**VerifierAllocateFailCount** (**REG\_DWORD**)  
この値が*n*に設定されている場合、n*番目*の割り当ての後、ドライバーのオブジェクトにメモリを割り当てようとするたびに、フレームワークは失敗します。

<a href="" id="trackhandles---------------reg-multi-sz-"></a>**Trackhandles** (**REG\_複数\_SZ**)  
この値がフレームワークオブジェクトハンドルの1つ以上の型名のリストに設定されている場合、フレームワークは、指定されたハンドル型に一致するすべてのオブジェクトハンドルへの参照を追跡します。

<a href="" id="enhancedverifieroptions-----------------------------reg-dword-"></a>**EnhancedVerifierOptions** (**REG\_DWORD**)  
**KMDF のみ**

フレームワークの検証ツールのオプション機能を有効にするために使用できるビットマップが含まれています。

<a href="" id="verifydownlevel--------------reg-dword-"></a>**Verifydownlevel レベル**(**REG\_DWORD**)  
0以外の値に設定されていて、現在のバージョンよりも古いバージョンのフレームワークを使用してドライバーがビルドされている場合、フレームワークの検証ツールには、ドライバーのビルド後に追加されたテストが含まれます。

一般的な規則として、上記のレジストリ値を設定した場合は、不要になったときに削除します。

これらのレジストリ値の詳細については、「[フレームワークベースのドライバーをデバッグするためのレジストリ値](registry-values-for-debugging-kmdf-drivers.md)」を参照してください。

 

 





