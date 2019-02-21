---
title: ビデオの UMDF ドライバーのデバッグ
description: このトピックには、一連ユーザー モード ドライバー フレームワーク (UMDF) ドライバーをデバッグする方法を示す Abhishek Ram でビデオにはが含まれています。
Search.SourceType: Video
ms.assetid: 969FD292-5D92-4257-8E15-F2129B832E22
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7d0431ca0b13cbd247d35a55eeae2c6f70519fc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531159"
---
# <a name="videos-debugging-umdf-drivers"></a>ビデオ:UMDF ドライバーのデバッグ


このトピックには、一連ユーザー モード ドライバー フレームワーク (UMDF) ドライバーをデバッグする方法を示す Abhishek Ram でビデオにはが含まれています。

後は、ビデオは、UMDF デバッガー拡張機能を熟知し、基本的なデバッグ シナリオで使用する方法を理解します。

ビデオでは、以前のバージョンの Windows バージョン 1 UMDF ドライバーのデバッグを示すため、中に、同じ手法を使用する現在のバージョンの Windows で実行されている UMDF バージョン 2 のドライバーを使用したことができます。

**注**  このビデオが Wudfext.dll、UMDF バージョン 1 のドライバーのみをデバッグするために使用できるデバッガー拡張機能のコマンドについて説明します。 UMDF バージョン 2.0 以降 UMDF ドライバーをデバッグするには、Wdfkd.dll デバッガー拡張ライブラリを使用すると、代わりに使用する必要があります。 Wudfext.dll で拡張機能のすべての Wdfkd.dll には、対応があります。 詳細については、次を参照してください。 [Wudfext.dll でデバッガー拡張の概要](using-umdf-debugger-extensions.md)と[Wdfkd.dll でデバッガー拡張の概要](debugger-extensions-for-kmdf-drivers.md)します。

 

UMDF のデバッグの詳細については、記載されたトピックを参照してください。[デバッグ WDF ドライバー](debugging-a-wdf-driver.md)します。

## <a name="prerequisites"></a>前提条件


このコンテンツを最大限に活用するには、UMDF と、デバッグ ツールの Windows の実用的な知識があります。 各セッションは、1 つ前のビルド、ために、表示されている順序でこれらのデモを表示することをお勧めします。

## <a name="basics-and-setup"></a>基本とセットアップ


WDK サンプルと、OSR usb-fx2 Learning Kit の使用について説明します。

>[!VIDEO https://www.microsoft.com/videoplayer/embed/d1040a16-81ec-40bb-a2d5-05021a37a144]

このビデオでは、UMDF デバッグの基礎、テスト コンピューターの準備など、Devcon ツールを使用して、WdfVerifier を使用して、指定された UMDF ドライバーをホストしている、アタッチ WdfVerifier を使用して、ホスト プロセスを識別する、UMDF Echo サンプル ドライバーをインストールするについて説明します初期化コードをデバッグするデバッガーを時間でのホスト プロセス。 このビデオでは、タスク マネージャー、およびドライバーのデバイス マネージャーでを実行しているビューで実行中のホスト プロセスを表示する方法についても説明します。

## <a name="examining-the-object-hierarchy-with-debugger-extensions"></a>デバッガーの拡張子を持つオブジェクトの階層を調べる

>[!VIDEO https://www.microsoft.com/videoplayer/embed/da033b03-b965-40cc-9697-ecb97430006a]

この部分では、UMDF ドライバーのデバッグを開始する方法を学習します。 ビデオでは、アプリの 3 つのインスタンスが、ドライバーを読み取り、書き込み、およびデバイスの I/O 制御要求を送信するため、OSR usb-fx2 ドライバーのサンプルとアプリケーションのサンプルを設定する方法について説明します。 要求フロー最初、reflector してから、ユーザー モード ドライバーのホスト プロセスにする方法を確認します。 このビデオでは、FX2 ドライバー サンプルでは、WDF オブジェクト階層が導入されていて、次の UMDF デバッガー拡張機能を使用して、UMDF オブジェクト階層を移動する方法について説明します。

-   [**!wudfext.umdevstacks**](https://msdn.microsoft.com/library/windows/hardware/ff566191)
-   [**!wudfext.wudfdriverinfo**](https://msdn.microsoft.com/library/windows/hardware/ff566207)
-   [**!wudfext.wudfdevice**](https://msdn.microsoft.com/library/windows/hardware/ff566199)
-   [**!wudfext.wudfdevicequeues**](https://msdn.microsoft.com/library/windows/hardware/ff566203)

UMDF 2 では、次を参照してください。 [Wdfkd.dll でデバッガー拡張の概要](debugger-extensions-for-kmdf-drivers.md)、たとえば[ **! wdfkd.wdfumdevstacks**](https://msdn.microsoft.com/library/windows/hardware/dn265380)します。

## <a name="accessing-framework-usb-objects"></a>Framework USB オブジェクトへのアクセス

>[!VIDEO https://www.microsoft.com/videoplayer/embed/f22577ab-1da0-47ae-b12b-ed3d586cde9e]

ここでは、ドライバーの framework USB オブジェクトを確認する方法を学びます。 これを行うには、USB パイプ オブジェクト、USB インターフェイス オブジェクト、および USB I/O ターゲット オブジェクトに到達する WDF オブジェクト階層をナビゲートします。

##  <a name="io-requests-and-queues"></a>I/O 要求とキュー

>[!VIDEO https://www.microsoft.com/videoplayer/embed/48165551-a75d-4855-b0c8-3e55826f4f5e]

このビデオでは、ドライバーのフレームワークの I/O 要求オブジェクトとフレームワークのキュー オブジェクトを確認するのにデバッガーを使用します。

## <a name="file-objects-and-callback-objects"></a>ファイル オブジェクトとコールバック オブジェクト

>[!VIDEO https://www.microsoft.com/videoplayer/embed/39c05ac7-3e20-4b8d-bcc9-37f450ddf507]

この部分では、framework のファイル オブジェクトと、ドライバーのコールバック オブジェクトを確認する方法を学習します。

##  <a name="tracking-io-requests-sent-by-a-umdf-driver"></a>UMDF ドライバーから送信された I/O 要求の追跡

>[!VIDEO https://www.microsoft.com/videoplayer/embed/8d1aa0a2-4360-4d68-9b09-310851a6087f]

ここでは、デバッグに役立つアプリケーション検証ツールを使用する方法を学びます。 ドライバーの初期化コードをデバッグする方法と、カーネル スタックを下に UMDF ドライバーによって送信された要求を追跡する方法も学習します。

##  <a name="driver-does-not-complete-an-io-request"></a>ドライバーは、I/O 要求を完了できません。

>[!VIDEO https://www.microsoft.com/videoplayer/embed/ddf4eff2-73f9-44a9-8602-adb08fc48373]

最後のビデオでは、UMDF ドライバーは、受信要求を完了しなかったときに、ケースを調査して、framework のオブジェクトの追跡と追跡機能の参照について説明します。

 

 





