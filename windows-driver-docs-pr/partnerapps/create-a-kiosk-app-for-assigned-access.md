---
title: キオスク アプリの割り当てのアクセスのベスト プラクティス
description: キオスク アプリの割り当てのアクセスのベスト プラクティス
ms.assetid: 2405B5BB-2214-4B40-B3A1-C47073390B21
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 448d0031bad39aca6e6ae5e2d95bc15ee24d4502
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537412"
---
# <a name="kiosk-apps-for-assigned-access-best-practices"></a>割り当てられたアクセスのキオスク アプリ:ベスト プラクティス


Windows 10 では、1 つのユニバーサル Windows アプリだけと対話するのにことができますキオスク デバイスを作成するのに割り当てられたアクセスを使用できます。 このトピックでは、キオスク アプリ、およびベスト プラクティスを実装する方法を説明します。

割り当てられたアクセスが提供する 2 つの異なるエクスペリエンスがあります。

1. シングル アプリ キオスク エクスペリエンス
    1. アカウントには、1 つのアプリを割り当てます。 ユーザーがログインするときは、のみ、このアプリとその他に何もへのアクセス、システム上、なります。 この期間中、キオスク アプリがロック画面上で実行されている、キオスク デバイスはロックされています。 このエクスペリエンスはパブリックに公開されたキオスク コンピューターのよく使用されます。 参照してください[を設定するには、Windows 10 Pro、Enterprise、または教育のキオスク](https://docs.microsoft.com/windows/configuration/set-up-a-kiosk-for-windows-10-for-desktop-editions)詳細についてはします。

2. マルチ アプリ キオスク エクスペリエンスの (Windows 10 バージョン 1709 以降で使用可能)
    1. アカウントには、1 つまたは複数のアプリを割り当てることができます。 ユーザーのログオン、選択したアプリのみへのアクセスを制限付きのシェル エクスペリエンスで、デバイスが開始されます。 参照してください[複数のアプリを実行している Windows 10 キオスクを作成する](https://docs.microsoft.com/windows/configuration/lock-down-windows-10-to-specific-apps)詳細についてはします。

> [!NOTE]
> この記事では、シングル アプリ キオスク エクスペリエンスのみについて説明します。 マルチ アプリ エクスペリエンスでは、選択されているアプリは、通常のデスクトップ コンテキストで実行され、特別な処理または変更は必要ありません。

## <a name="terms"></a>用語


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>用語</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><span id="assigned_access"></span><span id="ASSIGNED_ACCESS"></span>割り当てられたアクセス</p></td>
<td><p>により、システム管理者は、デバイスのユーザーに公開されているアプリケーションのエントリ ポイントを制限することで、ユーザーのエクスペリエンスを管理する機能です。 たとえば、キオスクのように、PC が機能するために 1 つのアプリを使用する、会社の顧客を制限できます。 だれかが指定されたアカウントでサインインするたびに、&#39;ll のみがその 1 つのアプリを使用できるようにします。 これらが勝利した&#39;アプリを切り替えるか、タッチ ジェスチャ、マウス、キーボード、またはハードウェア ボタンを使用してアプリケーションを終了することはできません。 これらもが勝利した&#39;t は、すべてのアプリ通知を参照してください。</p></td>
</tr>
<tr class="even">
<td><p><span id="lock_screen_app__or_lock_app_"></span><span id="LOCK_SCREEN_APP__OR_LOCK_APP_"></span>ロック画面アプリ (またはロック アプリ)</p></td>
<td><p>アプリケーション ロックの新しい機能拡張フレームワークの利用または動的の壁紙を設定することの利点は、いずれかのことです。</p></td>
</tr>
<tr class="odd">
<td><p><span id="above_lock_screen_app__or_above_lock_app_"></span><span id="ABOVE_LOCK_SCREEN_APP__OR_ABOVE_LOCK_APP_"></span>ロック画面のアプリ上 (またはロック アプリ上)</p></td>
<td><p>(たとえば、デスクトップがロックされている) 場合、ロック画面のアプリの実行中にロック画面を起動するアプリケーション。</p></td>
</tr>
<tr class="even">
<td><p><span id="under_lock_app"></span><span id="UNDER_LOCK_APP"></span>ロック アプリ</p></td>
<td><p>ロックされていない Windows コンテキストでは通常、実行されるアプリケーション。</p></td>
</tr>
<tr class="odd">
<td><p><span id="LockApplicationHost"></span><span id="lockapplicationhost"></span><span id="LOCKAPPLICATIONHOST"></span><a href="https://go.microsoft.com/fwlink/?LinkId=691219" data-raw-source="[LockApplicationHost](https://go.microsoft.com/fwlink/?LinkId=691219)">LockApplicationHost</a></p></td>
<td><p>要求をロック画面アプリ上のデバイスを許可する WinRT クラスは、ロックの解除し、アプリ、デバイスがロックを解除する開始時に通知が登録を許可します。</p></td>
</tr>
<tr class="even">
<td><p><span id="View_or_Application_View"></span><span id="view_or_application_view"></span><span id="VIEW_OR_APPLICATION_VIEW"></span>表示またはアプリケーションの表示</p></td>
<td><p>各ビューは、アプリに別のウィンドウです。 アプリは、main を表示、および複数の作成ができ、要求時にセカンダリを表示します。 参照してください<a href="https://go.microsoft.com/fwlink/?LinkId=691220" data-raw-source="[ApplicationView]( https://go.microsoft.com/fwlink/?LinkId=691220)">ApplicationView</a>詳細についてはします。</p></td>
</tr>
</tbody>
</table>



## <a name="the-windowsabovelockscreen-extension"></a>Windows.aboveLockScreen 拡張機能

Windows 10 で割り当てられたアクセスは、ロックのフレームワークを活用します。 割り当てられたアクセスのユーザーがログイン時にバック グラウンド タスクは、デスクトップをロックし、ロックの上、キオスク アプリを起動します。 Windows.aboveLockScreen 拡張機能を使用しているかどうかに応じて、アプリの動作が異なる場合があります。

使用して**windows.aboveLockScreen**キオスク アプリにアクセスできるように、 [LockApplicationHost](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.LockScreen.LockApplicationHost)アプリが実行されているロック上 (およびそのキオスクとして実行されている場合を把握できるようにするランタイム クラスエクスペリエンス)。 インスタンスを返すことができない場合は、通常のデスクトップのコンテキストで、アプリが実行されています。 

ロック framework ロックの上、キオスク アプリを起動して、アプリには、 **windows.aboveLockScreen**拡張機能では、ロックのフレームワークは自動的にロックの上の新しいセカンダリ ビューを作成します。 メイン ビューは、ロックの下にあります。 このセカンダリ ビューは、アプリのコンテンツが含まれてし、ユーザーに対して表示します。 この追加のビューは、キオスク、エクスペリエンスを調整する、拡張機能を使用できます。 たとえば、次のようなことができます。

* [キオスク エクスペリエンスをセキュリティで保護された](#secureinfo)キオスクだけのコンテンツを表示する個別のページを作成します。

* 呼び出す、 **LockApplicationHost.RequestUnlock()** メソッドへのアプリから[割り当てのアクセス モードを終了](#addaway)ログイン画面に戻ります。   

* [イベント ハンドラーを追加](#eventhandler)に、**LockApplicationHost.Unlocking*ユーザーが、キオスクのエクスペリエンスを終了するには Ctrl + Alt + Del キーを押したときに発生するイベントです。 ハンドラーが終了する前にデータを保存することも可能性があります。



アプリがない場合、 **windows.aboveLockScreen**拡張機能では、セカンダリのビューは作成されませんし、アプリは、通常どおり実行されている場合が起動します。 さらに、アプリには、LockApplicationHost のインスタンスへのアクセス権がないため、またはキオスク エクスペリエンスの正規表現のコンテキストで実行されている場合を判断することができません。 サポートするためにできるなどの利点があります、拡張子を含まない[複数のモニター](#multiplemonitors)


かどうか、アプリは、拡張機能を使用して、関係なく、そのデータをセキュリティで保護することを確認します。 参照してください、[アプリに割り当てられたアクセスするためのガイドライン](https://docs.microsoft.com/windows/configuration/guidelines-for-assigned-access-app#secure-your-information)詳細についてはします。

> [!NOTE]
> 以降では、Windows 10 version 1607 ではありません、ユニバーサル Windows プラットフォーム (UWP) 拡張機能の制限にほとんどのアプリを表示できるように**設定**アクセス権を割り当てるときにユーザーを構成します。

## <a name="best-practices"></a>ベスト プラクティス


> [!NOTE]
> このセクションを使用するキオスク アプリケーションに適用されます、 **windows.aboveLockScreen**拡張機能。



### お客様の情報をセキュリティで保護します。 <a name="secureinfo"></a>

キオスク アプリが実行するものである場合両方上のロックでアクセス権が割り当てとも、ロックされていない Windows コンテキストで、ロックの上に表示するために別のページと、ロックの状況で他のページを作成します。 これは、オプションを選択するキオスク モードは、通常、匿名アクセスを意味するため、キオスク モードの場合は、機密情報を表示しないようにすることができます。 次に、2 つの異なるページを使用して、用に 1 つのロックおよびロックの上の 1 つには次の手順に示します。

1.  内のオーバーライドで、 **OnLaunched** App.xaml.cs で関数のインスタンスを取得しようとしています、 [LockApplicationHost](https://go.microsoft.com/fwlink/?LinkId=691219) rootFrame ナビゲーションの前にクラス。
2.  呼び出しが失敗した場合、キオスク アプリは正常に起動、ロックの下。
3.  呼び出しが成功すると、割り当てられたアクセス モードで実行されているロック上キオスク アプリを起動する必要があります。 このバージョンの機密情報を非表示にする別のメイン ページに、キオスク アプリのことができます。

次の例では、これを行う方法を示します。 AssignedAccessPage.xaml は事前に定義し、アプリは、ロック モードの上で実行されていることが検出される AssignedAccessPage.xaml に移動します。 その結果、通常のページをでのみ表示は、ロックの状況下。

このメソッドを使用して、アプリのライフ サイクルでいつでも、ロック画面アプリが実行されているかどうかを決定し、それに対応することができます。
```cpp
using Windows.ApplicationModel.LockScreen;

// inside the override OnLaunched function in App.xaml.cs

if (rootFrame.Content == null)
{
    LockApplicationHost host = LockApplicationHost.GetForCurrentView();
    if (host == null)
    {
        // if call to LockApplicationHost is null, this app is running under lock
        // render MainPage normally
        rootFrame.Navigate(typeof(MainPage), e.Arguments);
    }
    else
    {
        // If LockApplicationHost was successfully obtained
        // this app is running as a lock screen app, or above lock screen app
        // render a different page for assigned access use
        // to avoid showing regular main page to keep secure information safe
        rootFrame.Navigate(typeof(AssignedAccessPage), e.Arguments);
    }
}
```

### 複数のビュー、windows、およびスレッド <a name="multiplemonitors"></a>

Windows 10、バージョン 1803、以降[複数ビュー](https://docs.microsoft.com/windows/uwp/design/layout/show-multiple-views)がないアプリのキオスク エクスペリエンスではサポートされている、 **windows.aboveLockScreen**拡張機能。 複数のビューを使用するには、キオスク デバイスを確認します。**マルチ ディスプレイ**にオプションが設定されている**これらの表示を拡張**します。

ときに複数のビューを使用するアプリ (されず**windows.aboveLockScreen**) が起動される、キオスク エクスペリエンス中に、アプリのメイン ビューを 1 日のモニターに表示されます。 新しいビューがアプリを使用して作成された場合[CreateNewView()](https://docs.microsoft.com/uwp/api/windows.applicationmodel.core.coreapplication)、これは、2 つ目のモニターにレンダリングされます。 アプリでは、別のビューを作成する場合は、3 つ目のモニターに移動し、具合にします。

> [!IMPORTANT]
> キオスク デバイスは、モニターごとに 1 つのビューのみを表示できます。 たとえば、キオスク デバイスに 1 つのモニターがある場合は、キオスク アプリのメイン ビュー常に表示されます。 アプリが作成した新しいビューには表示されません。

キオスク アプリがある場合、 **windows.aboveLockScreen**拡張機能が実行されていると、ロックの上、初期化が異なります。 セカンダリ上にビューを使用して、ロックの状況では、そのメイン ビューにあります。 このセカンダリ ビューは、ユーザーが表示されるものになります。 明示的にすべての新しいビューを作成しない場合でも必要があることも 2 つのビューで、アプリのインスタンスに注意してください。  

![ロック モードでアプリを実行するときにビューの z オーダー](images/assignedaccesssamplelayout.png)

(割り当てられたアクセス モード) では、アプリのメイン ウィンドウで、次のコードを実行すると、ビューの数と、現在の画面のメイン ビューがかどうかを参照してください。

```cpp
using Windows.ApplicationModel.Core;

CoreApplication.GetCurrentView().IsMain //false
CoreApplication.Views.Count //2
```

### <a name="dispatcher"></a>ディスパッチャー

各ビューまたはウィンドウは、独自のディスパッチャーを持っています。 メイン ビューがユーザーに表示されていないために、使用**GetCurrentView()** MainView() ではなく、ロックの上で実行されているアプリのセカンダリのビューにアクセスします。 

```cpp
using Windows.ApplicationModel.Core;

private async void Button_Click(object sender, RoutedEventArgs e)
{
    button.IsEnabled = false;

    // start a background task and update UI periodically (every 1 second)
    // using MainView dispatcher in below code will end up with app crash
    // in assigned access mode, use GetCurrentView().Dispatcher instead
    await CoreApplication.GetCurrentView().Dispatcher.RunAsync(
        CoreDispatcherPriority.Normal,
        async () =>
        {
            for (int i = 0; i < 60; ++i)
            {
                // do some background work, here we use Task.Delay to sleep
                await Task.Delay(1000);
                // update UI
                textBlock1.Text = "   " + i.ToString();
            }
            button.IsEnabled = true;
        });
}
```

アプリは、windows.aboveLockScreen を備え、キオスク エクスペリエンスとして実行され、ときに新しいビューを作成すると、アプリ内で例外が発生します。

```cpp
Windows.ApplicationModel.Core.CoreApplication.CreateNewView(); //causes exception
```

このため、複数のビューがあるまたは複数のモニター上で実行できません。 を、アプリがいずれもサポートする必要がある場合は、アプリから windows.aboveLockScreen 拡張機能を削除する必要があります。


### 割り当てられたアクセス外の手段を追加します。 <a name="addaway"></a>

場合によっては、[電源] ボタン、エスケープ ボタン、またはその他のボタンを使用してアプリケーションを停止できない可能性があります有効または、キーボードでご確認いただけます。 このような状況では、割り当てられたアクセス、ソフトウェア キーのインスタンスを停止する方法を提供します。 次のイベント ハンドラーは、ボタンに応答することによって割り当てられたアクセス モードを停止する方法を示しています。 ソフトウェア キーによって発生する可能性がイベントをクリックします。

```cpp
LockApplicationHost^ lockHost = LockApplicationHost::GetForCurrentView();
    if (lockHost != nullptr)
    {
        lockHost->RequestUnlock();
    }
```

### ライフ サイクル管理 <a name="eventhandler"></a>

キオスク アプリのライフ サイクルは、割り当てられたアクセス フレームワークによって処理されます。 アプリが予期せず終了した場合、フレームワークは再起動しようとします。 ただし、ユーザーは、ログイン画面を表示するには Ctrl + Alt + Del を押すと、ロックを解除するイベントがトリガーされます。 割り当てられたアクセス フレームワークは、イベントをリッスンし、アプリを終了ましょう。

キオスク アプリはこのイベントのハンドラーを登録し、終了する前にアクションを実行できます。 この例は、データを保存します。 ハンドラーの登録の例を次のコードを参照してください。

```cpp
using Windows.ApplicationModel.LockScreen;

public AssignedAccessPage()
{
    this.InitializeComponent();

    LockApplicationHost lockHost = LockApplicationHost.GetForCurrentView();
    if (lockHost != null)
    {
        lockHost.Unlocking += LockHost_Unlocking;
}
}

private void LockHost_Unlocking(LockApplicationHost sender, LockScreenUnlockingEventArgs args)
{
    // save any unsaved work and gracefully exit the app
    App.Current.Exit();
}
```

Ctrl + Alt + Del キーを押すし、ログイン画面が表示されます、次の 2 つが発生する可能性があります。

1.  ユーザーが、割り当てられたアクセス アカウントのパスワードを知っていて、デスクトップのロックを解除します。 割り当てられたアクセス フレームワークと起動、デスクトップ、およびキオスク アプリを起動、ロック画面アプリが起動をロックします。
2.  ユーザーがパスワードを知らないか、その後の操作を受け取りません。 ログイン画面のタイムアウトとデスクトップ relocks;ロック画面アプリが起動の結果には、キオスク アプリを起動します。

### <a name="span-iddontcreatenewwindowsorviewsinassignedaccessmodespanspan-iddontcreatenewwindowsorviewsinassignedaccessmodespanspan-iddontcreatenewwindowsorviewsinassignedaccessmodespandont-create-new-windows-or-views-in-assigned-access-mode"></a><span id="Don_t_create_new_windows_or_views_in_assigned_access_mode"></span><span id="don_t_create_new_windows_or_views_in_assigned_access_mode"></span><span id="DON_T_CREATE_NEW_WINDOWS_OR_VIEWS_IN_ASSIGNED_ACCESS_MODE"></span>割り当てられたアクセス モードで新しいウィンドウまたはビューを作成しないでください。

次の関数呼び出しは割り当てられたアクセス モードでメソッドが呼び出された場合に、ランタイム例外終了します。 ロックの状況で使用する場合は、同じアプリでは、関数を呼び出し場合、ランタイム例外は発生しません。 使用することをお勧め[LockApplicationHost](https://go.microsoft.com/fwlink/?LinkId=691219)アプリの割り当てられたアクセスのモードを決定し、新しいビューを作成しない場合は、アプリが割り当てられたアクセス モードなど、アプリをそれに応じてコードします。

```cpp
Windows.ApplicationModel.Core.CoreApplication.CreateNewView(); //causes exception
```

## <a name="span-idappendix1uwpextensionspanspan-idappendix1uwpextensionspanspan-idappendix1uwpextensionspanappendix-1-uwp-extension"></a><span id="Appendix_1__UWP_extension"></span><span id="appendix_1__uwp_extension"></span><span id="APPENDIX_1__UWP_EXTENSION"></span>付録 1:UWP 拡張機能


次のサンプル アプリケーションで使用するマニフェスト、 **windows.aboveLockScreen**UWP 拡張機能。 

> [!NOTE]
> 以降では、Windows 10 version 1607 ではありません、ユニバーサル Windows プラットフォーム (UWP) 拡張機能の制限にほとんどのアプリを表示できるように**設定**アクセス権を割り当てるときにユーザーを構成します。


```cpp
<Package xmlns="http://schemas.microsoft.com/appx/manifest/foundation/windows10" xmlns:mp="http://schemas.microsoft.com/appx/2014/phone/manifest" xmlns:uap="http://schemas.microsoft.com/appx/manifest/uap/windows10" IgnorableNamespaces="uap mp">
  <Identity Name="bd4df68b-dc18-4748-a14e-bc21dac13736" Publisher="Contoso" Version="1.0.0.0" />
  <mp:PhoneIdentity PhoneProductId="bd4df68b-dc18-4748-a14e-bc21dac13736" PhonePublisherId="00000000-0000-0000-0000-000000000000" />
  <Properties>
    <DisplayName>AboveLock</DisplayName>
    <PublisherDisplayName>Contoso</PublisherDisplayName>
    <Logo>Assets\StoreLogo.png</Logo>
  </Properties>
  <Dependencies>
    <TargetDeviceFamily Name="Windows.Universal" MinVersion="10.0.0.0" MaxVersionTested="10.0.0.0" />
  </Dependencies>
  <Resources>
    <Resource Language="x-generate" />
  </Resources>
  <Applications>
    <Application Id="App" Executable="$targetnametoken$.exe" EntryPoint="AboveLock.App">
      <uap:VisualElements DisplayName="AboveLock" Square150x150Logo="Assets\Square150x150Logo.png" Square44x44Logo="Assets\Square44x44Logo.png" Description="AboveLock" BackgroundColor="transparent">
        <uap:DefaultTile Wide310x150Logo="Assets\Wide310x150Logo.png">
        </uap:DefaultTile>
        <uap:SplashScreen Image="Assets\SplashScreen.png" />
      </uap:VisualElements>
      <Extensions>
        <uap:Extension Category="windows.lockScreenCall" />
        <uap:Extension Category="windows.aboveLockScreen" />
      </Extensions>
    </Application>
  </Applications>
  <Capabilities>
    <Capability Name="internetClient" />
  </Capabilities>
</Package>
```

## <a name="span-idappendix2troubleshootingspanspan-idappendix2troubleshootingspanspan-idappendix2troubleshootingspanappendix-2-troubleshooting"></a><span id="Appendix_2__troubleshooting"></span><span id="appendix_2__troubleshooting"></span><span id="APPENDIX_2__TROUBLESHOOTING"></span>付録 2: のトラブルシューティング


通常、キオスク アプリは、ロック画面のアプリ上のアクティブ化に失敗した場合、[ロックダウン] 画面で、アクティブ化エラー コードが表示されます。 エラー コードを使用して Windows を参照して、問題を見つけた[システム エラー コード](https://msdn.microsoft.com/library/windows/desktop/ms681381)します。 さらにイベント ビューアーには、ライセンス認証エラーの詳細が含まれています。 そのためには、次の操作を実行します。

1.  **イベント ビューアー**を開きます。 アクティブ化エラーを検出する可能性が高い 2 つの場所があります。
2.  **イベント ビューアー (ローカル)** ウィンドウで、展開**Windows ログ**、 をクリックし、**アプリケーション**します。
3.  また、**イベント ビューアー (ローカル)**、展開**Applications and Services Logs**、展開**Windows**、展開**アプリ**順にクリックします**Microsoft Windows-TWinUI/運用**します。

割り当てられたアクセス権を持つキオスク アプリが全画面表示モードで実行しないでくださいため**ApplicationView.GetForCurrentView() します。IsFullScreenMode**は false を返します。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[割り当てられたアクセス](https://msdn.microsoft.com/library/windows/hardware/mt620040)

[アプリの複数のビューを表示します。]( https://go.microsoft.com/fwlink/?LinkId=708251)





