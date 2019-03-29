---
title: Ndi キーへのサービス関連値の追加
description: Ndi キーへのサービス関連値の追加
ms.assetid: f967396c-6695-458c-a081-ef382ed7c9dd
keywords:
- 追加レジストリ セクション WDK ネットワー キング、Ndi 値とキー
- Nido キーと値の WDK ネットワーク
- Ndi キー WDK のネットワーク接続サービスに関連する値
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7badf1f4c35cbcc4349bf267529a4c4f0d271e8d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582217"
---
# <a name="adding-service-related-values-to-the-ndi-key"></a>Ndi キーへのサービス関連値の追加





コンポーネントに関連付けられているサービス (デバイス ドライバー) がある場合、*追加レジストリ セクション*によって参照される、 *DDInstall*セクションは、そのコンポーネントを追加する必要があります、**サービス**値を Ndi キー。 **サービス**値は、REG\_SZ 値コンポーネントに関連付けられているプライマリ サービスを指定します。 **サービス**値に一致する必要があります、 *ServiceName*のパラメーター、 **AddService**を参照するディレクティブ、*サービス インストール セクション* 、プライマリ サービス用です。 詳細については、次を参照してください。 [INF DDInstall.Services セクション](ddinstall-services-section-in-a-network-inf-file.md)します。

コンポーネントの 1 つまたは複数の関連付けられているサービスである場合、*追加レジストリ セクション*によって参照される、 *DDInstall*セクションは、そのコンポーネントを追加する必要があります、 **CoServices**値です。**Ndi**キー。 **CoServices**値は、マルチ\_SZ 値で指定されたプライマリ サービスを含め、コンポーネントをインストールするすべてのサービスを指定する、**サービス**値。 **CoServices**値は、すべての必要な**NetTrans**、 **NetClient**、および**NetService**コンポーネント。

**注**  **NetClient**コンポーネントは Windows 8.1、Windows Server 2012 R2 で非推奨以降。

 

**注**  **Net** (アダプター) のコンポーネントはありません、 **CoServices**値に設定するため、1 つのサービスは、アダプターを関連付けることができます。

 

サービスをシャット ダウンを除くすべてのサービスに関連するアクションの実行、 **CoServices**記載されている順序で。 たとえば、サービスが記載されている順序で開始されます。 サービスは、ただし、逆の順序で停止します。 そのサービスが表示されている場合にのみ、サービスのコンポーネントのサービスに関連するアクションが実行される**CoServices**します。

 

 





