---
title: アプリケーションの要求が完了しない理由を判断します。
description: このトピックでは、ユーザー モード ドライバー フレームワーク (UMDF) のバージョン 1 または 2 ドライバーと組み合わせて Wudfext.dll デバッガー拡張機能を使用してアプリケーションの要求が完了しない理由を判断する方法について説明します。
ms.assetid: 33a09277-1e00-4f91-b2ab-b2541091628f
keywords:
- UMDF WDK、アプリケーションの要求が完了していません。
- デバッグ シナリオ WDK UMDF、アプリケーションの要求が完了していません。
- UMDF WDK、デバッグ シナリオでは、アプリケーションの要求が完了していません。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bba49a3e241cc54caab7fd4de1f7f4d4caa7f824
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536256"
---
# <a name="determining-why-an-application-request-does-not-complete"></a>アプリケーションの要求が完了しない理由を判断します。


このトピックでは、ユーザー モード ドライバー フレームワーク (UMDF) のバージョン 1 または 2 ドライバーと組み合わせて Wudfext.dll デバッガー拡張機能を使用してアプリケーションの要求が完了しない理由を判断する方法について説明します。

UMDF バージョン 1、wudfext.dll で実装された拡張機能のコマンドを使用します。 UMDF バージョン 2 以降、wdfkd.dll で実装された拡張機能のコマンドを使用します。

アプリケーションの要求が完了しない理由を判断するには、次の手順を実行できます。

1.  使用[ **! wudfext.umirps** ](https://msdn.microsoft.com/library/windows/hardware/ff566197) (UMDF 1) または[ **! wdfkd.wdfumirps** ](https://msdn.microsoft.com/library/windows/hardware/dn265384) (UMDF 2) すべてのユーザー モードの未処理 I/O 要求パケット (を表示するにはIrp)、ホスト プロセスでします。 各ユーザー モード IRP の情報には、ユーザー モード IRP が作成された元のカーネル モード IRP が含まれています。

    アプリケーションで発生した IRP がカーネル モードに対応するユーザー モード IRP を決定します。

2.  使用[ **! wudfext.umirp** ](https://msdn.microsoft.com/library/windows/hardware/ff566195) (UMDF 1) または[ **! wdfkd.wdfumirp** ](https://msdn.microsoft.com/library/windows/hardware/dn265383) (UMDF 2) 特定のユーザー モード IRP に関する情報を取得します。

    ユーザー モード IRP の情報には、スタック内の場所が含まれます。 スタックの場所がわかっている場合、IRP が処理されているかを確認できます。 スタックの場所 0 は、UMDF (カーネル モード スタックまたは Microsoft Win32 や Winsock など、サブ システム) の下にあるスタックを表します。

3.  IRP がドライバーの層にある場合 (には、ドライバーが IRP を処理するレイヤーでは、)、次の手順に従います。
    1.  ドライバーのレイヤーで設定されている I/O キューを表示します。 使用することができます[ **! wudfext.wudfdevicequeues** ](https://msdn.microsoft.com/library/windows/hardware/ff566203) (UMDF 1) または[ **! wdfkd.wdfdevicequeues** ](https://msdn.microsoft.com/library/windows/hardware/ff565715) (UMDF 2) に設定されているすべての I/O キューの表示ドライバーのレイヤーでセットアップします。 使用することも[ **! wudfext.wudfqueue** ](https://msdn.microsoft.com/library/windows/hardware/ff566223) (UMDF 1) または[ **! wdfkd.wdfqueue** ](https://msdn.microsoft.com/library/windows/hardware/ff566118) (UMDF 2) 特定のキューに関する情報を取得します。

    2.  未処理要求が複数ある場合は、使用[ **! wudfext.wudfrequest** ](https://msdn.microsoft.com/library/windows/hardware/ff566226) (UMDF 1) または[ **! wdfkd.wdfrequest** ](https://msdn.microsoft.com/library/windows/hardware/ff566119) (UMDF 2) にを基になるユーザー モード IRP を含む要求に関する情報を取得します。 ユーザー モードの IRP 情報からは、興味のある要求を指定できます。
    3.  キューまたはドライバーに要求を所有するかどうかを確認します。 出力の一部としてこの情報が表示される[ **! wudfext.wudfqueue** ](https://msdn.microsoft.com/library/windows/hardware/ff566223)または[ **! wdfkd.wdfqueue**](https://msdn.microsoft.com/library/windows/hardware/ff566118)します。 キューまたはドライバーが要求を所有しているかどうかに応じて、次の確認のいずれかを実行します。
        -   キューによって、要求を所有している場合は、なぜキューが配信されなかった要求にドライバーを決定するキューの状態を確認します。
        -   ドライバーによって、要求を所有している場合は、スレッドがスタックしているか、要求の処理中にデッドロックかどうかを決定する、ホスト プロセスでスレッドを確認します。

4.  IRP が UMDF ドライバーのもう 1 つの層である場合は、そのレイヤーの前の手順を繰り返すことができます。 使用できることに注意してください[ **! wudfext.umdevstack** ](https://msdn.microsoft.com/library/windows/hardware/ff566189) (UMDF 1) または[ **! wdfkd.wdfumdevstack** ](https://msdn.microsoft.com/library/windows/hardware/dn265379)すべてに関する情報を表示する (UMDF 2)。スタック レイヤー。

5.  IRP が (たとえば、スタックの場所 0 の場合、IRP が現在処理中) UMDF のスタック以外の場合は、対応するカーネル モード IRP が完了しなかった理由を確認します。

 

 





