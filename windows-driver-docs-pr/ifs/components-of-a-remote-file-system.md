---
title: リモート ファイル システムのコンポーネント
description: リモート ファイル システムのコンポーネント
ms.assetid: b2cd153a-5bcc-4670-8542-afa55e14727a
keywords:
- WDK、リモート ファイル システム リダイレクターをネットワークします。
- リダイレクター ドライバー WDK、リモート ファイル システム
- WDK のリモート ファイル システム
- ファイル システム ドライバー WDK、リモート ファイル システム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a25f729727580b04a5f25d16fe625449b62d1d0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351472"
---
# <a name="components-of-a-remote-file-system"></a>リモート ファイル システムのコンポーネント


## <span id="ddk_components_of_a_remote_file_system_if"></span><span id="DDK_COMPONENTS_OF_A_REMOTE_FILE_SYSTEM_IF"></span>


リモート ファイル システムを実装するためには、次の基本的な要素が必要です。

-   ネットワーク リダイレクター ソフトウェアがクライアントにインストールします。

-   通信に使用する適切に定義されたトランスポート プロトコル。

-   ファイル サーバーのソフトウェアがサーバーにインストールします。

たとえば、Microsoft ネットワークのリモート ファイル システムとしては、次のように実装されます。

-   Microsoft ネットワーク ソフトウェア用のクライアントは、ネットワーク リダイレクター コンポーネントをクライアントに提供します。

-   共通インターネット ファイル システム (CIFS)、サーバー メッセージ ブロック (SMB) プロトコルとも呼ばれますが、これは、通信に使用されるネットワーク トランスポート プロトコルを定義します。

-   (SMB サーバーとも呼ばれます)、LAN Manager サーバーは、ファイル サーバーのサービスを提供します。

クライアントにインストールされているネットワーク リダイレクター ソフトウェアは、ユーザー モードで動作するものもありますし、カーネル モードで動作するいくつかは、複数のソフトウェア コンポーネントで構成されます。

次のセクションでは、Windows Server 2003、Windows XP、および Windows 2000 上のリモート ファイル システムの開発者にとって重要な概念について説明します。 次のトピックについて説明します。

[ネットワーク リダイレクターの概要](introduction-to-network-redirectors.md)

[カーネル ネットワーク リダイレクター ドライバー コンポーネント](kernel-network-redirector-driver-components.md)

 

 




