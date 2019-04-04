---
title: I/O 転送シーケンス
description: SPB フレームワーク拡張機能 (SpbCx) には、I/O 転送シーケンスがサポートしています。
ms.assetid: 7415DB28-5E93-4F47-B169-7C652969D4C7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ffbe0d3ea5c54f3185f321dd0e85df598e0bb63c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551981"
---
# <a name="io-transfer-sequences"></a>I/O 転送シーケンス


SPB フレームワーク拡張機能 (SpbCx) には、I/O 転送シーケンスがサポートしています。 I/O の転送シーケンスは、バスの転送 (読み取りし、書き込み操作) の順序付けされたセットがバスの単一のアトミック操作として実行します。 I/O の転送シーケンスで、転送のすべてバス上の同じターゲット デバイスにアクセスします。 シーケンスを実行中は、バス上の他のデバイスにはアクセスできません、場合でも、I/O の転送シーケンスが完了する前に、SPB コント ローラーのドライバーは他のデバイスの I/O 要求を受け取る可能性があります。

I/O の転送シーケンスの例は、バス書き込み操作で、バスの読み取り操作の後に読み取り-書き込み操作です。 クライアントの周辺機器のデバイス ドライバーは、SPB 接続の周辺機器の関数の選択レジスタへの書き込みをこの種類のシーケンスを使用してし、し、選択したデバイスの機能の値を読み取る可能性があります。 これら 2 つの転送には、さまざまな長さを指定できます。 たとえば、書き込み操作を 1 バイトのデータを転送し、読み取り操作は多くのバイトのデータを転送場合があります。

## <a name="types-of-io-transfer-sequences"></a>種類の I/O 転送シーケンス


クライアントは、これら 2 つの方法のいずれかでの I/O 転送シーケンスを開始できます。

-   クライアントは、全体のシーケンスを指定できます、 [ **IOCTL\_SPB\_EXECUTE\_シーケンス**](https://msdn.microsoft.com/library/windows/hardware/hh450857) I/O 制御要求。 この要求には、転送シーケンスを実行するどのようなハードウェア固有のパフォーマンスの最適化を使用する SPB コント ローラー ドライバーができます。 詳細については、[単一要求シーケンス](#buses-single-request-sequences)を参照してください。

-   クライアントが送信できる、 [ **IOCTL\_SPB\_ロック\_コント ローラー** ](https://msdn.microsoft.com/library/windows/hardware/hh450858)は、シーケンスの先頭に、コント ローラーをロックして、の送信I/O制御要求[ **IOCTL\_SPB\_UNLOCK\_コント ローラー** ](https://msdn.microsoft.com/library/windows/hardware/hh450859)シーケンスが完了するとします。 クライアントが別の I/O 要求を送信して、コント ローラーがロックされている間 ([**IRP\_MJ\_読み取り**](https://msdn.microsoft.com/library/windows/hardware/ff550794)または[ **IRP\_MJ\_書き込み**](https://msdn.microsoft.com/library/windows/hardware/ff550819)) ごとに読み取りまたは書き込み順序で操作します。 詳細については、[Client-Implemented シーケンス](#buses-client-implemented-sequences)を参照してください。

可能であれば、クライアントを使用する必要があります、 **IOCTL\_SPB\_EXECUTE\_シーケンス**が高速化、要求が、発生したエラーを生じとする他の中に時間が大幅に減少クライアントは、バスからロックアウトされました。 ただし、クライアントが使用できる、 **IOCTL\_SPB\_ロック\_コント ローラー**と**IOCTL\_SPB\_UNLOCK\_コント ローラー**要求のかどうかは、シーケンス内の以降の転送を開始できる前に、シーケンス内の転送の 1 つの中に読み取られる値を確認する必要があります。 この場合は、慎重に設計が他のクライアントは、必要に応じてよりも長い期間のバスからのロックを回避するために必要と、不適切に設計され周辺ドライバーには、システム全体のパフォーマンスが低下する可能性が。

## <a name="single-request-sequences"></a>単一要求シーケンス


パフォーマンスを向上させる SPB コント ローラーのドライバーを実装する必要があります、 [ *EvtSpbControllerIoSequence* ](https://msdn.microsoft.com/library/windows/hardware/hh450810)を処理するコールバック関数[ **IOCTL\_SPB\_EXECUTE\_シーケンス**](https://msdn.microsoft.com/library/windows/hardware/hh450857)要求。 この方法は、SPB コント ローラーのドライバーに複雑になりますが、クライアントを一連の個別の読み取りとして、I/O の転送シーケンスを実行し、その他のクライアントは、バスからロックアウトされたときに、書き込み操作が不要になります。

**注**  の実装、 *EvtSpbControllerIoSequence*関数は強くお勧めし、Windows 8 の要件になる可能性があります。

 

転送シーケンスの実装では、単純な読み取りまたは書き込み操作に似ていますが、さらに、シーケンス内の個々 の転送間隔シーケンス操作の状態を保存する更新プログラムが必要です。 最初の転送が完了すると、SPB コント ローラーのドライバーは、シーケンス内の次の転送を選択するシーケンスの状態を更新します。 シーケンスの状態は、デバイス コンテキストに格納されが含まれています、 [ **SPBREQUEST** ](https://msdn.microsoft.com/library/windows/hardware/hh450925)ハンドルに渡される、 *EvtSpbControllerIoSequence*コールバック。 SPB コント ローラーのドライバーでは、このハンドルを使用して、バッファー、長さ、方向を取得し、シーケンス内の個々 の転送パラメーターを配置します。 これらのパラメーターを取得する方法の詳細については、[ **SpbRequestGetTransferParameters**](https://msdn.microsoft.com/library/windows/hardware/hh450924)を参照してください。

SPB コント ローラーのドライバーが、要求を実行できないかどうか**IOCTL\_SPB\_EXECUTE\_シーケンス**操作、エラー コードを使用して要求を完了します。 このような障害が発生する場合、クライアントことができます、オプションとして、バスをロック、一連の簡単なの I/O 要求として I/O 転送シーケンスを明示的に実行およびバスのロックを解除します。 詳細については、[Client-Implemented シーケンス](#buses-client-implemented-sequences)を参照してください。

SpbCx はパラメーターのチェック**IOCTL\_SPB\_* XXX*** 周辺機器のデバイス ドライバーから受信した要求。 **IOCTL\_SPB\_EXECUTE\_シーケンス**要求、SpbCx は空のシーケンスとバッファー ポインターを NULL または長さ 0 のバッファーを含むシーケンスを拒否します。

SPB コント ローラーのドライバーでは、シーケンス内の各転送の長さが、ドライバーが指定した制限を超えていないことを確認してください。 たとえば、SkeletonI2C サンプル ドライバー Windows Driver Kit (WDK) で失敗を**IOCTL\_SPB\_EXECUTE\_シーケンス**4 K バイトを超える転送を指定し、状態を設定する要求この要求の状態をコード\_無効な\_パラメーター。 シーケンスの操作を開始する前に、 **IOCTL\_SPB\_EXECUTE\_シーケンス**要求と、ドライバーは、シーケンス内のすべての転送ことを確認するためのパラメーターを検証する必要があります、操作は正常に完了することができます。

決して SpbCx の前に、 *EvtSpbControllerIoSequence*のコールバックを[ *EvtSpbControllerLock* ](https://msdn.microsoft.com/library/windows/hardware/hh450814)コールバック、およびそれに依存しない、 *EvtSpbControllerIoSequence*のコールバックを[ *EvtSpbControllerUnlock* ](https://msdn.microsoft.com/library/windows/hardware/hh450814)コールバック。

## <a name="client-implemented-sequences"></a>クライアントで実装されたシーケンス


SPB コント ローラーのドライバーのクライアントと一連の単純な読み取りし、書き込み I/O の転送シーケンスを明示的に実行できます。 クライアントには、カーネル モード ドライバーまたはバスに接続されている周辺機器のデバイスを制御するユーザー モード ドライバーのいずれかを指定できます。 クライアントが送信シーケンスの最初の転送する前に、 [ **IOCTL\_SPB\_ロック\_コント ローラー** ](https://msdn.microsoft.com/library/windows/hardware/hh450858)を防ぐため、その他の要求をターゲット デバイス関連のないバスへのアクセスが、シーケンス内の転送間隔で発生しているからです。 次に、クライアントが送信[ **IRP\_MJ\_読み取り**](https://msdn.microsoft.com/library/windows/hardware/ff550794)と[ **IRP\_MJ\_書き込み**](https://msdn.microsoft.com/library/windows/hardware/ff550819)シーケンス内の転送を実行する要求。 クライアントの最後に、送信、 [ **IOCTL\_SPB\_UNLOCK\_コント ローラー** ](https://msdn.microsoft.com/library/windows/hardware/hh450859)ロックを解除する要求。

クライアントは、後での転送シーケンスで以前の転送に依存している場合、この種類の I/O 転送シーケンスを実装する必要があります。 たとえば、最初の読み込みでは、その後読み取りまたは書き込みを複数のバイト数を可能性があります。 このような依存関係が存在しない場合、ただし、クライアントが送信する必要があります、 [ **IOCTL\_SPB\_EXECUTE\_シーケンス**](https://msdn.microsoft.com/library/windows/hardware/hh450857) SPB コント ローラーのドライバーを要求することができますシーケンスをより効率的に実行します。

間、 **IOCTL\_SPB\_ロック\_コント ローラー**クライアント実装のシーケンスでは、開始要求と**IOCTL\_SPB\_ロックの解除\_コント ローラー** 、シーケンスを終了する要求、クライアントは、ターゲット デバイスに送信できる唯一の I/O 要求は**IRP\_MJ\_読み取り**と**IRP\_MJ\_書き込み**要求。 このルールの違反は、エラーです。

SPB ロックは、読み取りと書き込みのシーケンスが、バスのアトミック操作として実行され、その目的専用に使用する必要がありますの保証にのみ使用されます。

詳細については、[Handling Client-Implemented シーケンス](https://msdn.microsoft.com/library/windows/hardware/jj191736)を参照してください。

 

 




