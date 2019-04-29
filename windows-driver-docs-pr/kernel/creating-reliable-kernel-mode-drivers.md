---
title: 信頼性の高いカーネルモード ドライバーの作成
description: 信頼性の高いカーネルモード ドライバーの作成
ms.assetid: 31bbf1fe-dc90-43e0-a53e-eca902ec343e
keywords:
- カーネル モード ドライバー WDK、信頼性
- 信頼性の WDK カーネル
- 信頼性の高いドライバーに関する、信頼性の WDK カーネル
- Irp WDK カーネルでは、信頼性の問題
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec3d064e5f1bd63d0876519025edeaac9a2683d2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388249"
---
# <a name="creating-reliable-kernel-mode-drivers"></a>信頼性の高いカーネルモード ドライバーの作成





ドライバーは、カーネル モードで実行する合計コードのかなりの割合を構成します。 カーネル モード ドライバーとは、実際には、オペレーティング システムのコンポーネントを指します。 そのため、信頼性が高くセキュリティで保護されたドライバーはオペレーティング システムの全体的な信頼性を示すために非常に役立ちます。 信頼性の高いカーネル モード ドライバーを作成するには、次のガイドラインに従います。

-   デバイス オブジェクトを正しくセキュリティで保護します。

    システムのドライバーとデバイスへのユーザー アクセスは、システムは、デバイス オブジェクトに割り当てるセキュリティ記述子によって制御されます。 最も多くの場合、システムは、デバイスがインストールされている場合、デバイスのセキュリティ パラメーターを設定します。 詳細については、次を参照してください。[セキュリティで保護されたデバイスのインストールを作成する](https://msdn.microsoft.com/library/windows/hardware/ff540212)します。 そのデバイスへのアクセス制御に関与するためのドライバーの適切な場合があります。 詳細については、次を参照してください。[デバイス オブジェクトのセキュリティで保護する](securing-device-objects.md)します。

-   デバイス オブジェクトを正しく検証されます。

    ドライバーは、複数の種類のデバイス オブジェクトを作成する場合に各 IRP を受信する種類を確認するあります。 詳細については、次を参照してください。[デバイス オブジェクトの検証に失敗した](failure-to-validate-device-objects.md)します。

-   「安全な文字列」関数を使用します。

    文字列を操作する場合、ドライバーは、C と C++ 言語のランタイム ライブラリで提供されている文字列関数ではなく、安全な文字列関数を使用してください。 詳細については、次を参照してください。[安全な文字列関数を使用して](using-safe-string-functions.md)します。

-   オブジェクト ハンドルを検証します。

    オブジェクト ハンドルが表示されるように入力する必要があります、ハンドルが有効であることを確認するドライバーは、アクセス可能の種類が必要です。 詳細については、オブジェクトのハンドルを使用して、次のトピックを参照してください。

    [オブジェクトの管理](managing-kernel-objects.md)

    [オブジェクト ハンドルの検証に失敗しました](failure-to-validate-object-handles.md)

-   マルチプロセッサを正しくサポートします。

    シングル プロセッサ システムでのみ、ドライバーを実行することを想定しないでください。 プログラミングには、ドライバーがマルチプロセッサ システムで適切に動作することを確認するために使用できる手法については、次のトピックを参照してください。

    [同期方法](synchronization-techniques.md)

    [マルチプロセッサ環境でのエラー](errors-in-a-multiprocessor-environment.md)

-   ドライバーの状態を適切に処理します。

    常に、ドライバーがであると仮定する状態であることを確認するのには重要です。 たとえば、ドライバーは IRP を受信する場合、既にサービス中です、同じ種類の IRP でしょうか。 ドライバーは、このような状況をチェックしません、最初の IRP が失われる可能性があります。 詳細については、次を参照してください。[ドライバーの状態を確認するエラー](failure-to-check-a-driver-s-state.md)します。

-   IRP の入力値を検証します。

    信頼性とバッファーのアドレスと長さなどの IRP に関連付けられているすべての値を検証する、セキュリティの観点から、重要です。 次のトピックでは、IRP の入力値の検証に関する情報を提供します。

    [バッファー内の I/O を使用して DispatchReadWrite](dispatchreadwrite-using-buffered-i-o.md)

    [バッファー内の i/o エラー](errors-in-buffered-i-o.md)

    [ダイレクト I/O を使用して DispatchReadWrite](dispatchreadwrite-using-direct-i-o.md)

    [ダイレクト I/O エラー](errors-in-direct-i-o.md)

    [I/O 制御コードに関するセキュリティの問題](security-issues-for-i-o-control-codes.md)

    [ユーザー領域のアドレスを参照するエラー](errors-in-referencing-user-space-addresses.md)

-   I/O スタックを適切に処理します。

    ときに[ドライバー スタックを Irp を渡して](passing-irps-down-the-driver-stack.md)を呼び出してドライバーの重要[ **IoSkipCurrentIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff550355)または[ **IoCopyCurrentIrpStackLocationToNext** ](https://msdn.microsoft.com/library/windows/hardware/ff548387) [次へ] のドライバーの I/O スタックの場所を設定します。 次に I/O スタックの 1 つの場所を直接コピーするコードを書き込みません。

-   IRP の完了操作を適切に処理します。

    ドライバーは IRP の状態のステータス値を持つ決して完了する必要があります\_成功しない限り、実際にサポートし、IRP を処理します。 IRP の完了操作を処理する正しい方法については、次を参照してください。 [Irp の完了](completing-irps.md)します。

-   IRP の取り消し操作を適切に処理します。

    操作のキャンセルは難しいコードに正しくため、通常は非同期的に実行します。 ハンドルが操作をキャンセルするコードの問題はことができますので、このコードは、通常では実行されません頻繁に実行中のシステムに、時間が長く気付かない移動します。

    すべての提供情報を理解し、必ず[Irp のキャンセル](canceling-irps.md)します。 特に注意[同期 IRP のキャンセル](synchronizing-irp-cancellation.md)と[Irp の検討時にキャンセルを指す](points-to-consider-when-canceling-irps.md)します。

    関連付けられている同期の問題を回避する方法の 1 つキャンセル操作が実装するために、[キャンセル セーフ IRP キュー](cancel-safe-irp-queues.md)します。 キャンセルの安全な IRP のキューは、Windows XP およびそれ以降のオペレーティング システム バージョンが導入されましたが、旧バージョンと互換性のある以前のバージョンにもドライバー管理キューです。

-   IRP のクリーンアップを処理し、適切に操作を終了します。

    間の違いを理解しているかどうかを必ず[ **IRP\_MJ\_クリーンアップ**](https://msdn.microsoft.com/library/windows/hardware/ff550718)と[ **IRP\_MJ\_閉じる** ](https://msdn.microsoft.com/library/windows/hardware/ff550720)要求。 アプリケーションは、ファイル オブジェクトのすべてのハンドルを閉じますが、すべての I/O の前にも要求が完了した後、クリーンアップ要求が到着します。 閉じる要求は、ファイル オブジェクトのすべての I/O 要求が完了またはキャンセルされた後に到着します。 詳しくは、次のトピックをご覧ください。

    [DispatchCreate、DispatchClose、および DispatchCreateClose ルーチン](dispatchcreate--dispatchclose--and-dispatchcreateclose-routines.md)

    [DispatchCleanup ルーチン](dispatchcleanup-routines.md)

    [操作のクリーンアップと閉じる処理のエラー](errors-in-handling-cleanup-and-close-operations.md)

Irp を正しく処理の詳細については、次を参照してください。 [Irp の処理で関連するエラー](additional-errors-in-handling-irps.md)します。

### <a name="using-driver-verifier"></a>ドライバーの検証ツールの使用

[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)ドライバーの信頼性を確保する最も重要なことができるツールです。 Driver Verifier は、さまざまなこのセクションで説明したものの一部など、一般的なドライバーの問題を確認できます。 ただし、Driver Verifier の使用は、気を付けて、親切なソフトウェアの設計は置き換えられません。

 

 




