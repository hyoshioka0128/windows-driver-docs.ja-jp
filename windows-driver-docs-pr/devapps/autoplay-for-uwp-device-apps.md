---
title: UWP デバイス アプリの自動再生
description: このトピックでは、デバイス メタデータの作成ウィザードを使用して、自動再生を有効にする方法について説明しています。 アプリで自動再生のアクティブ化を処理する方法についても説明しています。
ms.assetid: A95382E6-DFF4-4F36-9C9B-4B26161160DE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76030386ae552f6e789b69fc3385241a48abfd89
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330747"
---
# <a name="autoplay-for-uwp-device-apps"></a>UWP デバイス アプリの自動再生


デバイスの製造元は、自分のデバイスの自動再生ハンドラーとして UWP デバイス アプリを指定できます。 その他の UWP アプリを自分のデバイス用の自動再生ハンドラーとして機能することもできます。 このトピックでは、デバイス メタデータの作成ウィザードを使用して、自動再生を有効にする方法について説明しています。 アプリで自動再生のアクティブ化を処理する方法についても説明しています。 デバイスのアプリに関する詳細については、次を参照してください。[満たす UWP デバイス アプリ](meet-uwp-device-apps.md)します。

**注**  すべての種類の自動再生デバイス メタデータを使用する必要はありません。 デバイスのメタデータなし自動再生では、ユーザーがデバイスを PC に接続するときに、オプションとして、アプリを提供できます。 ボリューム以外のデバイス、カメラまたはメディア プレーヤーなどが含まれますか、ボリューム デバイスなど、USB サム ドライブ、SD カード、または DVD。 自動再生では、ユーザーは、近接 (タップ) を使用して 2 つのマシン間でファイルを共有する場合、オプションとして、アプリを登録することもできます。 ただし、デバイス メタデータなし、アプリが自動的にインストールことはできません。 デバイスのメタデータが必要でない場合、自動再生の使用に関する詳細については、次を参照してください。[自動再生と自動起動](https://go.microsoft.com/fwlink/p/?LinkID=254861)します。

 

## <a name="span-idautoplayoverviewspanspan-idautoplayoverviewspanspan-idautoplayoverviewspanautoplay-overview"></a><span id="AutoPlay_overview"></span><span id="autoplay_overview"></span><span id="AUTOPLAY_OVERVIEW"></span>自動再生の概要


によって、アプリのバージョンは、次の方法で自動再生を有効にできます。

-   UWP デバイス アプリがデバイスの自動再生のアクティブ化を処理できるだけ\[Windows 8、Windows 8.1 でサポートされている\]します。
-   その他の UWP アプリは、デバイスの自動再生のアクティブ化を処理できる\[Windows 8.1 でのみサポート\]します。
-   UWP デバイス アプリとその他の UWP アプリは、デバイスの自動再生のアクティブ化を処理できる\[Windows 8.1 でのみサポート\]します。

この例は、という名前のアプリの自動再生ダイアログ ボックスを示しています。 **contoso 社のダッシュ ボード**が、の自動再生ハンドラーとして登録する、 **Contoso 歩数計**デバイス。

![デバイスの自動再生ダイアログ ボックスの例](images/autoplayfordeviceapps.png)

アプリをデバイスのメタデータを使用する場合、自動再生には、これらのデバイス タイプがサポートされています。

| デバイス クラス                 | Windows 8 でサポートされている自動再生                                                                    | Windows 8.1 でサポートされている自動再生                                                                    |
|------------------------------|----------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------|
| デジタル カメラ         | ![windows 8 では、このデバイス クラスに対する自動再生がサポートされています](images/ap-tools.png)                   | ![windows 8.1 では、このデバイス クラスに対する自動再生がサポートされています](images/ap-tools.png)                   |
| デジタル ビデオ_カメラ      | ![windows 8 では、このデバイス クラスに対する自動再生がサポートされています](images/ap-tools.png)                   | ![windows 8.1 では、このデバイス クラスに対する自動再生がサポートされています](images/ap-tools.png)                   |
| ポータブル メディア プレーヤー        | ![windows 8 では、このデバイス クラスに対する自動再生がサポートされています](images/ap-tools.png)                   | ![windows 8.1 では、このデバイス クラスに対する自動再生がサポートされています](images/ap-tools.png)                   |
| 携帯電話                   | ![windows 8 では、このデバイス クラスに対する自動再生がサポートされています](images/ap-tools.png)                   | ![windows 8.1 では、このデバイス クラスに対する自動再生がサポートされています](images/ap-tools.png)                   |
| モバイル ブロードバンド             | ![windows 8 では、このデバイス クラスに対する自動再生がサポートされていません](images/app-tools-doesnotapply.png) | ![windows 8.1 では、このデバイス クラスに対する自動再生がサポートされていません](images/app-tools-doesnotapply.png) |
| Web カメラ                       | ![windows 8 では、このデバイス クラスに対する自動再生がサポートされていません](images/app-tools-doesnotapply.png) | ![windows 8.1 では、このデバイス クラスに対する自動再生がサポートされていません](images/app-tools-doesnotapply.png) |
| ヒューマン インターフェイス デバイス (HID) | ![windows 8 では、このデバイス クラスに対する自動再生がサポートされていません](images/app-tools-doesnotapply.png) | ![windows 8.1 では、このデバイス クラスに対する自動再生がサポートされています](images/ap-tools.png)                   |
| プリンター、スキャナー、fax      | ![windows 8 では、このデバイス クラスに対する自動再生がサポートされていません](images/app-tools-doesnotapply.png) | ![windows 8.1 では、このデバイス クラスに対する自動再生がサポートされていません](images/app-tools-doesnotapply.png) |
| PC                           | ![windows 8 では、このデバイス クラスに対する自動再生がサポートされていません](images/app-tools-doesnotapply.png) | ![windows 8.1 では、このデバイス クラスに対する自動再生がサポートされていません](images/app-tools-doesnotapply.png) |
| スマート カード                   | ![windows 8 では、このデバイス クラスに対する自動再生がサポートされていません](images/app-tools-doesnotapply.png) | ![windows 8.1 では、このデバイス クラスに対する自動再生がサポートされています](images/ap-tools.png)                   |
| 一般的なポート                 | ![windows 8 では、このデバイス クラスに対する自動再生がサポートされていません](images/app-tools-doesnotapply.png) | ![windows 8.1 では、このデバイス クラスに対する自動再生がサポートされています](images/ap-tools.png)                   |
| Bluetooth デバイス             | ![windows 8 では、このデバイス クラスに対する自動再生がサポートされていません](images/app-tools-doesnotapply.png) | ![windows 8.1 では、このデバイス クラスに対する自動再生がサポートされていません](images/app-tools-doesnotapply.png) |

 

## <a name="span-idbeforeyoubeginspanspan-idbeforeyoubeginspanspan-idbeforeyoubeginspanbefore-you-begin"></a><span id="Before_you_begin"></span><span id="before_you_begin"></span><span id="BEFORE_YOU_BEGIN"></span>始める前に


-   **デバイス メタデータの作成ウィザードがあるかどうかを確認**します。 自動再生を有効にする必要があります。 このリリースでは、このウィザードは Microsoft Visual Studio Professional および Microsoft Visual Studio Ultimate に含まれています。 Microsoft Visual Studio Express for Windows があれば、ダウンロードする必要がありますが、[スタンドアロン Windows 8.1 の SDK](https://go.microsoft.com/fwlink/p/?linkid=309209)ウィザードを取得します。

-   **Microsoft Store アプリを関連付ける**します。 アプリのパッケージについては、自動再生を有効にする必要があります。 詳細については、次を参照してください。、 *Microsoft Store アプリを関連付ける*セクション[手順 1。UWP デバイスのアプリ作成](step-1--create-a-uwp-device-app.md)です。

-   **デバイス メタデータを作成する**します。 まだを開始していない場合を参照してください。[手順 2。デバイス メタデータを作成する](step-2--create-device-metadata.md)で、[ステップ バイ ステップの UWP デバイスのアプリをビルド](build-a-uwp-device-app-step-by-step.md)ガイド。

## <a name="span-idenablingautoplayspanspan-idenablingautoplayspanspan-idenablingautoplayspanenabling-autoplay"></a><span id="Enabling_AutoPlay"></span><span id="enabling_autoplay"></span><span id="ENABLING_AUTOPLAY"></span>自動再生を有効にします。


**デバイス メタデータの作成ウィザード**UWP アプリをデバイスの既定の自動再生ハンドラーを宣言することができます。 その他の UWP アプリをデバイスの自動再生ハンドラーとして機能することもできます。 これらのオプションのいずれかまたは両方のオプションを選択できます。

**デバイス メタデータの作成ウィザードで自動再生を有効にするには**

1.  開始、**デバイス メタデータの作成ウィザード**から *%programfiles (x86) %*\\Windows キット\\8.1\\bin\\をダブルクリックして、x86**DeviceMetadataWizard.exe**します。
2.  クリックして**デバイス メタデータの編集**します。 これからは、既存のデバイス メタデータ パッケージを編集できます。
3.  **オープン** ダイアログ ボックスで、UWP デバイス アプリに関連付けられている、デバイス メタデータ パッケージを見つけます。 (これが、 **devicemetadata ms**ファイル拡張子)。
4.  (省略可能)デバイス アプリのパッケージ名、発行者名、および便利なアプリ ID を持っていない場合はクリックして**アプリ情報**UWP デバイス アプリのパッケージに関する情報を表示します。
5.  クリックして**Windows 情報**自動再生の詳細を指定します。
6.  アプリにし、デバイスの既定の自動再生ハンドラーを指定したい場合**UWP デバイスのアプリを使用して**します。 UWP アプリや UWP デバイスのアプリを選択することができますが、そのアプリがデバイスの自動再生のアクティブ化を処理し、(次の手順で指定) と同じアプリ パッケージ マニフェストで対応する操作 ID を指定する必要があります。
    -   **パッケージ名**:アプリ パッケージ マニフェストでの Identity 要素の Name 属性になります。
    -   **発行元名**:アプリ パッケージ マニフェストでは、Identity 要素の Publisher 属性です。
    -   **アプリ ID**:アプリ パッケージ マニフェストでアプリケーションの要素の ID 属性です。
    -   **動詞**:これは、自動再生のアクティブ化の識別子です。 アプリをデバイスからアクティブ化が付属しているかを判断に使用します。 動詞設定では、任意の値を使用するには除く**開く**は予約されています。
    -   **自動再生イベントの種類**:としてのままに**デバイス**します。 デバイス メタデータ、ウィザードでは UWP デバイス アプリに関連付けられているエクスペリエンスの ID を指定することが自動的に。

7.  他のアプリを選択し、デバイスの自動再生ハンドラーとして機能できるようにする場合**登録済みのアプリの自動再生を有効にする**します。
8.  完了したら、クリックして**次**します。
9.  表示された場合、**完了** ページで、メモ、**エクスペリエンス ID**します。 必要になります次の手順で、アプリで自動再生のアクティブ化を処理するときにします。
10. 確認、**情報を保存** をクリック**保存**デバイス メタデータ パッケージを更新します。

## <a name="span-idhandlingautoplayactivationspanspan-idhandlingautoplayactivationspanspan-idhandlingautoplayactivationspanhandling-autoplay-activation"></a><span id="Handling_AutoPlay_activation"></span><span id="handling_autoplay_activation"></span><span id="HANDLING_AUTOPLAY_ACTIVATION"></span>自動再生のアクティブ化の処理


アプリの自動再生アクティブ化を処理するために登録する必要があります、`windows.autoPlayDevice`アプリ パッケージの拡張機能マニフェストし、では、そのイベントを処理し、`OnActivated`アプリケーション オブジェクトのイベント。 複数のデバイスの自動再生ハンドラーとして登録できることに注意してください。

### <a name="span-idtoregisteryourappasanautoplayhandlerspanspan-idtoregisteryourappasanautoplayhandlerspanspan-idtoregisteryourappasanautoplayhandlerspanto-register-your-app-as-an-autoplay-handler"></a><span id="To_register_your_app_as_an_AutoPlay_handler"></span><span id="to_register_your_app_as_an_autoplay_handler"></span><span id="TO_REGISTER_YOUR_APP_AS_AN_AUTOPLAY_HANDLER"></span>自動再生ハンドラーとしてアプリを登録するには

デバイスの自動再生ハンドラーとしてアプリを登録するには、UWP デバイス アプリと、自動再生に関連付けられているエクスペリエンスの ID を指定する必要があります**動詞**と**ActionDisplayName**するために使用されます。アプリをアクティブにします。

1.  Microsoft Visual Studio でアプリのプロジェクトを開きます。
2.  **ソリューション エクスプ ローラー**を右クリックし、 **Package.appxmanifest**ファイルおよび選択**コードの表示**します。 これにより、アプリのパッケージ マニフェストが XML (テキスト) エディターに表示されます。
3.  `Application`要素下の`VisualElements`要素では、以下を貼り付けます`Extensions`要素をパッケージ マニフェスト ファイルにします。
    ```XML
          <Extensions>
            <Extension Category="windows.autoPlayDevice">
              <AutoPlayDevice>
                <LaunchAction
                    Verb="showDevice1"
                    ActionDisplayName="Launch App for Device 1"
                    DeviceEvent="ExperienceID:{00000000-ABCD-EF00-0000-000000000000}"/>
              </AutoPlayDevice>
            </Extension>
          </Extensions>
    ```

4.  この例からの自動再生の値をアプリの実際の値に置き換えます。
    -   `Verb` :これは、自動再生のアクティブ化の識別子です。 アプリをデバイスからアクティブ化が付属しているかを判断に使用します。 この値に一致する必要があります、アプリは、デバイスの既定の自動再生ハンドラーとして指定されている場合、**動詞**デバイスのメタデータで指定しました。 アプリがデバイスの既定の自動再生ハンドラーとして指定されていない場合、動詞の設定では、任意の値を使用以外の**開く**、これは予約されています。
    -   `ActionDisplayName` :この文字列は、アプリの自動再生が表示されます。
    -   `Experience ID` :エクスペリエンスは、アプリをデバイスに関連付けられる ID の GUID。 これは、前の手順でメモした値です。

### <a name="span-idtohandleautoplayactivationspanspan-idtohandleautoplayactivationspanspan-idtohandleautoplayactivationspanto-handle-autoplay-activation"></a><span id="To_handle_AutoPlay_activation"></span><span id="to_handle_autoplay_activation"></span><span id="TO_HANDLE_AUTOPLAY_ACTIVATION"></span>自動再生のアクティブ化を処理するには

ライセンス認証の種類になりますが、デバイスには、自動再生のアクティブ化がトリガーされた場合`Windows.ApplicationModel.Activation.ActivationKind.device`します。 使用して、`eventObj`によって渡されるオブジェクト`OnActivated`アプリをアクティブにする方法を確認します。 自動再生の場合、使用できます`eventObj`をアクティブ化の原因とするデバイス ID と自動再生動詞を決定します。

この例では、アクティブ化イベントのパラメーター (eventObj) は、アクティブ化の動詞と同様に、デバイスの ID を実行します。

```JavaScript
<!DOCTYPE html>
<html>
<head>
  <script type="text/javascript">
    function OnActivated(eventObj) {
        if (eventObj.kind == Windows.ApplicationModel.Activation.ActivationKind.launch) {
            // Activated by the user.
        }
        else if (eventObj.kind == Windows.ApplicationModel.Activation.ActivationKind.device) {
            // Activated by a device, for AutoPlay.
            // Device path = eventObj.deviceInformationId;
            // verb (“showDevice1”) = eventObj.verb;
        }
    }

    Windows.UI.WebUI.WebUIApplication.addEventListener("activated", OnActivated, false);
  </script>
</head>

<body>
...
...
...
</body>
</html>
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[UWP デバイス アプリを満たす](meet-uwp-device-apps.md)

[UWP デバイス アプリのビルド手順](build-a-uwp-device-app-step-by-step.md)

[自動再生による自動起動](https://go.microsoft.com/fwlink/p/?LinkID=254861)

[起動する、再開、およびマルチタス キング](https://go.microsoft.com/fwlink/p/?LinkID=309316)

 

 






