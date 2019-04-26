---
title: 汎用ドライバーのサンプル
description: このディレクトリにサンプルでは、デバイス用のカスタム ドライバーを記述するための開始点を提供します。
ms.assetid: C5DC72F1-D093-47D0-9AC3-680878C5A868
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7660536daeff45e57cf012ca7aa791c59ac9c664
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356754"
---
# <a name="general-driver-samples"></a>汎用ドライバーのサンプル


このディレクトリにサンプルでは、デバイス用のカスタム ドライバーを記述するための開始点を提供します。

## <a name="general-samples"></a>一般的なサンプル


| サンプル名                     | ソリューション                                                              | 説明                                                                                                                                                                                                                                        |
|---------------------------------|-----------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 安全な IRP のキューをキャンセルします。           | [cancel](https://go.microsoft.com/fwlink/p/?LinkId=617705)             | キャンセルの安全なキュー ルーチン IoCsqInitialize、IoCsqInsertIrp、IoCsqRemoveIrp、IoCsqRemoveNextIrp の使用を示します。 これらのルーチンを使用すると、ドライバーの開発者は IRP キャンセル競合状態について心配ありません。                |
| KMDF エコー                       | [kmdfecho](https://go.microsoft.com/fwlink/p/?LinkId=617706)           | 読み取りをシリアル化および書き込み要求、ドライバーに提示する連続したキューを使用する方法を示します。                                                                                                                                           |
| UMDF エコー                       | [echo](https://go.microsoft.com/fwlink/p/?LinkId=617707)               | ドライバーを作成し、ベスト プラクティスを採用する UMDF 1 を使用する方法を示します。                                                                                                                                                                     |
| UMDF2 エコー                      | [umdf2echo](https://go.microsoft.com/fwlink/p/?LinkId=617708)          | ドライバーを作成し、ベスト プラクティスを採用する UMDF 2 を使用する方法を示します。                                                                                                                                                                     |
| UMDF SocketEcho                 | [umdfsocketecho](https://go.microsoft.com/fwlink/p/?LinkId=617709)     | UMDF を使用してドライバーを作成する方法とベスト プラクティスについて説明します。                                                                                                                                                                |
| ハードウェア イベント                  | [eventsample](https://go.microsoft.com/fwlink/p/?LinkId=617711)        | ハードウェア イベントに関するをアプリケーションに通知できる 2 つの方法はカーネル モード ドライバーを示します。 1 つの方法は、イベント ベースのメソッドを使用して他のメソッドを使用して、IRP ベースします。 ドライバーのサンプルでは、DPC タイマーを使用して、ハードウェアのイベントをシミュレートします。 |
| ファイル履歴                    | [filehistory](https://go.microsoft.com/fwlink/p/?LinkId=617712)        | 定期的なバックアップのスケジュールが停止している場合は、ファイル履歴、サービスを開始するコンソール アプリケーションを指定します。                                                                                                                                       |
| WDF のインストール パッケージ        | [installwdf](https://go.microsoft.com/fwlink/p/?LinkId=617713)         | WDF のパッケージをシステムにインストールする方法を示します。 このコードとして使用できます-ユーザー システムに必要な WDF コンポーネントをインストールすることです。 サンプル コードより優れたエクスペリエンスを提供する既存のセットアップ アプリケーションにもやり直すことができます。 |
| 非 PnP ドライバーのサンプル           | [ioctl](https://go.microsoft.com/fwlink/p/?LinkId=620307)              | カーネル モード ドライバー フレームワークを使用して、非 PnP ドライバーを作成する方法を示します。                                                                                                                                                                 |
| IOCTL                           | [ioctl](https://go.microsoft.com/fwlink/p/?LinkId=617715)              | Ioctl の 4 つのさまざまな種類の使用方法を示します (メソッド\_IN\_ダイレクト、メソッド\_アウト\_ダイレクト、メソッド\_NEITHER、およびメソッド\_バッファーに格納された)。                                                                                                         |
| ObCallback                      | [obcallback](https://go.microsoft.com/fwlink/p/?LinkId=617716)         | プロセスの保護のための登録済みのコールバックの使用について説明します。 ドライバーは、プロセスの作成時と呼ばれるコントロールのコールバックを登録します。                                                                                                  |
| PCIDRV                          | [pcidrv](https://go.microsoft.com/fwlink/p/?LinkId=617717)             | このサンプルでは、PCI デバイス KMDF ドライバーを作成する方法を示します。 Intel 82557/82558 でサンプルの動作は、PCI Ethernet アダプター (10/100) および Intel 互換に基づいています。                                                                       |
| カーネルのカウンター                  | [kcs](https://go.microsoft.com/fwlink/p/?LinkId=617718)                | カーネル モードのパフォーマンスのライブラリの使用を示します。 ドライバーは、任意のハードウェアを制御しません単に、カウンターを提供します。 コードには、各関数が何を説明するコメントが含まれています。                                                 |
| PLX9x5x PCI ドライバ              | [PLX9x5x](https://go.microsoft.com/fwlink/p/?LinkId=617719)            | Windows Driver Frameworks (WDF) を使用してジェネリック PCI デバイス ドライバーを作成する方法を示します。 このドライバーのターゲット ハードウェアは、PLX9656/9653RDK LITE の基盤です。                                                                                |
| RegFltr                         | [regflltr](https://go.microsoft.com/fwlink/p/?LinkId=617720)           | レジストリのフィルター ドライバーを作成する方法を示します。                                                                                                                                                                                                       |
| DMA システム                      | [SystemDma](https://go.microsoft.com/fwlink/p/?LinkId=617722)          | V3 システム DMA の使用状況を示します。 どのドライバーは、DMA を使用してハードウェアの場所にデータを書き込むの Windows でサポートされているシステム DMA コント ローラーを使用可能性がありますが表示されます。                                                                              |
| トースター ドライバーのサンプル           | [トースター](https://go.microsoft.com/fwlink/p/?LinkId=620309)            | 反復的な一連のカーネル モード ドライバー フレームワーク (KMDF) とユーザー モード ドライバー フレームワーク (UMDF) バージョン 1 の両方の Windows ドライバー開発の基本的な側面を示すサンプルです。                                                    |
| トースター パッケージ サンプル          | [toastpkg](https://go.microsoft.com/fwlink/p/?LinkId=617723)           | トースター サンプル ドライバーの優先ハードウェアとソフトウェア最初のインストールをシミュレートします。                                                                                                                                                             |
| トースター サンプル (UMDF バージョン 2) | [umdf2toaster](https://go.microsoft.com/fwlink/p/?LinkId=620310)       | 反復的な一連のユーザー モード ドライバー フレームワーク (UMDF) バージョン 2 を使用して Windows ドライバー開発の基本的な側面を示すサンプルです。                                                                                               |
| EventDrv                        | [evntdrv](https://go.microsoft.com/fwlink/p/?LinkId=617724)            | カーネル モード トレース プロバイダーとドライバー。 ドライバーは、任意のハードウェアを制御しません単に、トレース イベントを生成します。 Event Tracing for Windows (ETW) API、ドライバーの使用を示すために設計されています。                                 |
| システム トレース コントロール            | [SystemTraceControl](https://go.microsoft.com/fwlink/p/?LinkId=617725) | システム トレース プロバイダーからイベントを収集するイベント トレース管理 Api を使用する方法を示します。                                                                                                                                               |
| tracedrv                        | [tracedrv](https://go.microsoft.com/fwlink/p/?LinkId=617726)           | ソフトウェア トレース用にインストルメント化サンプル ドライバー。                                                                                                                                                                                                 |
| UMDF ドライバーのスケルトン            | [umdfSkeleton](https://go.microsoft.com/fwlink/p/?LinkId=617727)       | 最小限のドライバーを作成するために、ユーザー モード ドライバー フレームワークを使用する方法について説明し、ベスト プラクティスを示します。                                                                                                                                         |

 

 

 




