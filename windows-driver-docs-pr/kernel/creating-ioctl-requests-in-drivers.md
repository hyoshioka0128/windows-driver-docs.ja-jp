---
title: ドライバーの IOCTL 要求の作成
description: ドライバーの IOCTL 要求の作成
ms.assetid: 155e2577-0e9a-4c0b-a25a-8516ce3de631
keywords:
- 要求の作成、I/O 制御コード WDK カーネル
- 制御コード WDK Ioctl、要求の作成
- Ioctl WDK カーネル、要求の作成
- WDK Irp の同期
- 埋め込みポインター WDK Ioctl
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7484e66ea127da239c2c080d460c463d3f3b62d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560597"
---
# <a name="creating-ioctl-requests-in-drivers"></a>ドライバーの IOCTL 要求の作成





クラス ドライバーまたはその他の高度なドライバーは Irp をコントロールの I/O 要求を割り当てるし、次のように、次の下位ドライバーに送信。

1.  割り当てまたは I/O 要求パケットを再利用 ([**IRP**](https://msdn.microsoft.com/library/windows/hardware/ff550694)) メジャーの関数コードで[ **IRP\_MJ\_デバイス\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550744)または[ **IRP\_MJ\_内部\_デバイス\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550766)します。 使用することができます、 [ **IoBuildDeviceIoControlRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548318)ルーチンを具体的には、IOCTL IRP を割り当てます。 など、汎用的な IRP の作成と初期化ルーチンを使用することもできます[ **IoAllocateIrp**](https://msdn.microsoft.com/library/windows/hardware/ff548257)、 [ **IoReuseIrp**](https://msdn.microsoft.com/library/windows/hardware/ff549661)、または。[**IoInitializeIrp**](https://msdn.microsoft.com/library/windows/hardware/ff549315)します。 IRP の割り当ての詳細については、次を参照してください。[下位レベルのドライバーの作成の Irp](creating-irps-for-lower-level-drivers.md)します。

2.  IOCTL で IRP の下位のドライバーの I/O スタックの場所を設定\_*XXX*パラメーターを適切なコードをしています。

3.  IOCTL 要求を非同期的に完了する場合は、呼び出し、 [ **KeInitializeEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff552137)ルーチンを通知イベントとイベント オブジェクトを初期化します。 ドライバーでは、このイベントを使用して、I/O 操作を完了するまで待ちます。

4.  呼び出す[ **IoSetCompletionRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff549679) IRP が上のドライバーが提供できるように、 [ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)ルーチン、必要に応じて、実行するには次:

    -   下位のドライバーが、特定の要求を処理する方法を決定します。

    -   IRP 別の送信を要求または下位のドライバーが要求された操作が完了したら破棄 IRP がドライバーを作成、再利用します。 ドライバーは Irp を再利用できませんを[ **IoBuildDeviceIoControlRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548318)を作成します。 詳細については、次を参照してください。 [Irp の再利用](reusing-irps.md)します。

5.  呼び出す[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)から下位のドライバーに要求を渡します。

6.  場合[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)ステータスを返します\_保留中の呼び出し、 [ **kewaitforsingleobject の 1** ](https://msdn.microsoft.com/library/windows/hardware/ff553350)ルーチンを現在の配置スレッド待機状態にします。 ドライバーの設定、ルーチンの*オブジェクト*パラメーターへの呼び出しで初期化されたイベント オブジェクトのアドレスを[ **KeInitializeEvent**](https://msdn.microsoft.com/library/windows/hardware/ff552137)します。

    **注**ドライバーを呼び出す場合[ **kewaitforsingleobject の 1** ](https://msdn.microsoft.com/library/windows/hardware/ff553350)でその*タイムアウト*パラメーターはいずれかに設定**NULL**または、ドライバー、0 以外の値を格納する変数のアドレスは、IRQL で実行する必要があります&lt;APC を =\_nonarbitrary スレッド コンテキストでします。 IRQL でドライバーを実行する必要がありますそれ以外の場合、 &lt;= ディスパッチ\_レベル。




によって、イベントがシグナル状態その[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)ルーチン IOCTL 要求が完了するとします。 イベントがシグナル状態のスレッドが実行を再開します。

**重要な**、ドライバーが、スタック上のローカル変数として、イベント オブジェクトを割り当てた場合、ドライバーを呼び出す必要があります[ **kewaitforsingleobject の 1** ](https://msdn.microsoft.com/library/windows/hardware/ff553350)でその*WaitMode*パラメーターに設定**kernelmode である**します。 このパラメーターの値は、スタックがページ アウトされていることを防ぎます。




同期の問題と可能なアクセス違反を避けるため、I/O 制御コードのパラメーターには、埋め込みポインターにはほとんどが含まれます。 特定の SCSI の要求でバッファーを除く*Irp*-&gt;**AssociatedIrp**.**SystemBuffer**で*Irp*-&gt;**MdlAddress**、および**パラメーター**.**DeviceIoControl**.**Type3InputBuffer**ドライバーの I/O スタック内の場所にが含まれていないその他のデータ バッファーへのポインターにはも I/O 制御コードのシステム定義のポインターを格納する構造体を格納しないでください。 I/O の Irp でのデータ バッファーの使用方法の詳細については、制御コードを参照してください[I/O 制御コードの説明をバッファー](buffer-descriptions-for-i-o-control-codes.md)します。

それにもかかわらず、内部の I/O 制御コードを定義するクラス/ポート ドライバーのペアは、下位レベルのドライバーにより高度なドライバーから、ドライバーによって割り当てられたメモリに埋め込みポインターを渡すことができます。 クラス/ポート ドライバーのようなペアは、次が true であることを保証します。

-   一度に 1 つだけのドライバーは、データにアクセスできます。

-   プライベート データ バッファーは、ポート ドライバーによって任意のスレッド コンテキストでアクセスできます。

ディスプレイ ドライバーは、GDI 関数を呼び出すことができます[ **EngDeviceIoControl** ](https://msdn.microsoft.com/library/windows/hardware/ff564838)を介してシステム定義されたパブリック I/O 制御要求と同様に、個別に定義されたデバイスに固有の I/O 制御の要求を送信する、対応するアダプター固有のシステムのビデオ ポート ドライバー[ビデオのミニポート ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff570509)します。

ドライバー パッケージのすべてのユーザー モード コンポーネントを呼び出すことができます[ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363216)ドライバー スタックにコントロールの I/O 要求を送信します。 I/O マネージャーを作成、 [ **IRP\_MJ\_デバイス\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550744)を要求し、最上位レベルのドライバーに配信します。








