---
title: ネットワーク INF ファイル内のレジストリの追加セクション
description: ネットワーク INF ファイル内のレジストリの追加セクション
ms.assetid: 43c39389-5d01-49e9-a792-e853136068b4
keywords:
- INF ファイル WDK ネットワークの追加レジストリ セクション
- ネットワーク INF ファイル WDK、追加レジストリ セクション
- WDK ネットワークの追加レジストリ セクション
- 追加レジストリ セクションについての追加レジストリ セクション WDK ネットワーク
- キー WDK ネットワーク INF ファイル
- Ndi キー WDK ネットワーク
- WDK の値はネットワーク INF ファイル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce91eca10d49e0b3dfdcd8a3f87f2eadb2825387
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573673"
---
# <a name="add-registry-sections-in-a-network-inf-file"></a>ネットワーク INF ファイル内のレジストリの追加セクション





INF ファイルを含む 1 つまたは複数*追加レジストリ セクション*コンポーネントごとがインストールされます。 *追加レジストリ セクション*キーと値をレジストリに追加します。 **DDInstall** INF ファイルのセクションが含まれています、 **AddReg** 1 つまたは複数の参照ディレクティブ*追加レジストリ セクション*します。 詳細については、*追加レジストリ セクション*と**AddReg**ディレクティブを参照してください[ **INF AddReg ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546320)します。

### <a name="adding-keys-and-values-to-instance-keys"></a>インスタンス キーにキーと値を追加します。

1 つまたは複数*追加レジストリ セクション*キーと値を次のいずれかを実行するコンポーネントのインスタンス キーに追加できます。

-   ユーザー インターフェイスを通じて変更できない構成パラメーターは、コンポーネント--の静的パラメーターを設定します。 詳細については、次を参照してください。[静的パラメーターを設定](setting-static-parameters.md)します。

-   WAN アダプターのエンドポイント (チャネル、回線またはベアラー チャネルとも呼ばれます) の数を指定します。 詳細については、次を参照してください。 [WAN アダプター用の WAN のエンドポイントを指定する](specifying-wan-endpoints-for-a-wan-adapter.md)します。

-   キーおよび ISDN アダプターの値を指定します。 詳細については、次を参照してください。 [ISDN キーを指定すると、ISDN アダプターの値](specifying-isdn-keys-and-values-for-an-isdn-adapter.md)します。

-   別のネットワーク コンポーネントのインストールが必要です。 詳細については、次を参照してください。[インストールのもう 1 つのネットワーク コンポーネントを必要とする](requiring-the-installation-of-another-network-component.md)します。

-   ネットワーク アダプターのカスタム プロパティ シートをサポートする値を指定します。 詳細については、次を参照してください。[ネットワーク アダプターのカスタム プロパティ ページを指定する](specifying-custom-property-pages-for-network-adapters.md)します。

### <a name="adding-keys-and-values-to-a-netclient-component"></a>ネットワーク クライアント コンポーネントへのキーと値の追加

*追加レジストリ セクション*の INF ファイルで、 **NetClient**コンポーネントを追加する必要があります、 **NetworkProvider**キーを*サービス*をキーコンポーネント。 **NetworkProvider**キーが 2 つの値:**名前**、ネットワーク プロバイダーの名前を指定して、 **ProviderPath**ネットワークへの完全パスを指定します。プロバイダー DLL です。 詳細については、次を参照してください。 [NetClient コンポーネントのプロバイダーのパスと名前を指定する](specifying-the-name-and-provider-path-for-a-netclient-component.md)します。

**注**  **NetClient**コンポーネントは Windows 8.1、Windows Server 2012 R2 で非推奨以降。

 

### <a href="" id="ddk-creating-the-ndi-key-ng"></a>Ndi キーを作成します。

各ネットワーク INF ファイルには、少なくとも 1 つ含める必要があります*追加レジストリ セクション*を追加する、 **Ndi**ファイルによってインストールされているコンポーネントのキー。 **Ndi**キーは、コンポーネントのインスタンス キーに追加される特定のネットワークのキー。 キーと値に追加されますが、 **Ndi**キーは、インストールされているネットワーク コンポーネントとその機能の種類によって異なります。 **Ndi**キーは、次を指定します。

-   **HelpText**の値を**NetTrans**、 **NetClient**、または**NetService**コンポーネント。 詳細については、次を参照してください。 [HelpText 値を追加する](adding-a-helptext-value.md)します。

-   通知オブジェクトの値。 詳細については、次を参照してください。[通知オブジェクトのレジストリ値を追加する](adding-registry-values-for-a-notify-object.md)します。

-   サービスに関連する値。 詳細については、次を参照してください。 [Ndi キーに値を Adding Service-Related](adding-service-related-values-to-the-ndi-key.md)します。

-   バインド インターフェイス。 詳細については、次を参照してください。[バインド インターフェイスを指定する](specifying-binding-interfaces.md)します。

-   アダプターの構成パラメーターを**詳細**ページ。 詳細については、次を参照してください。[プロパティの詳細設定 ページの構成パラメーターを指定する](specifying-configuration-parameters-for-the-advanced-properties-page.md)します。

-   バンドルのメンバーシップ。 詳細については、次を参照してください。[バンドルのメンバーシップを指定する](specifying-bundle-membership.md)します。

一覧については**Ndi**レジストリ キーと Windows 95/98/Me で使用できますが、Windows 2000 以降のバージョンでは使用されない値を参照してください。 [Ndi 値とキーが Windows 2000 以降のバージョンで使用されません](ndi-values-and-keys-not-used-in-windows-2000-and-later-versions.md)します。

 

 





