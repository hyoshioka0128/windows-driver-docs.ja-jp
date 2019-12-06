---
title: WMIS からのデバイス メタデータ パッケージのインストール
description: WMIS からのデバイス メタデータ パッケージのインストール
ms.assetid: e2466b8a-c9c7-4d0d-9ce7-4648c83fc272
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 487b27b642664b1e0adba7bd8cc3045c3d9cf430
ms.sourcegitcommit: ba3199328ea5d80119eafc399dc989e11e7ae1d6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "74862368"
---
# <a name="installing-device-metadata-packages-from-wmis"></a>WMIS からのデバイス メタデータ パッケージのインストール


オペレーティングシステムは、新しいデバイスを検出すると、 [Windows メタデータおよびインターネットサービス](windows-metadata-and-internet-services.md)(WMIS) と呼ばれるオンラインサービスに対して、デバイスのメタデータパッケージを照会します。 デバイスメタデータパッケージが使用可能な場合、ローカルコンピューター上で実行されるデバイスメタデータ取得クライアント (DMRC) は、WMIS からパッケージをダウンロードし、ローカルコンピューターにパッケージをインストールします。

**注**  現在のユーザーが、組み込みの guest アカウントなどの guest 特権のみを持つアカウントを使用してログインしている場合は、WMIS からデバイスメタデータパッケージがダウンロードされないことに注意してください。

 

[ドライバーパッケージ](driver-packages.md)を[ハードウェア認定キット (HCK)](https://go.microsoft.com/fwlink/p/?linkid=227016)に送信してデジタル署名する場合に、デバイスメタデータパッケージを[Windows Quality Online Services (winqual)](https://docs.microsoft.com/windows-hardware/drivers/dashboard/winqual-submission-tool--winqualexe-)に送信すると、Windows 7 以降のバージョンの windows を実行している任意のコンピューターで DMRC によって行われたダウンロード要求に対して、WMIS がパッケージを使用できるようになります。

**重要**  OEM は WMIS を使用してのみデバイスメタデータパッケージを配布することを強くお勧めします。 WMIS を使用したデバイスメタデータパッケージの配布では、*ハードウェア優先*のインストールシナリオがサポートされます。 このシナリオでは、デバイスのドライバーとデバイス固有のソフトウェアがインストールされる前に、新しいデバイスがインストールされます。 このシナリオの詳細については、「[ハードウェア優先インストール](hardware-first-installation.md)」を参照してください。

 

デバイスメタデータパッケージは、次の方法で WMIS を介してインストールされます。

1.  ユーザーがデバイスとプリンターのユーザーインターフェイスの [ギャラリー] ビューウィンドウを開くと、[デバイスメタデータ取得クライアント](device-metadata-retrieval-client.md)(DMRC) は、デバイスとプリンターのユーザーインターフェイスに表示されるデバイスのデバイスメタデータを取得しようとします。

    DMRC は、まず、ローカルコンピューターの[デバイスメタデータキャッシュ](device-metadata-cache.md)とデバイスメタデータ[ストア](device-metadata-store.md)でデバイスメタデータを検索します。 デバイスが新しくインストールされた場合、または定期的なメタデータ更新のためにデバイスがスケジュールされている場合、DMRC は、デバイスの利用可能なメタデータパッケージを WMIS に照会します。

2.  デバイスメタデータパッケージが使用可能な場合、DMRC は WMIS からパッケージを自動的にダウンロードし、パッケージのデバイスメタデータコンポーネントを抽出して、[デバイスメタデータキャッシュ](device-metadata-cache.md)内に保存します。

 

 





