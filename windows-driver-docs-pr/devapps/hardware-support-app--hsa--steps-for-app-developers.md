---
title: アプリ開発者向けのハードウェアサポートアプリ (HSA) の手順
description: カスタム機能でハードウェアサポートアプリ (HSA) を開発するためのガイド
keywords:
- カスタム、機能
- UWP アプリ
- カスタム機能
- UWP
- ハードウェア
ms.date: 08/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed2ed079ee815762a788ec37c62cbb53f1efd621
ms.sourcegitcommit: 958a5ced83856df22627c06eb42c9524dd547906
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83235425"
---
# <a name="hardware-support-app-hsa-steps-for-app-developers"></a>ハードウェアサポートアプリ (HSA): アプリ開発者向けの手順

このトピックでは、デバイス固有のアプリをドライバーまたは[RPC (リモートプロシージャコール)](https://docs.microsoft.com/windows/desktop/Rpc/rpc-start-page)エンドポイントに関連付ける方法について説明します。  この方法でペアにすると、アプリはハードウェアサポートアプリ (HSA) と呼ばれます。  Microsoft Store を使用して、ハードウェアサポートアプリを配布および更新できます。

[ユニバーサル Windows プラットフォーム (UWP) アプリ](https://docs.microsoft.com/windows/uwp/get-started/universal-application-platform-guide)またはデスクトップ (Win32) アプリから開始します。  デスクトップアプリを使用する場合は、[デスクトップブリッジ](https://docs.microsoft.com/windows/uwp/porting/desktop-to-uwp-root)を使用して、ストアにアップロードできる Windows アプリパッケージを作成します。

このページでは、UWP アプリの手順について説明しますが、手順は Win32 オプションの場合と似ています。 

ドライバー開発者向けの手順については、「[ハードウェアサポートアプリ (HSA): ドライバー開発者向けの手順](hardware-support-app--hsa--steps-for-driver-developers.md)」を参照してください。

## <a name="getting-started"></a>作業の開始

まず、Visual Studio の最新バージョンをインストールし、UWP アプリプロジェクトを作成します。  カスタム機能を備えた UWP アプリをビルドするには Windows SDK バージョン 10.0.15063 (Windows 10 の作成者の更新) 以降が必要です。 プロジェクトファイルでは、バージョン10.0.15063 以上も指定する必要があります。 構成の詳細については、「 [Visual Studio を使用した UWP アプリの開発](/windows/uwp/develop/)」を参照してください。

Windows 10 バージョン1709以降では、特定のドライバーが存在する場合にのみ、ユニバーサル Windows プラットフォーム (UWP) アプリを読み込むように指定できます。  詳細については、「[ドライバーと UWP アプリのペアリング](../install/pairing-app-and-driver-versions.md)」を参照してください。

## <a name="create-a-microsoft-store-account"></a>Microsoft Store アカウントを作成する

Microsoft Store の開発者アカウントが必要です。 ハードウェアパートナーには、ハードウェアパートナーアカウントとは異なる Microsoft Store アカウントが必要です。 後の手順でアプリマニフェストとデバイスメタデータを作成するときに、発行者名が必要になります。 ストアプロファイルを作成したら、アプリの名前を予約することもできます。

Microsoft Store アカウントを作成するには、 [UWP アプリのサインアップページ](https://go.microsoft.com/fwlink/p/?LinkId=302197)にアクセスします。 詳細については、「[開発者アカウントを開く](https://docs.microsoft.com/windows/uwp/publish/opening-a-developer-account)」を参照してください。

## <a name="choosing-a-programming-language-for-the-app"></a>アプリのプログラミング言語の選択

アプリがドライバーと通信する場合は、WinRT API の一部である[Windows. Devices. Custom](https://docs.microsoft.com/uwp/api/windows.devices.custom)を使用できます。そのため、JavaScript、C#、および C++ で使用できます。

アプリが NT サービスと通信する場合は、RPC Api を使用する必要があります。  RPC Api は WinRT では使用できない Win32 Api なので、C++ を使用するか、.NET interop (PInvoke) を使用して RPC 呼び出しをラップする必要があります。  詳細については、「[マネージコードからのネイティブ関数の呼び出し](https://docs.microsoft.com/cpp/dotnet/calling-native-functions-from-managed-code)」を参照してください。

## <a name="contact-the-custom-capability-owner"></a>カスタム機能の所有者に問い合わせる

これで、機能所有者からカスタム機能へのアクセスを要求する準備ができました。  次の情報を収集する必要があります。

-   Microsoft Store からの App PFN (パッケージファミリ名)
-   カスタム機能の名前
-   アプリケーション署名証明書の署名ハッシュ。 certutil を使用して .cer ファイルから生成できます。 証明書は SHA-256 である必要があります。

署名ハッシュを生成するには、を実行 `C:\Windows\System32\certutil.exe -dump CertificateName.cer` します。

下部の近くにある署名ハッシュを探し、SHA256 であることを確認します。  それ以外の場合は、SHA256 証明書を使用してアプリに署名します。  結果は次のようになります。

```cpp
Signature Hash:
ca9fc964db7e0c2938778f4559946833e7a8cfde0f3eaa07650766d4764e86c4
```

機能の所有者は、この情報を使用して、署名された[カスタム機能記述子](hardware-support-app--hsa--steps-for-driver-developers.md#sccd-xml-schema)ファイルを生成し、このファイルをアプリの開発者に送信します。

アプリ開発者は、機能所有者が要求を承認するまでの間、開発者モードでカスタム機能を使用してアプリを開発し続けることができます。 たとえば、[開発者モード](https://docs.microsoft.com/windows/uwp/get-started/enable-your-device-for-development)のデスクトップ PC では、SCCD で次のコードを使用します。

-   SCCD のカタログエントリ。

    ```xml
    <Catalog>FFFF</Catalog>
    ```
-   SCCD の承認されたエンティティエントリの証明書署名ハッシュ。 強制も検証もされていませんが、64-char シーケンスを入力してください。

    ```xml
    <AuthorizedEntity AppPackageFamilyName="MicrosoftHSATest.Microsoft.SDKSamples.Hsa.CPP_q536wpkpf5cy2" CertificateSignatureHash="ca9fc964db7e0c2938778f4559946833e7a8cfde0f3eaa07650766d4764e86c4"></AuthorizedEntity>
    ```

## <a name="add-a-custom-capability-to-the-app-package-manifest"></a>アプリケーションパッケージマニフェストにカスタム機能を追加する

次に、[アプリパッケージのマニフェスト](https://docs.microsoft.com/uwp/schemas/appxpackage/appx-package-manifest)ソースファイル () を変更して、 `Package.appxmanifest` 機能属性を含めます。

```xml
<?xml version="1.0" encoding="utf-8"?>
<Package
  ...
  xmlns:uap4="http://schemas.microsoft.com/appx/manifest/uap/windows10/4">
...
<Capabilities>
    <uap4:CustomCapability Name="CompanyName.customCapabilityName_PublisherID"/>
</Capabilities>
</Package>
```

次に、SCCD ファイルを appx パッケージのパッケージルートにコピーします。 Visual Studio のソリューションエクスプローラーで、[プロジェクト- &gt; &gt; 既存項目の追加...] を右クリックします。 SCCD をプロジェクトに追加します。

![SCCD ファイルを appx パッケージに追加する](images/addSCCDToAppx.png)

SCCD ファイルを右クリックし、[**コンテンツ**] を [ **True**] に変更して、ビルドコンテンツとして SCCD をマークします。  C# プロジェクトの場合は、プロパティ `Build Action = Content` を使用します。 JavaScript プロジェクトの場合は、を使用し `Package Action = Content` ます。 

![SCCD をコンテンツとしてマークする](images/markSCCDAsContent.png)

最後に、プロジェクトを右クリックし、[**ストア**]、[**アプリパッケージの作成**] の順に選択します。

**注**: モバイルプラットフォームにカスタム機能を持つ UWP アプリはサポートされていません。

## <a name="install-the-app"></a>アプリをインストールする

カスタム機能を備えた UWP アプリを事前にインストールするには、 [DISM-展開イメージのサービスと管理](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism---deployment-image-servicing-and-management-technical-reference-for-windows)を使用します。

## <a name="troubleshooting"></a>トラブルシューティング

ターゲットコンピューターが開発者モードの場合は、次の手順を実行して、アプリの登録エラーをデバッグできます。

1.  AppX マニフェストからカスタム機能のエントリを削除します。
2.  アプリをビルドしてデプロイします。
3.  PowerShell ウィンドウで、「」と入力 `Get-AppxPackage` します。
4.  一覧でアプリを探し、アプリの厳密なパッケージファミリ名を確認します。
5.  パッケージファミリ名を使用して SCCD を更新します。
6.  カスタム機能のエントリを AppX マニフェストに再び追加します。
7.  リビルドとデプロイ。 

## <a name="see-also"></a>参照

* [ハードウェアサポートアプリ (HSA): ドライバー開発者向けの手順](hardware-support-app--hsa--steps-for-driver-developers.md)
* [デバイスを開発用に有効にする](https://docs.microsoft.com/windows/uwp/get-started/enable-your-device-for-development)
* [カスタム機能のサンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/CustomCapability)
* [Windows ドライバーでのはじめに](../develop/getting-started-with-windows-drivers.md)
* [ドライバーとユニバーサル Windows プラットフォーム (UWP) アプリとのペアリング](../install/pairing-app-and-driver-versions.md)
* [ユニバーサル Windows プラットフォームの紹介](https://docs.microsoft.com/windows/uwp/get-started/universal-application-platform-guide)
* [ユニバーサル Windows プラットフォーム (UWP)](https://docs.microsoft.com/windows/uwp/design/basics/design-and-ui-intro)
