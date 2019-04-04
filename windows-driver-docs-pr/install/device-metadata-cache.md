---
title: デバイス メタデータのキャッシュ
description: デバイス メタデータのキャッシュ
ms.assetid: 0b20e1e0-9137-4572-8a5b-6bde63c34ce4
keywords:
- デバイスのメタデータ キャッシュ WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 25d7d9324654be1033323127a6ba145bb9ca4c12
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527555"
---
# <a name="device-metadata-cache"></a>デバイス メタデータのキャッシュ


デバイス メタデータのキャッシュは、ローカル コンピューターのデバイス メタデータ パッケージが保存されるディレクトリです。

Windows 7 では、デバイス メタデータのキャッシュは、次のディレクトリからアクセスします。

```cpp
%LOCALAPPDATA%\Local\Microsoft\Device Metadata\
```

Windows 8 以降、デバイス メタデータのキャッシュは、次のディレクトリからへのアクセスします。

```cpp
%PROGRAMDATA%\Microsoft\Windows\DeviceMetadataCache\
```

ときに、[デバイス メタデータの取得クライアント](device-metadata-retrieval-client.md)(DMRC)、Windows メタデータ and Services (WMIS) web サイトからデバイス メタデータ パッケージをダウンロードして、デバイスのメタデータ キャッシュ内に保存します。 このプロセスの詳細については、[WMIS からデバイス メタデータ パッケージをインストールする](installing-device-metadata-packages-from-wmis.md)を参照してください。

**注**  デバイス メタデータのキャッシュは使用するオペレーティング システムのみに予約されています。 インストールされていない DMRC などは、OEM によって提供されるアプリケーションを通じてデバイス メタデータ パッケージをコピーする必要があります、[デバイス メタデータ ストア](device-metadata-store.md)代わりにします。

 

 

 





