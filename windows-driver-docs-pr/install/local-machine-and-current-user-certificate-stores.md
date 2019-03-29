---
title: ローカル コンピューターと現在のユーザーの証明書ストア
description: ローカル コンピューターと現在のユーザーの証明書ストア
ms.assetid: b7362f2e-c8ff-42e4-9edc-df4b9967df29
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d36a1347d7728dd19230cfd3d5d2fd5a18379006
ms.sourcegitcommit: 23dc00b066687b068836d617e3355d7970301c7c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/14/2019
ms.locfileid: "56582945"
---
# <a name="local-machine-and-current-user-certificate-stores"></a>ローカル コンピューターと現在のユーザーの証明書ストア


各システムの証明書ストアは、次の種類があります。

* ローカル コンピューターの証明書ストア

    この種類の証明書ストアは、コンピューターのローカルには、コンピューター上のすべてのユーザーにグローバルです。 この証明書ストアは、レジストリの HKEY_LOCAL_MACHINE のルートにあります。

* 現在のユーザー証明書ストア

    この種類の証明書ストアでは、コンピューターのユーザー アカウントにローカルです。 この証明書ストアは、レジストリの HKEY_CURRENT_USER のルートにあります。

証明書ストアの場所を特定のレジストリを参照してください。[システム ストアの場所](https://docs.microsoft.com/windows/desktop/seccrypto/system-store-locations)します。

注意してくださいを現在のすべてのユーザー証明書ストア*を除き、現在のユーザー/個人用ストア*ローカル コンピューターの証明書ストアの内容を継承します。 たとえば、証明書がローカル コンピューターに追加された場合[信頼されたルート証明機関証明書ストア](trusted-root-certification-authorities-certificate-store.md)、(上記の注意点があります) にも信頼されたルート証明機関の証明書を格納する現在のすべてのユーザー証明書が含まれてください。

>[!NOTE]
>ドライバーのプラグ アンド プレイ (PnP) のインストール時に検証の署名には、そのルートが必要ですし、Authenticode 証明書を含む[テスト証明書](test-certificates.md)、ローカル コンピューターの証明書ストア内にあります。

 

追加またはシステムの証明書ストアから証明書を削除する方法の詳細については、次を参照してください。 [ **CertMgr**](https://msdn.microsoft.com/library/windows/hardware/ff543411)します。

 

 





