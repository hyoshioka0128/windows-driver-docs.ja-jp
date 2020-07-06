---
Description: サンプル ドライバーのテストとデバッグ
title: サンプル ドライバーのテストとデバッグ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 54429252d457fa8fe3d9695302c04161a0274bef
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85967861"
---
# <a name="testing-and-debugging-the-sample-driver"></a>サンプル ドライバーのテストとデバッグ


WDK には、WPD ドライバーのテストとデバッグに使用できる3つのツールが含まれています。 これらのツールについては、次の表で説明します。

**ツール**: 説明

***WpdInfo.exe***: このツールでは、デバイスの開閉、デバイス上でのオブジェクトの作成または削除、サポートされているコマンドの表示、イベントの表示、イベントの表示、読み取り可能なプロパティ値の取得、および書き込み可能なプロパティ値の設定を行うことができます。

***WpdDeviceInspector.exe***: デバイスの機能とコンテンツを記述する HTML レポートを生成します。

***WpdMon.exe***: wpd ドライバーとオペレーティングシステムまたは wpd アプリケーションの間で渡されるメッセージとコマンドをトレースします。


 

これらのツールとその使用方法の詳細については、WDK ドキュメントの「 [WPD ドライバー開発ツール](familiarizing-yourself-with-the-sample-driver.md)」を参照してください。

## <a name="span-idtracking_the_sensor_reading_event_by_using_wpdinfoexespanspan-idtracking_the_sensor_reading_event_by_using_wpdinfoexespantracking-the-sensor-reading-event-by-using-wpdinfoexe"></a><span id="tracking_the_sensor_reading_event_by_using_wpdinfo.exe"></span><span id="TRACKING_THE_SENSOR_READING_EVENT_BY_USING_WPDINFO.EXE"></span>WpdInfo.exe を使用したセンサーの読み取りイベントの追跡


*WpdInfo.exe*を開始する前に、センサーの \_ 読み取りとセンサー更新間隔プロパティの propertykeys を \_ 対応する \_ フレンドリ文字列にマップするエントリを使用して、wpdinfo. プロパティファイルを更新します。

```ManagedCPlusPlus
{a7ef4367-6550-4055-b66f-be6fdacf4e9f}.2, SENSOR_READING, VT_UI8
{a7ef4367-6550-4055-b66f-be6fdacf4e9f}.3, SENSOR_UPDATE_INTERVAL, VT_UI4
```

WpdInfo. Properties ファイルは、 *WpdInfo.exe*と同じフォルダーにあります。 このファイルが存在しない場合は、 *WpdInfo.exe*一度実行して生成します。

*WpdInfo.exe*を開始すると、インストールされている WPD デバイスの一覧からポータブルデバイスを選択するように求められます。 センサーデバイスを選択すると、そのウィンドウの下のウィンドウにイベントが記録されます。

![wpd 情報ツール](images/wpdinfo_temphumidity_object.png)

前の例でセンサーの読み取りイベントが発生すると、次の情報が true になりました。

-   センサー読み取りプロパティ (センサー \_ 読み取り) は2170720417でした。 この値は、センサー識別子 2 (Sensiron 温度と湿度センサーに対応)、カウント1、要素あたり7バイト、華氏72.0 °、および41.7% の相対湿度を示します (温度と湿度センサーに対応します)。
-   間隔のプロパティである [センサーの \_ 更新 \_ 間隔] が2000に設定されました。

## <a name="span-idupdating_the_interval_property_by_using_wpdinfoexespanspan-idupdating_the_interval_property_by_using_wpdinfoexespanupdating-the-interval-property-by-using-wpdinfoexe"></a><span id="updating_the_interval_property_by_using_wpdinfo.exe"></span><span id="UPDATING_THE_INTERVAL_PROPERTY_BY_USING_WPDINFO.EXE"></span>WpdInfo.exe を使用した Interval プロパティの更新


視差 BS2 センサーデバイスを選択した後、このツールを使用して、間隔プロパティの [センサー \_ \_ の更新間隔] を既定値の2000ミリ秒から別の値 (2 ~ 60 秒) に変更できます。

1.  最初の手順では、列挙ペインから TempHumidity 機能オブジェクトを選択して、そのオブジェクトのすべてのプロパティ値を表示する必要があります。 このオブジェクトは、一番左のウィンドウで、デバイスオブジェクトの直接の子として検索できます。
2.  次に、[**センサー \_ 更新 \_ 間隔**] をクリックします。 [**編集**] ダイアログボックスが開き、新しい値を VT UI4 タイプとして入力でき \_ ます。

![wpd 情報ツール](images/wpdinfo_interval.png)

許容される値の範囲は 02000 ~ 6万です。 [ **OK**] をクリックすると、新しい interval プロパティ値がデバイスに送信されます。 [イベント] ウィンドウを確認すると、イベントパラメーターに [新しい更新間隔] の値が表示されたイベントが表示されます。

## <a name="span-iddebugging_the_driver_with_visual_studio_8spanspan-iddebugging_the_driver_with_visual_studio_8spanspan-iddebugging_the_driver_with_visual_studio_8spandebugging-the-driver-with-visual-studio-8"></a><span id="Debugging_the_Driver_with_Visual_Studio_8"></span><span id="debugging_the_driver_with_visual_studio_8"></span><span id="DEBUGGING_THE_DRIVER_WITH_VISUAL_STUDIO_8"></span>Visual Studio 8 を使用したドライバーのデバッグ


WPD ドライバーは、Windows Driver Framework (WDF) の UMDF プラットフォームに基づいています。 UMDF ドライバーは、カーネルモードドライバーよりも安定性とセキュリティを向上させると共に、同等のパフォーマンスを実現します。 また、UMDF ドライバーでは、Visual Studio 8 などのユーザーモードのデバッガーを使用できます。 ユーザーモードでのドライバーのデバッグは、コンピューター全体ではなく現在のプロセスのみに影響するため、カーネルモードでのデバッグよりも速くなる傾向があります。

ドライバーをインストールした後、Visual Studio 8 でデバッグプロジェクトを作成するには、次の手順を実行します。

1.  管理者特権 ([管理者として実行]) を使用して Visual Studio 8 を開き、[ &lt; 既存のコードパスからファイル] [新しいプロジェクト] の順に移動し &gt; ます。
    **メモ**   LocalService アカウントにはこれらの特権が必要であるため、昇格された特権で Visual Studio 8 を開く必要があります。 WUDFHost プロセスは、LocalService アカウント内で実行されます。 Visual Studio 8 を使用すると、ドライバープロジェクトをデバッグできます。

     

2.  「**既存のコードファイルからのプロジェクトの作成ウィザードの開始**」に記載されている手順に従います。 言語、ドライバーのソースファイルの場所、プロジェクト名などを指定してください。
3.  新しく作成したプロジェクトを開きます。
4.  [**デバッグ/プロセスにアタッチ**] メニューの [**プロセスにアタッチ**] ダイアログボックスに表示される [選択**可能なプロセス**] ボックスの一覧の [ *WudfHost.exe* ] をクリックします。 *WudfHost.exe*プロセスのインスタンスが複数ある場合は、ドライバーの DLL を読み込んだものを選択します。
5.  前の手順を完了したら、ソースコードにブレークポイントを設定し、ドライバーをデバッグできます。

## <a name="span-idtips_for_debugging_wpd_driver_initialization_codespanspan-idtips_for_debugging_wpd_driver_initialization_codespanspan-idtips_for_debugging_wpd_driver_initialization_codespantips-for-debugging-wpd-driver-initialization-code"></a><span id="Tips_for_Debugging_WPD_Driver_Initialization_Code"></span><span id="tips_for_debugging_wpd_driver_initialization_code"></span><span id="TIPS_FOR_DEBUGGING_WPD_DRIVER_INITIALIZATION_CODE"></span>WPD ドライバー初期化コードのデバッグに関するヒント


WPD ドライバーの初期化コード。たとえば、WDK でパッケージ化された2つの WPD サンプルドライバーの**Wpdbasedriver:: Initialize**にあるコードは、ドライバーのインストール時に実行され、この初期化コードをデバッグします。そのためには、Windows driver Kit に含まれている*wdfverifier*ツールを使用する必要があります。 このツールを使用すると、ホストプロセスの起動時、またはドライバーの読み込み時に、ユーザーモードのデバッガーを自動的に起動できます。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


****
[Wpdbasicハードウェアのサンプル](the-wpdbasichardwaredriver-sample.md)

[WPD ドライバーのサンプル](the-wpd-driver-samples.md)

 

 





