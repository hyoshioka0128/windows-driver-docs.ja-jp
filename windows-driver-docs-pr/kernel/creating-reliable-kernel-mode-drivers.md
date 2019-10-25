---
title: 信頼性の高いカーネルモード ドライバーの作成
description: 信頼性の高いカーネルモード ドライバーの作成
ms.assetid: 31bbf1fe-dc90-43e0-a53e-eca902ec343e
keywords:
- カーネルモードドライバー WDK、信頼性
- 信頼性 WDK カーネル
- 信頼性のある WDK カーネル、信頼性の高いドライバーの概要
- Irp WDK カーネル、信頼性の問題
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 29416bf9729329149b4ea280ec49f001c43b25c0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828439"
---
# <a name="creating-reliable-kernel-mode-drivers"></a>信頼性の高いカーネルモード ドライバーの作成





ドライバーは、カーネルモードで実行されるコード全体の割合を大幅に増やします。 カーネルモードドライバーは、実質的にはオペレーティングシステムのコンポーネントです。 したがって、信頼性が高く、セキュリティで保護されたドライバーは、オペレーティングシステムの全体的な信頼性に大きく影響します。 信頼性の高いカーネルモードドライバーを作成するには、次のガイドラインに従ってください。

-   デバイスオブジェクトを適切にセキュリティで保護します。

    システムのドライバーとデバイスへのユーザーアクセスは、システムによってデバイスオブジェクトに割り当てられるセキュリティ記述子によって制御されます。 多くの場合、デバイスのインストール時に、システムによってデバイスのセキュリティパラメーターが設定されます。 詳細については、「[安全なデバイスのインストールの作成](https://docs.microsoft.com/windows-hardware/drivers/install/creating-secure-device-installations)」を参照してください。 場合によっては、ドライバーがデバイスへのアクセスを制御するために、一部を再生するのが適切な場合があります。 詳細については、「[デバイスオブジェクトのセキュリティ保護](securing-device-objects.md)」を参照してください。

-   デバイスオブジェクトを正しく検証します。

    ドライバーが複数の種類のデバイスオブジェクトを作成する場合は、各 IRP で受信する種類を確認する必要があります。 詳細については、「[デバイスオブジェクトの検証エラー](failure-to-validate-device-objects.md)」を参照してください。

-   "安全な文字列" 関数を使用します。

    文字列を操作する場合、ドライバーは、C/C++言語ランタイムライブラリに用意されている文字列関数ではなく、安全な文字列関数を使用する必要があります。 詳細については、「[安全な文字列関数の使用](using-safe-string-functions.md)」を参照してください。

-   オブジェクトハンドルを検証します。

    オブジェクトハンドルを入力として受け取るドライバーは、ハンドルが有効であること、アクセス可能であること、および予期される型であることを確認する必要があります。 オブジェクトハンドルの使用方法の詳細については、次のトピックを参照してください。

    [オブジェクト管理](managing-kernel-objects.md)

    [オブジェクトハンドルの検証エラー](failure-to-validate-object-handles.md)

-   マルチプロセッサを適切にサポートします。

    ドライバーがシングルプロセッサシステムでのみ実行されるとは限りません。 マルチプロセッサシステムでドライバーが正しく機能することを確認するために使用できるプログラミング手法の詳細については、次のトピックを参照してください。

    [同期方法](synchronization-techniques.md)

    [マルチプロセッサ環境でのエラー](errors-in-a-multiprocessor-environment.md)

-   ドライバーの状態を適切に処理します。

    ドライバーがあると想定されている状態であることを常に確認することが重要です。 たとえば、ドライバーが IRP を受信した場合、同じ種類の IRP を既にサービスしていますか。 ドライバーがこの状況を確認しない場合、最初の IRP が失われる可能性があります。 詳細については、「[ドライバーの状態を確認](failure-to-check-a-driver-s-state.md)できません」を参照してください。

-   IRP 入力値を検証します。

    信頼性とセキュリティの観点から、IRP に関連付けられているすべての値 (バッファーアドレスや長さなど) を検証することが不可欠です。 次のトピックでは、IRP 入力値の検証に関する情報を提供します。

    [バッファーされる i/o を使用した DispatchReadWrite](dispatchreadwrite-using-buffered-i-o.md)

    [バッファーされる i/o のエラー](errors-in-buffered-i-o.md)

    [直接 i/o を使用した DispatchReadWrite](dispatchreadwrite-using-direct-i-o.md)

    [ダイレクト i/o のエラー](errors-in-direct-i-o.md)

    [I/o 制御コードに関するセキュリティの問題](security-issues-for-i-o-control-codes.md)

    [ユーザー領域のアドレスを参照中のエラー](errors-in-referencing-user-space-addresses.md)

-   I/o スタックを適切に処理します。

    [Irp をドライバースタックに渡す](passing-irps-down-the-driver-stack.md)ときには、ドライバーが次のドライバーの i/o スタックの場所を[**設定するために、** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocopycurrentirpstacklocationtonext) [**ioskipのエンティティの場所**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)を呼び出す必要があります。 1つの i/o スタック位置を直接コピーするコードを記述しないでください。

-   IRP 完了操作を適切に処理します。

    Irp を実際にサポートして処理しない限り、状態の値が [成功] の\_IRP を完了することはできません。 IRP の完了操作を処理する正しい方法については、「 [irp の完了](completing-irps.md)」を参照してください。

-   IRP のキャンセル操作を適切に処理します。

    通常、キャンセル操作は非同期的に実行されるため、適切にコーディングするのが困難な場合があります。 通常、このコードは実行中のシステムで頻繁に実行されないため、キャンセル操作を処理するコードの問題は、長時間気付かないことがあります。

    「 [Irp の取り消し](canceling-irps.md)」で提供されているすべての情報を読んで理解してください。 Irp を[キャンセルするときに考慮する必要が](points-to-consider-when-canceling-irps.md)ある[irp のキャンセル](synchronizing-irp-cancellation.md)とポイントの同期に特に注意してください。

    キャンセル操作に関連付けられている同期の問題を回避する1つの方法は、[キャンセルセーフの IRP キュー](cancel-safe-irp-queues.md)を実装することです。 キャンセルセーフな IRP キューは、Windows XP 以降のバージョンのオペレーティングシステムで導入されたドライバー管理のキューですが、以前のバージョンとの下位互換性もあります。

-   IRP のクリーンアップと終了操作を適切に処理します。

    [**Irp\_MJ\_CLEANUP**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-cleanup)と[**irp\_MJ\_CLOSE**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-close)要求の違いを理解していることを確認してください。 クリーンアップ要求は、アプリケーションがファイルオブジェクトのすべてのハンドルを閉じた後に到着しますが、すべての i/o 要求が完了する前に発生することもあります。 Close 要求は、ファイルオブジェクトのすべての i/o 要求が完了または取り消された後に到着します。 詳しくは、次のトピックをご覧ください。

    [DispatchCreate、DispatchClose、および DispatchCreateClose ルーチン](dispatchcreate--dispatchclose--and-dispatchcreateclose-routines.md)

    [DispatchCleanup ルーチン](dispatchcleanup-routines.md)

    [クリーンアップおよび終了操作の処理中に発生したエラー](errors-in-handling-cleanup-and-close-operations.md)

Irp を正しく処理する方法の詳細については、「 [irp の処理に関するその他のエラー](additional-errors-in-handling-irps.md)」を参照してください。

### <a name="using-driver-verifier"></a>ドライバーの検証ツールの使用

ドライバーの[検証](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)ツールは、ドライバーの信頼性を確保するために使用できる最も重要なツールです。 ドライバーの検証ツールでは、このセクションで説明しているいくつかの一般的なドライバーの問題を確認できます。 ただし、ドライバーの検証ツールを使用しても、慎重なソフトウェア設計には代わるものではありません。

 

 




