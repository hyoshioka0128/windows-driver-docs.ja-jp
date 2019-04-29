---
Description: サンプル ドライバーのテストとデバッグ
title: サンプル ドライバーのテストとデバッグ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f54469f5c79fb6c1967aa016a1f2c6faac5add13
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387305"
---
# <a name="testing-and-debugging-the-sample-driver"></a>サンプル ドライバーのテストとデバッグ


WDK には、テストおよびデバッグ WPD ドライバーを使用できる 3 つのツールが含まれています。 これらのツールは、次の表で説明します。

|                          |                                                                                                                                                                                                                  |
|--------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ツール                     | 説明                                                                                                                                                                                                      |
| *WpdInfo.exe*            | このツールを開くか、デバイスを閉じる、作成またはデバイス、表示がサポートされているコマンド、コマンドを発行上のオブジェクトを削除、イベントの表示、読み取り可能なプロパティの値を取得および書き込み可能なプロパティ値を設定します。 |
| *WpdDeviceInspector.exe* | デバイスの機能とコンテンツを表す HTML レポートを生成します。                                                                                                                                     |
| *WpdMon.exe*             | メッセージと WPD ドライバーと、オペレーティング システムまたは WPD アプリケーション間で渡されるコマンドをトレースします。                                                                                                 |

 

これらのツールとその使用の詳細については、次を参照してください。 [WPD ドライバーの開発ツール](familiarizing-yourself-with-the-sample-driver.md)WDK ドキュメント。

## <a name="span-idtrackingthesensorreadingeventbyusingwpdinfoexespanspan-idtrackingthesensorreadingeventbyusingwpdinfoexespantracking-the-sensor-reading-event-by-using-wpdinfoexe"></a><span id="tracking_the_sensor_reading_event_by_using_wpdinfo.exe"></span><span id="TRACKING_THE_SENSOR_READING_EVENT_BY_USING_WPDINFO.EXE"></span>WpdInfo.exe を使用して、センサー読み取りイベントを追跡します。


開始する前に*WpdInfo.exe*、WpdInfo.Properties ファイル、センサー、PROPERTYKEYs をマップするエントリを更新\_読み取りとセンサー\_更新\_間隔プロパティを対応するフレンドリ文字列。

```ManagedCPlusPlus
{a7ef4367-6550-4055-b66f-be6fdacf4e9f}.2, SENSOR_READING, VT_UI8
{a7ef4367-6550-4055-b66f-be6fdacf4e9f}.3, SENSOR_UPDATE_INTERVAL, VT_UI4
```

WpdInfo.Properties ファイルが同じフォルダーに見つかった*WpdInfo.exe*します。 このファイルが存在しない場合は、実行*WpdInfo.exe*それを生成する 1 つの時間。

開始すると*WpdInfo.exe*、インストールされている WPD デバイスの一覧からポータブル デバイスを選択するよう求められます。 センサー デバイスを選択した後、ツールは、そのウィンドウの下のウィンドウでイベントを記録します。

![wpd 情報ツール](images/wpdinfo_temphumidity_object.png)

前の例では、センサー読み取りイベントが発生した、ときに、次の情報が true:

-   センサー読み取りプロパティ、センサー\_2170720417 を読み取り、でした。 この値は、(Sensiron 気温・湿度センサーに対応します) を 2 に、センサーの識別子を示します。 1 つの要素、1 つの要素の 7 バイトのサイズ、72.0 の華氏の気温の数および 41.7% の相対湿度。
-   その間隔のプロパティ、センサー\_更新\_間隔、2,000 に設定されています。

## <a name="span-idupdatingtheintervalpropertybyusingwpdinfoexespanspan-idupdatingtheintervalpropertybyusingwpdinfoexespanupdating-the-interval-property-by-using-wpdinfoexe"></a><span id="updating_the_interval_property_by_using_wpdinfo.exe"></span><span id="UPDATING_THE_INTERVAL_PROPERTY_BY_USING_WPDINFO.EXE"></span>WpdInfo.exe を使用して、間隔のプロパティを更新しています


センサー、間隔のプロパティを変更するツールを使用するには、視差 BS2 センサー デバイスを選択したら\_UPDATE\_ 2 ~ 60 秒間、別の値を 2,000 ミリ秒の既定値からの間隔。

1.  最初の手順では、そのオブジェクトの値すべてのプロパティを表示するウィンドウを列挙体から TempHumidity 機能オブジェクトを選択することが必要です。 一番左のウィンドウでデバイス オブジェクトの直接の子としては、このオブジェクトを見つけることができます。
2.  次をクリックする**センサー\_更新\_間隔**を開いて、**編集**、VT として、新しい値を入力 ダイアログ ボックスで、\_UI4 型。

![wpd 情報ツール](images/wpdinfo_interval.png)

値の許容範囲では、02000 ~ 60000、包括的です。 をクリックして**OK**、新しい間隔プロパティの値は、デバイスに送信されます。 イベント ペインを確認し、イベントのパラメーターに新しい更新間隔の値に到着したイベントを確認できます。

## <a name="span-iddebuggingthedriverwithvisualstudio8spanspan-iddebuggingthedriverwithvisualstudio8spanspan-iddebuggingthedriverwithvisualstudio8spandebugging-the-driver-with-visual-studio-8"></a><span id="Debugging_the_Driver_with_Visual_Studio_8"></span><span id="debugging_the_driver_with_visual_studio_8"></span><span id="DEBUGGING_THE_DRIVER_WITH_VISUAL_STUDIO_8"></span>Visual Studio 8 を使用したドライバーのデバッグ


WPD ドライバーは、Windows Driver Frameworks (WDF) UMDF プラットフォームに基づいています。 UMDF ドライバーより安定性とセキュリティ、ほかのカーネル モード ドライバーよりも、同等のパフォーマンスを提供します。 また、UMDF ドライバーは、Visual Studio 8 などのユーザー モード デバッガーの使用を許可します。 ユーザー モードでのドライバーのデバッグは、エラーは、コンピューター全体ではなく、現在のプロセスのみに影響するために、カーネル モードでデバッグするよりも高速にする傾向があります。

ドライバーをインストールした後は、次の手順に従って Visual Studio 8 デバッグ プロジェクトを作成できます。

1.  管理者特権 (管理者として実行) で Visual Studio 8 を開き、ファイルに移動します&lt;新規&gt;プロジェクト既存のコード パスから。
    **注**  LocalService アカウントがこれらの特権を必要とするために、昇格した特権で Visual Studio 8 を開く必要があります。 WUDFHost プロセスは、LocalService アカウント内で実行されます。 Visual Studio 8 を使用して、ドライバーのプロジェクトをデバッグすることができます。

     

2.  手順に従って、**既存コード ファイル ウィザードからのプロジェクトの作成へようこそ**します。 言語、プロジェクト名では、ドライバー ソース ファイルの場所を指定することを確認し、します。
3.  新しく作成されたプロジェクトを開きます。
4.  **プロセスには、デバッグ/アタッチ**メニューの [ *WudfHost.exe*で、**選択可能なプロセス**一覧に表示される、 **のプロセスにアタッチ**] ダイアログ ボックス。 1 つ以上のインスタンスがある場合、 *WudfHost.exe*処理で、ドライバーの DLL が読み込まれている 1 つを選択します。
5.  前の手順を完了すると、ソース コードにブレークポイントを設定して、ドライバーをデバッグできます。

## <a name="span-idtipsfordebuggingwpddriverinitializationcodespanspan-idtipsfordebuggingwpddriverinitializationcodespanspan-idtipsfordebuggingwpddriverinitializationcodespantips-for-debugging-wpd-driver-initialization-code"></a><span id="Tips_for_Debugging_WPD_Driver_Initialization_Code"></span><span id="tips_for_debugging_wpd_driver_initialization_code"></span><span id="TIPS_FOR_DEBUGGING_WPD_DRIVER_INITIALIZATION_CODE"></span>WPD ドライバーの初期化コードをデバッグするためのヒント


たとえば、コードの WPD ドライバーの場合、初期化がコード**WpdBaseDriver::Initialize** WDK に同梱されている 2 つの WPD サンプル ドライバー、この初期化コードをデバッグするには、ドライバーがインストールされているときに実行します。使用する必要があります、 *WDFVerifier* Windows Driver Kit に含まれているツールです。 このツールは、ホスト プロセスの起動時に、または、ドライバーの読み込み時に自動的に起動されるように、ユーザー モード デバッガーを使用できます。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


****
[WpdBasicHardwareDriverSample](the-wpdbasichardwaredriver-sample.md)

[WPD ドライバーのサンプル](the-wpd-driver-samples.md)

 

 





