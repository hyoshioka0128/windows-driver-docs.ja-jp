---
title: パートナーの設定アプリを作成する
description: パートナーの設定アプリを作成する
ms.assetid: 3b549c11-f8b2-46e8-9d22-4edc787743ee
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 64e15e9175a87c5bb64a027b20d22b4313b1a6db
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577692"
---
# <a name="create-a-partner-settings-app"></a>パートナーの設定アプリを作成する

Oem および携帯電話会社は、その他のデバイスと区別できるデバイスのハードウェア機能向けのカスタム設定を公開できます。 例としては、スピーカー、センサー、またはマイクです。 最大 5 つは、これらのカスタム設定は、設定アプリの 2 つのページ レベルのいずれかでその他のリンクとして表示されます。  

たとえば、**デバイス**のタブ、**設定**アプリケーションでは、次のページの各最大個保持できますカスタム設定アプリへの 5 つの追加リンク。

* プリンターとスキャナー
* 接続されたデバイス
* Bluetooth
* マウス
* タッチパッド
* 入力
* ペンと Windows Ink
* 自動再生
* USB

![設定アプリでデバイスの一覧](images/devices-list-in-settings.png)

内のすべてのレベル 2 ページの一覧を検索することができます、 [Windows 設定アプリを起動](https://msdn.microsoft.com/windows/uwp/launch-resume/launch-settings-app)トピック。 配置されているページに関連するすべてのリンクである必要がありますに重要です。

さらに、各ページでは、ページ上のコンテンツに関連する必要がありますに最大 5 つの検索語句を追加することはできます。 最良の検索結果には、特定のフレーズを使用します。 全般と 1 単語の用語を使用すると、関連する検索で表示されない、リンクする場合があります。  

たとえば、"Fabricam multipen"デバイスがあればなどの設定 fabricam mulitipen「ペン」などの一般的な検索用語ではなく、検索語句を作成します。

## <a name="characteristics-of-partner-settings-app"></a>パートナー [設定] アプリの特性

パートナーの設定アプリでは、次の特性があります。

* ユニバーサル Windows プラットフォーム (UWP) アプリ、または Windows Phone Silverlight アプリのいずれかがいます。

* ユーザーこれらをアンインストールできますを直接その他のアプリと同様です。

* その他の Windows アプリと同様、ストアの [設定] アプリを更新することで、アップグレードできます。

* これらは、最初の起動時にインストールされているアプリケーションがプレインストールされました。

    その他のプレインストールされているアプリケーションでとしてパートナーには、Windows デベロッパー センターへのシステム設定アプリケーションを送信する必要があります。
  * アプリケーションを認定します。
  * 署名済みの .appx ファイルとデバイスのイメージにアプリケーションを含めるために必要なライセンス ファイルを取得します。

* これらは、ユーザーが参照するか、検索を使用して見つけることはできませんが、ストア内の非表示の場所に発行されます。

## <a name="creating-system-settings-applications"></a>システムの設定アプリケーションを作成します。

> [!NOTE]
> 設定アプリケーションでは、ユニバーサル Windows プラットフォーム アプリし、すべての UWP プログラミング ガイドラインに従う必要があります。 参照してください[ユニバーサル Windows プラットフォーム (UWP) アプリのガイドライン](https://msdn.microsoft.com/library/windows/apps/hh465424.aspx)詳細についてはします。

1. Windows ユニバーサル アプリを作成するのにには、Windows ソフトウェア開発キット (SDK) を使用します。 Windows ユニバーサル アプリを作成する方法の詳細については、次を参照してください。 [Visual Studio でのビルドの UWP アプリ](https://msdn.microsoft.com/library/windows/apps/xaml/dn609832.aspx)します。

    Windows Phone を対象とする設定アプリを作成する場合は、Windows Phone Silverlight アプリも作成できます。

2. 以下のアプリケーション マニフェストの場合。

    `xmlns:rescap=http://schemas.microsoft.com/appx/manifest/foundation/windows10/restrictedcapabilities`
  
    ページの説明を使用して、アプリケーションのリンクがリスト表示、`SettingsPageUri`属性。 使用して、`AppActivationMode`属性をこのリンクをポイントします。 例としては、次のコード サンプルを使用します。

    ```xml
    <Extensions>
      <rescap:Extension Category="windows.settingsApp">
        <rescap:SettingsApp SettingsPageUri="ms-settings:yourl2pageuri">
          <rescap:AppLinks>
            <rescap:Link AppActivationMode ="uri://yourapp#deeplink" DisplayName="Link 1 Title" />
            <rescap:Link AppActivationMode ="uri://yourapp#deeplink" DisplayName="Link 2 Title" />
          </rescap:AppLinks>
            <rescap:SearchTerms>
            <rescap:Term>setup foo</rescap:Term>
            <rescap:Term>disable foo</rescap:Term>
            </rescap:SearchTerms>
          </rescap:SettingsApp>
        </rescap:Extension>
    </Extensions>
    ```

   このパッケージが、エントリをすべてのアプリの一覧ではできないことに注意してください。 これを行うには、設定、 [AppListEntry](https://docs.microsoft.com/uwp/api/windows.applicationmodel.core.applistentry)プロパティを**none**します。

    ```xml
     <uap:VisualElements AppListEntry="none" DisplayName="OptionalPackage"
       ....
     </uap:VisualElements>
    ```

3. プレインストールされているアプリケーションとして構成するには、設定アプリケーションを Windows デベロッパー センターを送信します。 署名済みの .appx ファイルを受信すると、ライセンス ファイルを入手するには、デバイスのイメージで、アプリケーションが含まれます。

## <a name="updating-system-settings-applications"></a>システム設定のアプリケーションの更新

Microsoft Store にアプリケーションの更新プログラムの設定を送信します。 更新プログラムが送信された後、インストール、設定アプリをお持ちのお客様は、更新プログラムに通知し、ストアで更新プログラムをインストールすることができます。

システム設定アプリは、デバイス アプリケーションの一覧に表示されません。 混乱を避けるためには、ユーザーがアプリの更新プログラムの通知されたときに、そのストアの説明に表示されるシステム レベルの設定が用意されていることを指定することを確認します**設定**デバイス。

## <a name="what-happens-to-legacy-control-panel-or-system-settings-apps-when-the-os-upgrades-to-windows-10"></a>OS は Windows 10 にアップグレードしたときのコントロール パネルまたはシステムの設定のレガシ アプリを動作します。

コントロール パネル アプリケーションは、Windows 7、Windows 8、または Windows 8.1 用に記述されたは引き続き動作し、(まで、削除、将来のリリースで)、従来のコントロール パネルに表示されますが、Windows 10 システム設定アプリでは表示されません。、し、その機能のいずれかをサポートします。

同様に、従来のシステム設定アプリは、Windows 8 または Windows 8.1 用に記述された、そのを継続するが、Windows 10 システム設定 アプリの機能にはサポートされていません。
