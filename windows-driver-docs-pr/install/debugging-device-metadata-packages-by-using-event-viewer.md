---
title: イベント ビューアーを使用したデバイス メタデータ パッケージのデバッグ
description: イベント ビューアーを使用したデバイス メタデータ パッケージのデバッグ
ms.assetid: 168a9dd1-aab2-4497-a59d-b8fe52d8cde2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 10a6ba2d48a0d191822a799c9bb33e8f2308af01
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352076"
---
# <a name="debugging-device-metadata-packages-by-using-event-viewer"></a>イベント ビューアーを使用したデバイス メタデータ パッケージのデバッグ


Windows 7 以降では、Event Tracing for Windows (ETW) サービスは、デバイス メタデータ パッケージの処理に関連するイベントの DeviceMetadata/デバッグ チャネルをサポートします。

DeviceMetadata/デバッグ チャネルには、エラーと、ダウンロードまたはデバイス メタデータ パッケージの処理中に発生するイベントの情報が格納されます。 このチャネルもメタデータ パッケージ内で検出とデバイスのクエリに関する追加のステータスを提供するイベントを警告と情報を格納、[デバイス メタデータ ストア](device-metadata-store.md)します。

### <a name="viewing-device-metadatadebug-etw-events-through-event-viewer"></a>イベント ビューアーからデバイス メタデータ/デバッグ ETW イベントの表示

デバイス メタデータ パッケージのイベント ビューアーをログに記録されるイベントの表示を使用します。 これらのイベントを表示するイベント ビューアーで DeviceMetadata/デバッグ ETW チャネルを開いて次の手順に従います。

1.  **開始** メニューを右クリックして**コンピューター**、順にクリックします**管理**します。

2.  展開、**システム ツール**ノード。

3.  展開し、をクリックし、**イベント ビューアー**ノード。

4.  **[表示]** メニューで、**[分析およびデバッグ ログの表示]** をクリックします。

5.  展開、 **Applications and Services Logs**ノード。

6.  展開、 **Microsoft**ノード。

7.  展開、 **Windows**ノード。

8.  展開、 **UserPnP**ノード。

9.  をクリックして、 **DeviceMetadata/デバッグ**ノード。

    **注**  DeviceMetadata/デバッグ ETW チャネルを受信し、イベントの表示でログ記録を有効にする必要がありますまずします。 これを行うを右クリックし、 **DeviceMetadata/デバッグ**ノード**プロパティ**します。 をクリックし、**ログの有効化**します。

     

### <a name="device-metadatadebug-etw-events"></a>デバイス メタデータ/デバッグの ETW イベント

オペレーティング システムは、次のエラー、警告、および情報イベントをダウンロードまたはデバイス メタデータ パッケージの処理中に記録されます。

<a href="" id="event-id--7900-error--device-metadata-package-error"></a>イベント ID:7900 エラー:デバイス メタデータ パッケージのエラー  
デバイス メタデータ パッケージのコンポーネントの 1 つでエラーが検出されました。

このイベント ログ メッセージには、次の情報が含まれています。

-   エラーの原因の説明が、エラーの説明です。 エラーの発生元は、[デバイス メタデータ ストア](device-metadata-store.md)または[デバイス メタデータのキャッシュ](device-metadata-cache.md)します。

-   デバイス メタデータ パッケージの名前。

-   アプリケーション固有のエラー コード。 これらのエラー コードの詳細については、次を参照してください。[デバイス メタデータのエラー コード](device-metadata-error-codes.md)します。

-   Win32 エラー コード。

<a href="" id="event-id--7901-information--device-metadata-package-downloaded-from-wmis-"></a>イベント ID:7901 情報:デバイス メタデータ パッケージは、WMIS からダウンロードします。  
デバイス メタデータ パッケージからダウンロードされた、 [Windows メタデータとインターネット サービス](windows-metadata-and-internet-services.md)(WMIS) によって、[デバイス メタデータの取得クライアント](device-metadata-retrieval-client.md)(DMRC) パッケージからコンポーネントを抽出して内でそれらを保存、[デバイス メタデータのキャッシュ](device-metadata-cache.md)します。

このイベント ログ メッセージには、次の情報が含まれています。

-   イベントの説明。

-   内で展開したデバイス メタデータ パッケージの場所、[デバイス メタデータのキャッシュ](device-metadata-cache.md)します。

-   デバイス メタデータ パッケージの名前。

<a href="" id="event-id--7902-error--device-metadata-package-not-signed--"></a>イベント ID:7902 エラー:デバイス メタデータ パッケージは署名されていません。   
によって、インストール済みのデバイス メタデータ パッケージが署名されていない、 [Windows Quality Online Services (Winqual)](https://go.microsoft.com/fwlink/p/?linkid=62651)します。

**注**  WMIS からダウンロードされるときにのみ、デバイス メタデータ パッケージの署名を検証します。

 

このイベント ログ メッセージには、次の情報が含まれています。

-   エラーの説明。

-   デバイス メタデータ パッケージの名前。

-   アプリケーション固有のエラー コード。 これらのエラー コードの詳細については、次を参照してください。[デバイス メタデータのエラー コード](device-metadata-error-codes.md)します。

-   Win32 エラー コード。

<a href="" id="event-id--7950-information--new-device-metadata-package-discovered-in-the-local-metadata-store-"></a>イベント ID:7950 情報:新しいデバイス メタデータ パッケージがローカルのメタデータ ストアで検出されました。  
DMRC はローカル コンピューターにインストールされている新しいデバイス メタデータ パッケージを検出しました。

このイベント ログ メッセージには、次の情報が含まれています。

-   イベントの説明。

-   次のいずれか、デバイス メタデータ パッケージのソース、[デバイス メタデータ ストア](device-metadata-store.md)または[デバイス メタデータのキャッシュ](device-metadata-cache.md)します。

-   デバイス メタデータ パッケージの名前。

<a href="" id="event-id--7951-information--query-for-metadata-packages-in-progress-"></a>イベント ID:7951 情報:進行中のメタデータ パッケージを照会します。  
DMRC クエリでは、特定のデバイスのデバイス メタデータ パッケージをインストールします。

このイベント ログ メッセージには、次の情報が含まれています。

-   イベントの説明。

-   デバイスのハードウェア ID などのモデル ID、デバイスのルックアップ キー 詳細については、次を参照してください。 [ **HardwareID** ](https://msdn.microsoft.com/library/windows/hardware/ff546114)と[ **ModelID**](https://msdn.microsoft.com/library/windows/hardware/ff549295)します。

    **注**  ハードウェアの一覧をパラメーターとして Id が渡されるときに、特定のハードウェア ID のみが記録されます。

     

<a href="" id="event-id--7952-warning--network-related-errors-"></a>イベント ID:7952 警告:ネットワーク関連のエラー。  
DMRC では、パッケージ、WMIS からデバイス メタデータのダウンロード中にネットワーク エラーが発生しました。

**注**  ネットワークが利用できない場合、この警告は生成されません。

 

このイベント ログ メッセージには、次の情報が含まれています。

-   エラーの詳細な説明。

-   アプリケーション固有のエラー コード。 これらのエラー コードの詳細については、次を参照してください。[デバイス メタデータのエラー コード](device-metadata-error-codes.md)します。

-   ネットワーク エラーの時点で HTTP ステータス コード。

 

 





