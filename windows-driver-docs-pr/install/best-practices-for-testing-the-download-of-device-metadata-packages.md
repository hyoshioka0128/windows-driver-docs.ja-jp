---
title: デバイス メタデータ パッケージのダウンロードをテストするためのベスト プラクティス
description: デバイス メタデータ パッケージのダウンロードをテストするためのベスト プラクティス
ms.assetid: 4470fa63-527a-4e92-916f-a84421259f57
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8ee2209dbfca24f119e5d566d7f084b2beccb1da
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557288"
---
# <a name="best-practices-for-testing-the-download-of-device-metadata-packages"></a>デバイス メタデータ パッケージのダウンロードをテストするためのベスト プラクティス


方法により、デバイス メタデータの取得のクライアント ([DMRC](device-metadata-retrieval-client.md)) デバイス メタデータ パッケージは Windows メタデータで使用可能な時刻とインターネット サービスの間キャッシュ メタデータ パッケージ、遅延が発生する可能性が ([WMIS](windows-metadata-and-internet-services.md)) サーバーと、DMRC がクライアント システムにメタデータ パッケージをダウンロードするときの時刻。 デバイス メタデータ パッケージのダウンロードをテストするには、次の方法のいずれかで、ダウンロードを強制することができます。

-   内のフォルダーを削除、[デバイス メタデータのキャッシュ](device-metadata-cache.md)します。 このキャッシュは、次のディレクトリに格納されます。

    Windows 7:

    ```cpp
    %LOCALAPPDATA%\Microsoft\Device Metadata\
    ```

    Windows 8 の場合:

    ```cpp
    %PROGRAMDATA%\Microsoft\Windows\DeviceMetadataCache\
    ```

    値をリセットするこれらのフォルダーを削除する**LastCheckedDate**強制的にすべてのデバイスの WMIS サーバーにクエリを DMRC とします。

-   設定、 **CheckBackMDRetrieved**と**CheckBackMDNotRetrieved**レジストリ キーを 0 にします。 これらの値が 0 の場合、DMRC はすぐにターゲット デバイスの WMIS サーバーを照会します。

    WMIS サーバーが、DMRC が WMIS から応答を受信するたびにについてこれらの値を上書きすることに注意します。 そのため、ターゲット デバイスの WMIS サーバーのクエリを実行する前に、DMRC が他の任意のデバイス用の応答を受信した場合、これらのパラメーターは変更できます。

    **注**  メタデータ パッケージをテストする場合にのみ、これらの変更を行う必要があります。 DMRC によって使用されるレジストリ値を変更する任意のツールを使用してエンドユーザーを提供する必要がありますされません。

     

 

 





