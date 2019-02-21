---
title: デバイス メタデータ パッケージを手動で追加します。
description: デバイス メタデータ パッケージを手動で追加します。
ms.assetid: 1d0cee1f-8aa7-4fa9-b3c7-797cd09a07f4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c2556262ee39e07c50793870d8b12e526a7a7325
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535500"
---
# <a name="manually-adding-device-metadata-packages"></a>デバイス メタデータ パッケージを手動で追加します。


デバイス メタデータ パッケージは、次の方法でコンピューターにインストールできます。

-   OEM は、Windows 7 OEM プレインストール キット (OPK) を使用して、オペレーティング システムのオフライン イメージを更新できます。 OEM、OPK を使用すると、デバイス メタデータ パッケージに、イメージのコピー[デバイス メタデータ ストア](device-metadata-store.md)します。

-   開発者は、デバイス メタデータ パッケージをコピーできます、[デバイス メタデータ ストア](device-metadata-store.md)テストおよびデバッグ、パッケージがインストールされます。 詳細については、次を参照してください。[デバイス メタデータ パッケージのデバッグ](debugging-device-metadata-packages.md)します。

    **注**  はお勧めしませんそのエンドユーザー コピー デバイス メタデータ パッケージをデバイスのメタデータ ストアにします。 代わりに、エンドユーザーは、Windows メタデータとインターネット サービス (WMIS) または OEM によって提供されるインストール アプリケーションを使用してデバイス メタデータ パッケージをインストールする必要があります。

     

次のパスの場所を示しています、[デバイス メタデータ ストア](device-metadata-store.md):

```cpp
%PROGRAMDATA%\Microsoft\Windows\DeviceMetadataStore
```

デバイスのメタデータをコピーするパッケージを[デバイス メタデータ ストア](device-metadata-store.md)、次の手順を完了します。

1.  デバイス メタデータ パッケージのロケールのデバイスのメタデータ ストアのサブディレクトリが存在しない場合は、ターゲット ロケールの名前を使用して、サブディレクトリを作成する必要があります。

    たとえば、パッケージのロケールが EN-US の場合は、作成する必要が最初に、次のディレクトリが現在存在しない場合。

    ```cpp
    %PROGRAMDATA%\Microsoft\Windows\DeviceMetadataStore\EN-US
    ```

2.  デバイス メタデータ パッケージのコピーを適切な*&lt;ロケール&gt;* のサブディレクトリ、[デバイス メタデータ ストア](device-metadata-store.md)します。

デバイス後メタデータ パッケージがインストールされている、[デバイス メタデータ ストア](device-metadata-store.md)、[デバイス メタデータの取得クライアント](device-metadata-retrieval-client.md)(DMRC) は、デバイス メタデータ パッケージにアクセスし、デバイス情報を表示しますデバイスとプリンターのユーザー インターフェイス。

 

 





