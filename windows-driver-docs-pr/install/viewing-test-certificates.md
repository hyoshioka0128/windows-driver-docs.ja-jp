---
title: テスト証明書の参照
description: テスト証明書の参照
ms.assetid: bdfa8970-fdba-4d65-8a9c-960e5f6844d6
keywords:
- ドライバー WDK の署名、テスト証明書の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b0e6dbfefe8d6188f0714848fbfd41f304531ff
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339328"
---
# <a name="viewing-test-certificates"></a>テスト証明書の参照


証明書が作成され、コピーは、証明書ストアに、Microsoft 管理コンソール (MMC) の証明書スナップインで使用できますそれを表示します。 MMC で証明書を表示するには、次の操作を行います**証明書**スナップイン。

1.  クリックして**開始**し、[検索の開始] をクリックします。

2.  証明書スナップインを開始する入力 Certmgr.msc とキーを押して、 **Enter**キー。

3.  証明書スナップインの左側のウィンドウで、PrivateCertStore 証明書ストアのフォルダーを展開し、証明書をダブルクリックします。

次のスクリーン ショットの証明書スナップインでビューを示しています、 **PrivateCertStore**証明書ストアのフォルダー。

![テスト証明書を示す証明書ストアのスクリーン ショット ](images/certstore.png)

Contoso.com(Test) 証明書に関する詳細を表示するには、右側のウィンドウで、証明書をダブルクリックします。 次のスクリーン ショットでは、証明書に関する詳細を表示します。

![contoso.com の詳細を表示する証明書 ウィンドウのスクリーン ショットは証明書を (テスト)](images/certinfo.png)

証明書のダイアログ ボックスを示すことに注意してください。"この CA ルート証明書は信頼されていません。 信頼を有効にするには、この証明書をインストール、信頼されたルート証明機関ストア内。" これは、想定される動作です。 Windows が既定では、"Contoso.com(Test)"証明機関を信頼しないために、証明書を検証できません。

 

 





