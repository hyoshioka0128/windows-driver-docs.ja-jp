---
title: 割り当てられたアクセスのベストプラクティス用キオスクアプリ
description: 割り当てられたアクセスのベストプラクティス用キオスクアプリ
ms.assetid: 2405B5BB-2214-4B40-B3A1-C47073390B21
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3799a1a850bc4c77163cd6b4f15750f8bb66c0e8
ms.sourcegitcommit: 6bd546fea677833fc20cd802256d030633ac562e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/11/2020
ms.locfileid: "84717451"
---
# <a name="kiosk-apps-for-assigned-access-best-practices"></a>割り当てられたアクセス用のキオスクアプリ: ベストプラクティス


Windows 10 では、割り当てられたアクセスを使用してキオスクデバイスを作成することができます。これにより、ユーザーは単一のユニバーサル Windows アプリと対話できるようになります。 このトピックでは、キオスクアプリを実装する方法とベストプラクティスについて説明します。

割り当てられたアクセスでは、次の2つの異なるエクスペリエンスが提供されます。

1. シングルアプリキオスクエクスペリエンス
    1. 1つのアプリをアカウントに割り当てます。 ユーザーがログインすると、このアプリにのみアクセスでき、システム上では何もアクセスできなくなります。 この間、キオスクデバイスはロック画面上で実行されているキオスクアプリでロックされます。 このエクスペリエンスは、一般に公開されているキオスクコンピューターでよく使用されます。 詳細については、「 [Windows 10 Pro、Enterprise、または教育でのキオスクのセットアップ](https://docs.microsoft.com/windows/configuration/set-up-a-kiosk-for-windows-10-for-desktop-editions)」を参照してください。

2. マルチアプリキオスクエクスペリエンス (Windows 10 バージョン1709以降で使用可能)
    1. 1つまたは複数のアプリをアカウントに割り当てることができます。 ユーザーがログインすると、デバイスは、選択したアプリにのみアクセスできる制限付きシェルエクスペリエンスで開始されます。 詳細については[、「複数のアプリを実行する Windows 10 キオスクを作成](https://docs.microsoft.com/windows/configuration/lock-down-windows-10-to-specific-apps)する」を参照してください。

> [!NOTE]
> この記事では、シングルアプリキオスクエクスペリエンスのみについて説明します。 マルチアプリエクスペリエンスでは、選択したアプリは通常のデスクトップコンテキストで実行され、特別な処理や変更は必要ありません。

## <a name="terms"></a>用語


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>期間</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><span id="assigned_access"></span><span id="ASSIGNED_ACCESS"></span>割り当てられたアクセス</p></td>
<td><p>デバイスのユーザーに公開されているアプリケーションのエントリポイントを制限することで、システム管理者がユーザーのエクスペリエンスを管理できるようにする機能。 たとえば、会社の顧客を1つのアプリを使用するように制限して、PC がキオスクのように動作するようにすることができます。 指定されたアカウントでサインインするたびに、その1つのアプリのみを使用できます。 タッチジェスチャ、マウス、キーボード、またはハードウェアボタンを使用してアプリを切り替えたり、アプリを閉じたりすることはできません。 また、アプリの通知も表示されません。</p></td>
</tr>
<tr class="even">
<td><p><span id="lock_screen_app__or_lock_app_"></span><span id="LOCK_SCREEN_APP__OR_LOCK_APP_"></span>ロック画面アプリ (またはロックアプリ)</p></td>
<td><p>動的な壁紙を設定したり、新しいロック拡張フレームワークを利用したりする機能を利用できるアプリケーション。</p></td>
</tr>
<tr class="odd">
<td><p><span id="above_lock_screen_app__or_above_lock_app_"></span><span id="ABOVE_LOCK_SCREEN_APP__OR_ABOVE_LOCK_APP_"></span>ロック画面アプリ (またはその上のロックアプリ)</p></td>
<td><p>ロック画面アプリの実行中にロック画面の上に起動するアプリケーション (デスクトップがロックされている場合など)。</p></td>
</tr>
<tr class="even">
<td><p><span id="under_lock_app"></span><span id="UNDER_LOCK_APP"></span>[アプリのロック]</p></td>
<td><p>ロックされていない Windows コンテキストで、正常に実行されるアプリケーション。</p></td>
</tr>
<tr class="odd">
<td><p><span id="LockApplicationHost"></span><span id="lockapplicationhost"></span><span id="LOCKAPPLICATIONHOST"></span><a href="https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.LockScreen.LockApplicationHost" data-raw-source="[LockApplicationHost](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.LockScreen.LockApplicationHost)">LockApplicationHost</a></p></td>
<td><p>上のロック画面アプリがデバイスのロックを解除することを許可し、デバイスのロック解除が開始されたときにアプリが通知を受け取ることができるようにする WinRT クラス。</p></td>
</tr>
<tr class="even">
<td><p><span id="View_or_Application_View"></span><span id="view_or_application_view"></span><span id="VIEW_OR_APPLICATION_VIEW"></span>ビューまたはアプリケーションビュー</p></td>
<td><p>各ビューは、アプリの別のウィンドウです。 アプリはメインビューを持つことができ、必要に応じて複数のセカンダリビューを作成できます。 詳細については、「 <a href="https://docs.microsoft.com/uwp/api/Windows.UI.ViewManagement.ApplicationView" data-raw-source="[ApplicationView]( https://docs.microsoft.com/uwp/api/Windows.UI.ViewManagement.ApplicationView)">Applicationview</a> 」を参照してください。</p></td>
</tr>
</tbody>
</table>



## <a name="the-windowsabovelockscreen-extension"></a>AboveLockScreen 拡張機能

Windows 10 で割り当てられたアクセスは、ロックフレームワークを活用します。 割り当てられたアクセスユーザーがログインすると、バックグラウンドタスクによってデスクトップがロックされ、ロックの上にキオスクアプリが起動されます。 AboveLockScreen 拡張機能を使用するかどうかによって、アプリの動作が異なる場合があります。

**AboveLockScreen**を使用すると、キオスクアプリで[lockapplicationhost](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.LockScreen.LockApplicationHost) runtime クラスにアクセスできるようになります。これにより、アプリがロックの上で実行されている (したがって、キオスク環境として実行されている) ことを確認できます。 インスタンスを返すことができない場合、アプリは通常のデスクトップコンテキストで実行されています。 

ロックフレームワークがロックの上にキオスクアプリを起動し、アプリに**aboveLockScreen**拡張子がある場合、ロックフレームワークによって、ロックの上に新しいセカンダリビューが自動的に作成されます。 メインビューはロックの下にあります。 このセカンダリビューには、アプリのコンテンツが含まれ、ユーザーに表示されます。 この追加のビューを拡張機能と共に使用して、キオスクエクスペリエンスを調整できます。 たとえば、次のように操作できます。

* キオスク専用のコンテンツを表示する別のページを作成して[、キオスクエクスペリエンスを保護](#secureinfo)します。

* アプリから**Lockapplicationhost. RequestUnlock ()** メソッドを呼び出して、[割り当てられたアクセスモードを終了](#addaway)し、ログイン画面に戻ります。   

* ユーザーが Ctrl + Alt + Del キーを押してキオスクエクスペリエンスを終了したときに発生する、**Lockapplicationhost. アンロック*イベントに[イベントハンドラーを追加](#eventhandler)します。 ハンドラーは、終了する前にデータを保存するために使用することもできます。



アプリに**aboveLockScreen**拡張子がない場合、セカンダリビューは作成されず、アプリは正常に実行されているかのように起動します。 また、アプリは LockApplicationHost のインスタンスにアクセスできないため、通常のコンテキストで実行されているか、キオスクエクスペリエンスで実行されているかを判断できません。 拡張機能を含まない場合は、[複数のモニター](#multiplemonitors)をサポートできるなどの利点があります。


アプリが拡張機能を使用しているかどうかにかかわらず、データをセキュリティで保護する必要があります。 詳細については、「[割り当てられたアクセスアプリのガイドライン](https://docs.microsoft.com/windows/configuration/guidelines-for-assigned-access-app#secure-your-information)」を参照してください。

> [!NOTE]
> Windows 10 バージョン1607以降では、ユニバーサル Windows プラットフォーム (UWP) 拡張機能に制限がなくなりました。そのため、ユーザーが割り当てられたアクセスを構成すると、ほとんどのアプリが**設定**に表示されるようになります。

## <a name="best-practices"></a>ベスト プラクティス


> [!NOTE]
> このセクションは、 **aboveLockScreen**拡張機能を使用するキオスクアプリケーションに適用されます。



### <a name="secure-your-information"></a>情報をセキュリティで保護する<a name="secureinfo"></a>

キオスクアプリが、割り当てられたアクセスで上記のロックと、ロックされていない Windows コンテキストの両方を実行することを意図している場合は、別のページを作成して、ロックの上に別のページを表示することもできます。 これにより、キオスクモードでは通常匿名アクセスが使用されるため、キオスクモードでは機密情報を表示しないようにすることができます。 2つの異なるページを使用する手順を次に示します。1つはロックの下、もう1つはロックの上にあります。

1.  App.xaml.cs の**Onlaunched**関数のオーバーライド内で、rootframe ナビゲーションの前に[lockapplicationhost](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.LockScreen.LockApplicationHost)クラスのインスタンスを取得してみてください。
2.  呼び出しが失敗した場合、キオスクアプリはロックの下で正常に起動されます。
3.  呼び出しが成功した場合、キオスクアプリは、割り当てられたアクセスモードで実行されているロックの上に起動する必要があります。 このバージョンのキオスクアプリでは、機密情報を非表示にするために別のメインページが必要になる場合があります。

これを行う方法を次の例に示します。 AssignedAccessPage は事前に定義されています。アプリは、上記のロックモードで実行されていることを検出すると、AssignedAccessPage に移動します。 その結果、通常のページは [ロック] シナリオでのみ表示されます。

このメソッドを使用して、アプリがアプリのライフサイクルの任意の時点でロック画面上で実行されているかどうかを確認し、それに応じて対応することができます。
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

### <a name="multiple-views-windows-and-threads"></a>複数のビュー、ウィンドウ、スレッド<a name="multiplemonitors"></a>

Windows 10 バージョン1803以降では、 **aboveLockScreen**拡張子のないアプリでは、[複数のビュー](https://docs.microsoft.com/windows/uwp/design/layout/show-multiple-views)がキオスク環境でサポートされています。 複数のビューを使用するには、[キオスクデバイスの**複数ディスプレイ**] オプションが、**これらの表示を拡張**するように設定されていることを確認します。

キオスクエクスペリエンス中に複数のビュー ( **aboveLockScreen**なし) のアプリが起動されると、アプリのメインビューが1つ目のモニターに表示されます。 [CreateNewView ()](https://docs.microsoft.com/uwp/api/windows.applicationmodel.core.coreapplication)を使用してアプリで新しいビューを作成すると、2番目のモニターに表示されます。 アプリが別のビューを作成すると、3番目のモニターに移ります。

> [!IMPORTANT]
> キオスクデバイスは、モニターごとに1つのビューのみを表示できます。 たとえば、キオスクデバイスにモニターが1つしかない場合、キオスクアプリのメインビューが常に表示されます。 アプリによって作成された新しいビューは表示されません。

キオスクアプリに**aboveLockScreen**拡張子があり、ロックの上で実行されている場合は、異なる方法で初期化されます。 メインビューはロックの下にあり、その上に2つ目のビューがあります。 このセカンダリビューには、ユーザーに表示されるものが表示されます。 新しいビューを明示的に作成しない場合でも、アプリインスタンスには2つのビューがあります。  

![アプリがロックモードで実行されている場合のビューの z オーダー](images/assignedaccesssamplelayout.png)

アプリのメインウィンドウ ([割り当てられたアクセスモード]) で次のコードを実行すると、ビューカウントと、現在の画面がメインビューであるかどうかを確認できます。

```cpp
using Windows.ApplicationModel.Core;

CoreApplication.GetCurrentView().IsMain //false
CoreApplication.Views.Count //2
```

### <a name="dispatcher"></a>ディスパッチャー

各ビューまたはウィンドウには、独自のディスパッチャーがあります。 メインビューはユーザーに表示されないため、 **GetCurrentView ()** を使用して、mainview () ではなく、ロックの上にあるアプリのセカンダリビューにアクセスします。 

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

アプリに aboveLockScreen があり、キオスク環境として実行されている場合、新しいビューを作成すると、アプリ内で例外が発生します。

```cpp
Windows.ApplicationModel.Core.CoreApplication.CreateNewView(); //causes exception
```

このため、複数のビューを使用したり、複数のモニターで実行したりすることはできません。 アプリでいずれかをサポートする必要がある場合は、アプリから aboveLockScreen 拡張機能を削除する必要があります。


### <a name="add-a-way-out-of-assigned-access"></a>割り当てられたアクセスからの方法の追加<a name="addaway"></a>

場合によっては、アプリケーションを停止するために使用されている電源ボタン、エスケープボタン、またはその他のボタンが、キーボードで有効になっていないか、使用できないことがあります。 このような状況では、ソフトウェアキーなど、割り当てられたアクセスを停止する方法を提供します。 次のイベントハンドラーは、ソフトウェアキーによってトリガーされる可能性があるボタンクリックイベントに応答して、割り当てられたアクセスモードを停止する方法を示しています。

```cpp
LockApplicationHost^ lockHost = LockApplicationHost::GetForCurrentView();
    if (lockHost != nullptr)
    {
        lockHost->RequestUnlock();
    }
```

### <a name="lifecycle-management"></a>ライフサイクル管理<a name="eventhandler"></a>

キオスクアプリのライフサイクルは、割り当てられたアクセスフレームワークによって処理されます。 アプリが予期せず終了した場合、フレームワークはそれを再起動しようとします。 ただし、ユーザーが Ctrl + Alt + Del キーを押してログイン画面を表示すると、ロック解除イベントがトリガーされます。 割り当てられたアクセスフレームワークはイベントをリッスンし、アプリを終了しようとします。

また、キオスクアプリはこのイベントのハンドラーを登録し、終了前にアクションを実行することもできます。 この例として、データを保存することがあります。 ハンドラーを登録する例については、次のコードを参照してください。

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

ユーザーが Ctrl + Alt + Del キーを押した後、ログイン画面が表示されると、次の2つの処理が発生する可能性があります。

1.  ユーザーは、割り当てられたアクセスアカウントのパスワードを認識し、デスクトップのロックを解除します。 割り当てられたアクセスフレームワークが起動し、デスクトップがロックされ、ロック画面アプリが起動されます。これにより、キオスクアプリが起動されます。
2.  ユーザーはパスワードを知らないか、それ以上のアクションを実行していません。 ログイン画面のタイムアウトとデスクトップの再ロック。ロック画面アプリが起動すると、キオスクアプリが起動します。

### <a name="span-iddon_t_create_new_windows_or_views_in_assigned_access_modespanspan-iddon_t_create_new_windows_or_views_in_assigned_access_modespanspan-iddon_t_create_new_windows_or_views_in_assigned_access_modespandont-create-new-windows-or-views-in-assigned-access-mode"></a><span id="Don_t_create_new_windows_or_views_in_assigned_access_mode"></span><span id="don_t_create_new_windows_or_views_in_assigned_access_mode"></span><span id="DON_T_CREATE_NEW_WINDOWS_OR_VIEWS_IN_ASSIGNED_ACCESS_MODE"></span>割り当てられたアクセスモードで新しいウィンドウまたはビューを作成しない

次の関数呼び出しは、割り当てられたアクセスモードで呼び出された場合、ランタイム例外が発生します。 同じアプリが lock で使用されている場合、関数を呼び出すと、ランタイム例外は発生しません。 [Lockapplicationhost](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.LockScreen.LockApplicationHost)を使用してアプリの割り当てられたアクセスモードを決定し、アプリがアクセスモードに割り当てられている場合に新しいビューを作成しないなど、アプリを適宜コーディングすると便利です。

```cpp
Windows.ApplicationModel.Core.CoreApplication.CreateNewView(); //causes exception
```

## <a name="span-idappendix_1__uwp_extensionspanspan-idappendix_1__uwp_extensionspanspan-idappendix_1__uwp_extensionspanappendix-1-uwp-extension"></a><span id="Appendix_1__UWP_extension"></span><span id="appendix_1__uwp_extension"></span><span id="APPENDIX_1__UWP_EXTENSION"></span>付録 1: UWP 拡張機能


次のサンプルアプリケーションマニフェストでは、 **aboveLockScreen**UWP 拡張を使用します。 

> [!NOTE]
> Windows 10 バージョン1607以降では、ユニバーサル Windows プラットフォーム (UWP) 拡張機能に制限がなくなりました。そのため、ユーザーが割り当てられたアクセスを構成すると、ほとんどのアプリが**設定**に表示されるようになります。


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

## <a name="span-idappendix_2__troubleshootingspanspan-idappendix_2__troubleshootingspanspan-idappendix_2__troubleshootingspanappendix-2-troubleshooting"></a><span id="Appendix_2__troubleshooting"></span><span id="appendix_2__troubleshooting"></span><span id="APPENDIX_2__TROUBLESHOOTING"></span>付録 2: トラブルシューティング


通常、キオスクアプリがロック画面アプリ上でアクティブ化に失敗した場合は、ロックダウン画面でアクティブ化エラーコードを見つけることができます。 エラーコードを使用して、Windows[システムエラーコード](https://docs.microsoft.com/windows/desktop/Debug/system-error-codes)を検索して問題を検出します。 さらにイベントビューアーには、ライセンス認証エラーの詳細が含まれています。 次の手順に従います。

1.  **イベント ビューアー**を開きます。 アクティブ化エラーを検出できる場所は2つあります。
2.  [**イベントビューアー (ローカル)** ] ウィンドウで、[ **Windows ログ**] を展開し、[**アプリケーション**] をクリックします。
3.  また、**イベントビューアー (ローカル)** で、[**アプリケーションとサービスログ**]、 **[Windows**]、[**アプリ**] の順に展開し、[ **TWinUI/Operational**] をクリックします。

アクセス権が割り当てられているキオスクアプリは全画面**表示モード (GetForCurrentView) で実行されないことに注意してください。IsFullScreenMode**は false を返します。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[割り当てられたアクセス](https://docs.microsoft.com/windows-hardware/customize/enterprise/assigned-access)

[アプリの複数のビューの表示](https://docs.microsoft.com/windows/uwp/design/layout/show-multiple-views)





