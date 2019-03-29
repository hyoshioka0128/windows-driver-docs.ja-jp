---
title: ホットスポット認証サンプルを更新する
description: ホットスポット認証サンプルを更新する
ms.assetid: 68ebcdee-7b21-4177-b032-ba725ad2aee4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e9e74240085dcd4e327499732cdd3a0f129f5bc1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580178"
---
# <a name="update-the-hotspot-authentication-sample"></a>ホットスポット認証サンプルを更新する


[ホット スポット認証サンプル](https://go.microsoft.com/fwlink/p/?linkid=313215)プロジェクトは既定の通信事業者の ID とアプリケーションのファミリ名。 テスト環境でサンプルを使用するには、次のものを変更する必要があります。

-   **更新プログラム、通信事業者 ID**モバイル ブロード バンドのアプリを発行する場合、アプリとサービスのメタデータに関連付けられている ID エクスペリエンスがあります。 Wi Fi 専用オペレーターの場合は、会社の ID として使用する新しい GUID を生成します。

-   **SSID を更新**テストに使用する、SSID がプロビジョニング ファイルの SSID と一致する必要があり、接続するクライアントにする必要がありますプラン captive portal と WISPr チャレンジします。

-   **プロビジョニング ファイルの署名**Wi Fi 専用オペレーターの場合は、プロビジョニング ファイルに署名する必要があります。 Windows 8 SDK または Windows 8.1 の SDK、ツールを見つける**ProvisioningTestHelper.psd1**します。 次の 4 つの追加コマンドレットに追加の PowerShell セッションには、これをインポートします。

    -   **インストール TestEVCert**新しい CA 証明書を生成、EV SSL プロバイダーを信頼するには、テスト コンピューターに登録およびそれを生成および署名で使用するため、EV 証明書の署名に使用します。

    -   **ConvertTo SignedXml** (テストの生成またはサード パーティ プロバイダーによって発行された) が EV 証明書を使用してプロビジョニングのメタデータ XML ファイルに、XML DSig 署名を適用します。 信頼された証明書からこの署名は、モバイル ブロード バンド アプリ関連のハードウェアがないから有効なものとしてプロビジョニング ファイルを受け入れるように Windows をによりします。

    -   **テスト SignedXml**スキーマ準拠と有効な署名を確保するプロビジョニング ファイルを確認します。

    -   **インストール RootCertFromFile**テスト ルート証明書を開発用 PC 以外のコンピューター上のクライアント エクスペリエンスをテストする別の PC に適用されます。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[ホット スポットの認証アプリを概要します。](get-started-with-a-hotspot-authentication-app.md)

 

 






