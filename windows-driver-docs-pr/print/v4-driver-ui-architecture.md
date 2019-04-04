---
title: V4 ドライバー UI アーキテクチャ
description: Microsoft Store アプリのユーザー インターフェイスの組み込みサポートを提供すること、v4 ドライバー アーキテクチャの大まかな設計目標でした。
ms.assetid: 6318E480-C567-4866-8E88-B19904408C59
ms.date: 09/28/2018
ms.localizationpriority: medium
ms.openlocfilehash: ddb6a7e4feb816b79aa9f366bff0883f79b7c120
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580542"
---
# <a name="v4-driver-ui-architecture"></a>V4 ドライバー UI アーキテクチャ

Microsoft Store アプリのユーザー インターフェイスの組み込みサポートを提供すること、v4 ドライバー アーキテクチャの大まかな設計目標でした。

導入されているアプリケーションに基づく UI パラダイムでは、この明確な例を示します。 UWP デバイス アプリでは、Microsoft Store アプリの UI でサポートされている全画面表示エクスペリエンスを持つユーザーを提供します。 印刷用の UWP デバイス アプリが印刷の設定の拡張機能を提供し、印刷ドライバーを v4 をサポートするプリンターのプリンターを通知します。 印刷用の UWP デバイス アプリでは、新しいスタート画面で、印刷デバイスの可視性を提供します。

プリンター拡張アプリは、ユーザーが Windows デスクトップで既存のアプリケーションを実行すると、印刷設定とプリンターの通知をサポートします。 向けにタッチ、マウスとキーボードのユーザー用に最適化されたもう 1 つではこれらのアプリケーションの Ui が大きく異なる、ビジネス ロジックと v4 印刷ドライバーへの接続にも似ていますが、UI に関係なく。

次の図は向け Microsoft Store デバイス アプリの高レベルのアーキテクチャ、 [v4 プリンター ドライバーとプリンターの拡張機能サンプル](https://github.com/Microsoft/Windows-driver-samples/tree/master/print/v4PrintDriverSamples)github に用意されています。

![カスタム ui のアーキテクチャの概要](images/v4custuiarch.png)

前の図に示すように、モデル/ビュー/コント ローラー ベースのアーキテクチャにより、層では、モデルで記述されたコードを共有するアプリC#します。

## <a name="extending-printerextensionlibrary"></a>PrinterExtensionLibrary を拡張します。

さまざまなサンプルに付属している PrinterExtensionLibrary プロジェクトは、新しいクラスを使用して、拡張またはクラスのセットを指定された拡張できます。 マイクロソフトは、サンプル コードに更新プログラムを定期的には、ために、パートナーに指定されたソース ファイルに行ったコード変更の数が最小限に抑える必要がありますをお勧めします。 指定された一連のクラスを拡張するパートナーの場合は、既存のクラスを"partial"としてマークし、別のソース ファイルで新しい関数または上書きを追加することお勧めします。

## <a name="sharing-compiled-binaries-between-uwp-apps-and-desktop-apps"></a>コンパイル済みバイナリを UWP アプリとデスクトップ アプリとの間の共有

Microsoft Store のデバイスのアプリとプリンターの拡張機能のサンプルに付属している PrinterExtensionLibrary プロジェクトには、同じのソース コードが利用しながら、ごとに個別に作成されることがなくプロジェクト間で移植性のためにコードをビルドする役に立つ可能性があります。プロジェクトです。 PrinterExtensionLibrary プロジェクトのコードを移植するためには、ポータブル クラス ライブラリをプロジェクトに変換があります。 変換を行うには、次の手順を実行します。

1. Microsoft Visual studio で次のようにクリックします**ファイル** &gt; **新規** &gt; **プロジェクト**、で"ポータブル"を検索し、**検索。インストールされたテンプレート**ボックス。

2. ポータブル クラス ライブラリ Visual 選択C#、プロジェクトの名前を指定し、**名前**テキスト ボックスをクリックします **[ok]。**

3. 新しいプロジェクトに既存の PrinterExtensionLibrary プロジェクトからソース コードをコピーします。

4. ポータブル クラス ライブラリ プロジェクトを右クリックし、選択**アンロード**します。 .Csproj ファイルを開きし、ファイル、ドキュメントの最後のタグの直前に次のセクションを追加します。

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

5. 追加するには、次の COM 参照の結果として警告を表示する場合、 &lt;PropertyGroup&gt;タグ。

```xml
<ResolveComReferenceSilent>true</ResolveComReferenceSilent>
```

## <a name="api-for-print-ui-scenarios"></a>印刷の UI シナリオ用の API

API は、印刷用のプリンター拡張と UWP デバイス用アプリケーションをサポートするために v4 印刷ドライバー モデルの一部として開発されました。 高レベルは、印刷設定のシナリオは、取得し、すべての情報を格納する PrintTicket、PrintCapabilities と新しいプロパティ バッグを使用します。 プリンターの通知は、双方向通信 (Bidi) スキーマに基づいている新しいイベント システムによって駆動し、この新しいシステムがクライアントとサーバー間 AsyncUI プロトコルを使用します。 この API のデータ中心の性質は、1 つのアプリケーションは、多くのデバイスに簡単にサポート可能性がありますを意味します。

プリンターの拡張機能は、ことが適切に低下することが要求されたデータが利用できない場合、このような方法でビルドする必要があります。 たとえば、特定 PrintCapabilities 機能が使用できない場合、またはプロパティ バッグのいずれかのプロパティが使用できない場合は、これする必要がありますいないしなく、アプリの残りの部分。 プロパティ バッグ、またはプロパティ バッグ内の特定のプロパティにアクセスするとき、アプリは、スローされる例外には、アプリのクラッシュが発生しないことを確認するには、try-catch 構文を使用する必要があります。 詳細については、[プリンター拡張機能インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/index#interfaces)を参照してください。

## <a name="related-resources"></a>関連リソース

[プリンター拡張機能インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/#interfaces)

[GitHub の v4 プリンター ドライバーのサンプル](https://github.com/Microsoft/Windows-driver-samples/tree/master/print/v4PrintDriverSamples)



