---
title: WMIS からのデバイス メタデータ パッケージのインストール
description: WMIS からのデバイス メタデータ パッケージのインストール
ms.assetid: e2466b8a-c9c7-4d0d-9ce7-4648c83fc272
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4bb0f72b149433dfa980fa4d0135dae4e09b28d1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570721"
---
# <a name="installing-device-metadata-packages-from-wmis"></a>WMIS からのデバイス メタデータ パッケージのインストール


呼ばれるオンライン サービスに照会し、オペレーティング システムが新しいデバイスを検出、 [Windows メタデータとインターネット サービス](windows-metadata-and-internet-services.md)(WMIS) ためのデバイス メタデータ パッケージ。 デバイス メタデータ パッケージを使用できる場合、デバイス メタデータの取得クライアント (DMRC)、ローカル コンピューターで実行されているは WMIS からパッケージをダウンロードし、ローカル コンピューターにパッケージをインストールします。

**注**  WMIS からは、現在のユーザーが組み込みのゲスト アカウントなどのゲスト特権のみを任意のアカウントを使用してログインしている場合デバイス メタデータ パッケージはダウンロードされません。

 

デバイス メタデータ パッケージを提出する場合は[Windows Quality Online Services (Winqual)](https://go.microsoft.com/fwlink/p/?linkid=62651)送信するとき、[ドライバー パッケージ](driver-packages.md)を[ハードウェア認定キット (HCK)](https://go.microsoft.com/fwlink/p/?linkid=227016)では、デジタル署名、パッケージは Windows 7 および Windows の以降のバージョンを実行しているコンピューターで DMRC によって行われるダウンロード要求の使用可能 WMIS になります。

**重要な**  Oem が WMIS を介してのみ、デバイス メタデータ パッケージを配布することを強くお勧めします。 デバイス メタデータの配布パッケージの WMIS サポートを通じて、*ハードウェア最初*インストール シナリオです。 このシナリオで、ドライバーの前に、新しいデバイスがインストールされているし、デバイスのデバイスに固有のソフトウェアがインストールされています。 このシナリオの詳細については、[ハードウェア最初インストール](hardware-first-installation.md)を参照してください。

 

デバイス メタデータ パッケージは、次のように WMIS を通じてインストールされます。

1.  ユーザーがデバイスとプリンターのユーザー インターフェイスのギャラリー ビュー ウィンドウを開いたときに、[デバイス メタデータの取得のクライアント](device-metadata-retrieval-client.md)(DMRC) は、デバイスのデバイス メタデータを取得しようとしているデバイスとプリンターのユーザー インターフェイス表示されます。

    DMRC はまず、ローカル コンピューターの[デバイス メタデータのキャッシュ](device-metadata-cache.md)と[デバイス メタデータ ストア](device-metadata-store.md)デバイス メタデータ。 デバイスが新しくインストールした場合、またはデバイスが、定期的なメタデータの更新のスケジュールされている場合は、DMRC は、デバイスの使用可能なメタデータ パッケージの WMIS を照会します。

2.  デバイス メタデータ パッケージを使用できる場合 DMRC 自動的に WMIS からダウンロードしたパッケージ、パッケージのデバイスのメタデータ コンポーネントを抽出および内でそれらを保存、[デバイス メタデータのキャッシュ](device-metadata-cache.md)します。

 

 





