---
title: リモート ファイル システムのコンポーネント
description: リモート ファイル システムのコンポーネント
ms.assetid: b2cd153a-5bcc-4670-8542-afa55e14727a
keywords:
- ネットワークリダイレクター WDK、リモートファイルシステム
- リダイレクタードライバー WDK、リモートファイルシステム
- リモートファイルシステム WDK
- ファイルシステムドライバー WDK、リモートファイルシステム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3850c759684eb2ff680659e703c5ad2312fe907d
ms.sourcegitcommit: 8c898615009705db7633649a51bef27a25d72b26
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/07/2020
ms.locfileid: "78910434"
---
# <a name="components-of-a-remote-file-system"></a>リモート ファイル システムのコンポーネント


## <span id="ddk_components_of_a_remote_file_system_if"></span><span id="DDK_COMPONENTS_OF_A_REMOTE_FILE_SYSTEM_IF"></span>


リモートファイルシステムを実装するには、次の基本的な要素が必要です。

-   クライアントにインストールされているネットワークリダイレクターソフトウェア。

-   通信に使用される、適切に定義されたトランスポートプロトコル。

-   サーバーにインストールされているファイルサーバーソフトウェア。

たとえば、Microsoft ネットワークリモートファイルシステムは次のように実装されます。

-   Microsoft ネットワーク用クライアントソフトウェアには、クライアントネットワークリダイレクターコンポーネントが用意されています。

-   Common Internet File System (CIFS) は、サーバーメッセージブロック (SMB) プロトコルとも呼ばれ、通信に使用されるネットワークトランスポートプロトコルを定義します。

-   LAN Manager サーバー (SMB サーバーとも呼ばれます) は、ファイルサーバーサービスを提供します。

クライアントにインストールされるネットワークリダイレクターソフトウェアは、ユーザーモードで動作し、カーネルモードで動作するいくつかのソフトウェアコンポーネントで構成されています。

