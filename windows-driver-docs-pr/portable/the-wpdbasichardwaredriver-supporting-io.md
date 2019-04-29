---
Description: I/O のサポート
title: I/O のサポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 798e00df7061e57ca8f86d1bdc531b5a6a7c0993
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387352"
---
# <a name="supporting-io"></a>I/O のサポート


ドライバーのサンプルは、rs-232 接続を使用して Parallax の基本的なスタンプ マイクロ コント ローラーと通信します。

マイクロ コント ローラーは、定期的なセンサーの読み取りを送信し、転送間隔を更新するドライバーから入力のコマンドを受信するようにプログラミングします。

次の図は、ドライバーのサンプルと、基本的なスタンプのユニット間のデータ フローを示します。 デモのために、基本的なスタンプ ファームウェアは非常に単純なプロトコルを使用してセンサー データを更新します。

-   基本的なスタンプでは、マルチバイト データ パケットを送信で構成されると、ドライバーに*n*-センサーの読み取りおよび更新間隔を 5 バイトのバイト数。 データは、ANSI 文字で終端の null 文字を使用せず、SEROUT コマンドを使用して送信されます。 更新間隔は、次のデータ パケットが送信され、既定では 02000 (2 秒) までの時間をミリ秒単位の経過を定義します。
-   サンプル ドライバーを更新する間隔を動的に構成するには、終端の null 文字を ANSI 文字で新しい更新間隔を含む 6 バイトのデータ パケットを送信できます (05000 など\\0)。 終端の null 文字は、基本的なスタンプ プログラム SERIN コマンドを使用してデータを受信する必要があります。

![データ フローの i/o](images/wpd_overview_new.png)

ドライバーのサンプルでは、UMDF ホスト プロセス (図 WUDF) でホストされているし、WPD アプリケーションからコマンドを受信します。 ドライバーは、UMDF ファイル ハンドルの I/O のターゲット オブジェクトを使用して、rs-232 ポートを使用してデータを交換します。

I/O ターゲットの管理と完了コールバック ルーチンは RS232Target オブジェクトで実装され、次の手順が含まれます。

1.  初期化時に**WpdBaseDriver::Initialize**ドライバーは、既定のポートとして COM1 を使用して、rs-232 接続設定を構成します。 Rs-232 に固有のセットアップ コードが実装された、 **RS232Connection**オブジェクト。
2.  ドライバーのサンプルは、呼び出すことによって、COM1 に接続する**CreateFileW** rs-232 ポートへのハンドルを取得します。
3.  ドライバーのサンプルを使用して**IWDFFileHandleTargetFactory::CreateFileHandleTarget**ファイル ハンドルに基づく I/O ターゲット オブジェクトを作成し、COM1 手順 2. で取得されたハンドルに割り当てます。 このセットアップ コードは、 **RS232Target::Create**メソッド。
4.  ドライバーのサンプルが I/O ターゲットで起動 I/O ターゲットを作成すると後、 **IPnpCallback::OnDOEntry**呼び出して**RS232Target::Start**します。 ターゲットは、要求を処理する準備ができて、ドライバーに最初の非同期読み取り要求を送信します。 ドライバーは、更新間隔のプロパティを変更するには、アプリケーションからコマンドを受信するたびにも非同期書き込み要求を送信します。
5.  ドライバーがない (たとえば、devnode がデバイス マネージャーを無効にした場合)、初期化された**IPnpCallback::OnD0Exit**呼びますサンプル ドライバーは呼び出すことによって、I/O ターゲットを停止および**RS232Target::Stop**. ターゲットに、保留中の I/O 要求がある場合、自動的に取り消されます UMDF で。

RS232 の読み取り要求は、次の手順で示すように実装されます。

1.  生成される**RS232Target::SendReadRequest**として**IWDFIoRequest**オブジェクト
2.  使用して初期化される**IWDFIoTarget::FormatRequestForRead**と
3.  使用して転送される**IWDFIoRequest::Send**します。

**RS232Target::OnCompletion**コールバック ルーチンは、要求データを処理し、次の読み取り要求を送信します。

RS232 書き込み要求は、次の一覧に示すように実装されます。

1.  生成される**RS232Target::SendWriteRequest**として**IWDFIoRequest**オブジェクト
2.  使用して初期化される**IWDFIoTarget::FormatRequestForWrite**と
3.  使用して転送される**IWDFIoRequest::Send**します。

アプリケーションが、センサーを設定するときに\_UPDATE\_間隔プロパティの値、 **WpdObjectProperties::OnSetPropertyValues**コマンド ハンドラーが、ヘルパー関数を呼び出す**WpdObjectProperties::SendUpdateIntervalToDevice**であり、さらにこの**RS232Target::SendWriteRequest**します。

UMDF I/O ターゲットは、状態管理とエラー処理を含む、複数の利点を提供しより簡単かつより堅牢なドライバーのコードにします。 UMDF I/O ターゲットより高度なドライバーのシナリオまたはスタックの構成は、キャンセル、キューの要求、および [次へ] の下のドライバーに要求の転送をネイティブ サポートします。

サンプル ドライバーの場合はユーザーの体感パフォーマンス オーバーヘッド UMDF ファイル I/O ターゲット オブジェクトのハンドル ベースを Microsoft Win32® Api の代わりに使用する場合。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


****
[WpdBasicHardwareDriverSample](the-wpdbasichardwaredriver-sample.md)

[WPD ドライバーのサンプル](the-wpd-driver-samples.md)

 

 





