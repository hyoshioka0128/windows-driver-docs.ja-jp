---
title: V4 ドライバー UI アーキテクチャ
description: V4 ドライバーアーキテクチャの設計上の目標は、Microsoft Store アプリのユーザーインターフェイスの組み込みサポートを提供することでした。
ms.assetid: 6318E480-C567-4866-8E88-B19904408C59
ms.date: 09/28/2018
ms.localizationpriority: medium
ms.openlocfilehash: 8419a777f40fb5dbfa2db76e6d5d93faecd55861
ms.sourcegitcommit: 3fbf71b2bd92abca0bfb3c373f57af9a0eb67c93
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/09/2020
ms.locfileid: "75775730"
---
# <a name="v4-driver-ui-architecture"></a>V4 ドライバー UI アーキテクチャ

V4 ドライバーアーキテクチャの設計上の目標は、Microsoft Store アプリのユーザーインターフェイスの組み込みサポートを提供することでした。

この例では、アプリケーションベースの UI パラダイムが採用されています。 UWP デバイスアプリは、Microsoft Store アプリ UI でサポートされている全画面表示エクスペリエンスをユーザーに提供します。 印刷用 UWP デバイスアプリは、印刷設定の機能拡張と、v4 印刷ドライバーをサポートするプリンターのプリンター通知を提供します。 印刷用の UWP デバイスアプリでは、新しいスタート画面で印刷デバイスを表示することもできます。

プリンター拡張アプリは、ユーザーが Windows デスクトップで既存のアプリケーションを実行するときの印刷設定とプリンター通知をサポートしています。 これらのアプリケーションの Ui は非常に異なりますが、タッチ用に調整されたものと、マウスとキーボードのユーザー向けに最適化されたものがありますが、UI に関係なく、ビジネスロジックと v4 印刷ドライバーへの接続は似ています。

次の図は、GitHub で提供されている[V4 印刷ドライバーとプリンター拡張のサンプル](https://github.com/Microsoft/Windows-driver-samples/tree/master/print/v4PrintDriverSamples)用の Microsoft Store デバイスアプリの高レベルなアーキテクチャを示しています。

![カスタム ui アーキテクチャの概要](images/v4custuiarch.png)

上の図に示すように、モデル/ビュー/コントローラーベースのアーキテクチャにより、アプリは、でC#記述されたモデルレイヤーでコードを共有できます。

## <a name="extending-printerextensionlibrary"></a>プリンター Extensionlibrary の拡張

さまざまなサンプルに収録されているプリンター Extensionlibrary プロジェクトは、新しいクラスを使用するか、指定された一連のクラスを拡張することによって拡張できます。 Microsoft はサンプルコードを定期的に更新するため、提供されたソースファイルに対して実行するコード変更の数は、パートナーが最小限にすることをお勧めします。 提供された一連のクラスを拡張するパートナーの場合は、既存のクラスを "partial" としてマークし、新しい関数またはオーバーライドを別のソースファイルに追加することをお勧めします。

## <a name="sharing-compiled-binaries-between-uwp-apps-and-desktop-apps"></a>UWP アプリとデスクトップアプリ間でコンパイル済みバイナリを共有する

Microsoft Store デバイスアプリとプリンター拡張機能のサンプルに付属しているプリンターの Extensionlibrary プロジェクトでは、同じソースコードを使用しますが、プロジェクト間の移植性を確保するために、個別にビルドしなくてもコードをビルドすることが重要な場合があります。作品. プリンター Extensionlibrary プロジェクトのコードを移植できるようにするには、プロジェクトをポータブルクラスライブラリに変換する必要があります。 変換を行うには、次の手順を実行します。

1. Microsoft Visual Studio で、**ファイル** > **新しい** > **プロジェクト** をクリックし、**インストールされたテンプレートの検索** ボックスで ポータブル を検索します。

2. ポータブルクラスライブラリ] C#ビジュアルを選択し、 **[名前]** テキストボックスにプロジェクトの名前を指定して、[OK をクリックし**ます。**

3. 既存のプリンター Extensionlibrary プロジェクトから新しいプロジェクトにソースコードをコピーします。

4. ポータブルクラスライブラリプロジェクトを右クリックし、 **[アンロード]** を選択します。 次に、.csproj ファイルを開き、ドキュメントの最後のタグの直前に、次のセクションをファイルに追加します。

    ```xml
      <ItemGroup>
        <COMReference Include="PrinterExtensionLib">
          <Guid>{91CE54EE-C67C-4B46-A4FF-99416F27A8BF}</Guid>
          <VersionMajor>1</VersionMajor>
          <VersionMinor>0</VersionMinor>
          <Lcid>0</Lcid>
          <WrapperTool>tlbimp</WrapperTool>
          <Isolated>False</Isolated>
          <EmbedInteropTypes>True</EmbedInteropTypes>
        </COMReference>
      </ItemGroup>
    ```

5. COM 参照の結果として警告が表示された場合は、\<PropertyGroup\> タグに次のを追加します。

```xml
<ResolveComReferenceSilent>true</ResolveComReferenceSilent>
```

## <a name="api-for-print-ui-scenarios"></a>印刷 UI シナリオ用 API

API は、印刷用のプリンター拡張機能と UWP デバイスアプリをサポートするために、v4 印刷ドライバーモデルの一部として開発されました。 大まかに言えば、印刷設定のシナリオでは、PrintTicket、PrintCapabilities、および新しいプロパティバッグを使用して、すべての情報を取得し、格納します。 プリンター通知は、双方向通信 (Bidi) スキーマに基づく新しいイベントシステムによって駆動されます。この新しいシステムでは、クライアントとサーバーの間で AsyncUI プロトコルを使用します。 この API のデータ中心の性質は、1つのアプリケーションが多くのデバイスを簡単にサポートできることを意味します。

要求されたデータを使用できない場合は、プリンターの拡張機能を適切に低下させるように構築する必要があります。 たとえば、特定の PrintCapabilities 機能が使用できない場合や、いずれかのプロパティバッグ内のプロパティが使用できない場合は、アプリの残りの部分が機能しないようにする必要があります。 プロパティバッグまたはプロパティバッグ内の特定のプロパティにアクセスする場合、スローされる例外が発生してもアプリがクラッシュしないようにするために、アプリは try-catch 構文を使用する必要があります。 詳細については、「[プリンター拡張機能インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/index#interfaces)」を参照してください。

## <a name="related-resources"></a>関連リソース

[プリンター拡張インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/#interfaces)

[GitHub の v4 印刷ドライバーのサンプル](https://github.com/Microsoft/Windows-driver-samples/tree/master/print/v4PrintDriverSamples)
