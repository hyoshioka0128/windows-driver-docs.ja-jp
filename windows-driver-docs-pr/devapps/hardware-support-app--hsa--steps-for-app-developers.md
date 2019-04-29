---
title: アプリ開発者のためのハードウェア サポート アプリ (HSA) の手順
description: カスタムの機能を備えたハードウェア サポート アプリ (HSA) の開発ガイドします。
keywords:
- ユーザー設定 機能
- UWP アプリ
- カスタムの機能
- UWP
- ハードウェア
ms.date: 08/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e9f45b8c1005a42b8905086d9f1d3038c8ec1130
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330708"
---
# <a name="hardware-support-app-hsa-steps-for-app-developers"></a>ハードウェア サポート アプリ (HSA):アプリ開発者向けの手順

このトピックでは、ドライバーを使用して、デバイス固有のアプリに関連付ける方法を説明しますまたは[RPC (リモート プロシージャ コール)](https://msdn.microsoft.com/library/windows/desktop/aa378651)エンドポイント。  このような形で組み合わせると、ハードウェア サポート アプリ (HSA) として、アプリを参照します。  配布し、Microsoft Store を通じてハードウェア サポートのアプリを更新できます。

いずれかで始まり、[ユニバーサル Windows プラットフォーム (UWP) アプリ](https://docs.microsoft.com/windows/uwp/get-started/universal-application-platform-guide)またはデスクトップ (Win32) アプリです。  デスクトップ アプリを使用する場合を使用して、[デスクトップ ブリッジ](https://docs.microsoft.com/windows/uwp/porting/desktop-to-uwp-root)ストアにアップロードできる Windows アプリ パッケージを作成します。

このページは、UWP アプリでは、手順を説明しますが、手順は Win32 オプションに似ています。 

ドライバー開発者向けの手順が記載されて[ハードウェア サポート アプリ (HSA)。Steps for Driver Developers (ハードウェア サポート アプリ (HSA): ドライバー開発者向け手順)](hardware-support-app--hsa--steps-for-driver-developers.md)」をご覧ください。

## <a name="getting-started"></a>作業の開始

まず、Visual Studio の最新バージョンをインストールし、UWP アプリ プロジェクトを作成します。  カスタム機能を使った UWP アプリをビルドするには、Windows SDK バージョン 10.0.15063 追加されたため (Windows 10 Creators Update) を必要がありますまたはそれ以降。 プロジェクト ファイルは、バージョン 10.0.15063 追加されたためを指定する必要がありますもまたはそれ以降。 構成の取得の詳細については、次を参照してください。[開発の UWP アプリの Visual Studio を使用して](/windows/uwp/develop/)します。

Windows 10 バージョン 1709 以降、特定のドライバーが存在する場合に、ユニバーサル Windows プラットフォーム (UWP) アプリがのみ読み込むことを指定できます。  学習する方法についてを参照してください[UWP アプリでのドライバーをペアリング](../install/pairing-app-and-driver-versions.md)します。

## <a name="create-a-microsoft-store-account"></a>Microsoft Store アカウントを作成します。

Microsoft Store での開発者アカウントが必要です。 ハードウェア パートナーには、そのハードウェア パートナーのアカウントとは異なる Microsoft Store のアカウントが必要です。 アプリケーション マニフェストと後の手順でデバイスのメタデータを作成するときに、発行元名が必要があります。 ストアのプロファイルを作成したら、アプリの名前を予約することもできます。

Microsoft Store アカウントを作成するには、 [UWP アプリのサインアップ ページ](https://go.microsoft.com/fwlink/p/?LinkId=302197)します。 詳細については、次を参照してください。[開発者アカウントを開く](https://docs.microsoft.com/windows/uwp/publish/opening-a-developer-account)します。

## <a name="choosing-a-programming-language-for-the-app"></a>アプリのプログラミング言語の選択

使用することができる場合、アプリは、ドライバーと通信、 [Windows.Devices.Custom](https://docs.microsoft.com/uwp/api/windows.devices.custom)、これは、WinRT API の一部であるため、JavaScript では、使用可能なC#、および C++。

場合は、アプリは、NT サービスと通信、RPC Api を使用する必要があります。  RPC Api は、WinRT では使用できない Win32 Api であるため、C++ を使用するか、.NET interop (PInvoke) を使用して RPC 呼び出しをラップする必要があります。  詳細については、次を参照してください。[マネージ コードからネイティブ関数の呼び出し](https://docs.microsoft.com/cpp/dotnet/calling-native-functions-from-managed-code)します。

## <a name="contact-the-custom-capability-owner"></a>カスタムの機能の所有者にお問い合わせください。

機能の所有者からカスタムの機能にアクセスを要求する準備ができました。  次の情報を収集する必要があります。

-   Microsoft Store からアプリの PFN (パッケージ ファミリ名)
-   カスタムの機能の名前
-   Certutil.exe を使用して、.cer ファイルから生成される証明書の署名、アプリの署名ハッシュです。 証明書は、sha-256 である必要があります。

署名のハッシュを生成するには、実行`C:\Windows\System32\certutil.exe -dump CertificateName.cer`します。

下部に表示される署名のハッシュを SHA256 になったことを確認します。  それ以外の場合、SHA256 証明書を使用してアプリに署名します。  このよう、結果になります。

```cpp
Signature Hash:
ca9fc964db7e0c2938778f4559946833e7a8cfde0f3eaa07650766d4764e86c4
```

機能の所有者では、この情報を使用して、生成、[カスタム機能の記述子を署名](hardware-support-app--hsa--steps-for-driver-developers.md#sccd-xml-schema)ファイルを開き、アプリ開発者にこのファイルを送信します。

アプリ開発者は、要求を承認する機能の所有者の待機中に開発者モードでカスタム機能を使用してアプリの開発を続行できます。 たとえば、次を使用してでデスクトップ PC で SCCD で[開発者モード](https://docs.microsoft.com/windows/uwp/get-started/enable-your-device-for-development):

-   SCCD 内のエントリをカタログします。

    ```xml
    <Catalog>FFFF</Catalog>
    ```
-   承認されたエンティティのエントリ、SCCD で証明書署名ハッシュです。 適用も、検証には、中に 64 文字のシーケンスに配置してください。

    ```xml
    <AuthorizedEntity AppPackageFamilyName="MicrosoftHSATest.Microsoft.SDKSamples.Hsa.CPP_q536wpkpf5cy2" CertificateSignatureHash="ca9fc964db7e0c2938778f4559946833e7a8cfde0f3eaa07650766d4764e86c4"></AuthorizedEntity>
    ```

## <a name="add-a-custom-capability-to-the-app-package-manifest"></a>アプリ パッケージのマニフェストにカスタム機能を追加します。

次に、変更、[アプリ パッケージのマニフェスト](https://msdn.microsoft.com/library/windows/apps/BR211474)ソース ファイル (`Package.appxmanifest`) 機能の属性を含める。

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

Appx パッケージのパッケージ ルートに SCCD ファイルをコピーします。 Visual Studio のソリューション エクスプ ローラーで右クリック"プロジェクト -&gt;追加 -&gt;既存のアイテムの..." SCCD をプロジェクトに追加します。

![Appx パッケージに SCCD ファイルを追加します。](images/addSCCDToAppx.png)

マーク SCCD ファイルを右クリックし、変更によってコンテンツをビルドとして SCCD**コンテンツ**に**True**します。  C#プロジェクトで、プロパティを使用して`Build Action = Content`、JavaScript プロジェクトの場合は、使用および`Package Action = Content`します。 

![SCCD をコンテンツとしてマークします。](images/markSCCDAsContent.png)

最後に、プロジェクトを右クリックし、選択**ストア**、し**アプリ パッケージの作成**です。

**注意**:モバイル プラットフォームでのカスタム機能を備えた UWP アプリのサポートはありません。

## <a name="install-the-app"></a>アプリをインストールします。

使用済みのカスタム機能を使った UWP アプリをインストールする[DISM - Deployment Image Servicing and Management](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism---deployment-image-servicing-and-management-technical-reference-for-windows)します。

## <a name="troubleshooting"></a>トラブルシューティング

開発者モードで、ターゲット マシンがある場合は、アプリの登録エラーをデバッグするには、次の手順を実行できます。

1.  AppX マニフェストからのカスタム機能のエントリを削除します。
2.  アプリをビルドして展開します。
3.  PowerShell ウィンドウで、入力`Get-AppxPackage`します。
4.  一覧で、アプリを検索し、アプリと同じパッケージ ファミリ名を確認します。
5.  パッケージ ファミリ名を持つ、SCCD を更新します。
6.  AppX マニフェストにカスタム機能のエントリを追加します。
7.  再構築して展開します。 

## <a name="see-also"></a>関連項目

* [ハードウェア サポート アプリ (HSA):ドライバー開発者向け手順](hardware-support-app--hsa--steps-for-driver-developers.md)
* [開発用にデバイスを有効にします。](https://docs.microsoft.com/windows/uwp/get-started/enable-your-device-for-development)
* [カスタムの機能のサンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/CustomCapability)
* [ユニバーサル Windows ドライバーの概要](../develop/getting-started-with-universal-drivers.md)
* [ユニバーサル Windows プラットフォーム (UWP) アプリとドライバーのペアリング](../install/pairing-app-and-driver-versions.md)
* [ユニバーサル Windows プラットフォームの紹介](https://docs.microsoft.com/windows/uwp/get-started/universal-application-platform-guide)
* [ユニバーサル Windows プラットフォーム (UWP)](https://docs.microsoft.com/windows/uwp/design/basics/design-and-ui-intro)
