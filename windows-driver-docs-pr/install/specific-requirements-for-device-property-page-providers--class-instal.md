---
title: デバイスのプロパティ ページ プロバイダー (共同インストーラー) の要件
description: デバイスのプロパティ ページのプロバイダーの一般的な要件 (共同インストーラー)
ms.assetid: b57beaed-5e5f-499e-b973-532f33b7fb99
keywords:
- デバイスのプロパティ ページ DIF_ADDPROPERTYPAGE_ADVANCED WDK デバイスのインストール
- プロパティ ページ DIF_ADDPROPERTYPAGE_ADVANCED WDK デバイスのインストール
- カスタム プロパティ ページ DIF_ADDPROPERTYPAGE_ADVANCED WDK デバイスのインストール
- DIF_ADDPROPERTYPAGE_ADVANCED
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 969c786ab427c18ba75381f0fc56e2b6014211d0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385892"
---
# <a name="specific-requirements-for-device-property-page-providers-co-installers"></a>デバイスのプロパティ ページのプロバイダーの一般的な要件 (共同インストーラー)





A[共同インストーラー](writing-a-co-installer.md)提供する 1 つまたは複数のカスタム デバイス プロパティ ページを処理する必要があります、 [ **DIF_ADDPROPERTYPAGE_ADVANCED** ](https://docs.microsoft.com/windows-hardware/drivers/install/dif-addpropertypage-advanced)デバイス インストール機能 (差分) コード。 デバイス マネージャーは、ユーザーがクリックしたときにこの要求を発行、**プロパティ**デバイスでデバイス マネージャーまたはコントロール パネルのタブ。

この要求に応答して、インストーラーはについて各カスタム プロパティ ページの情報を提供します、ページの作成し、デバイスの動的プロパティ ページの一覧に、作成したページを追加します。 インストーラーではこれを初期化し、要求のクラスのインストール パラメーターの SP_ADDPROPERTYPAGE_DATA 構造体を返すことで。

デバイス マネージャーに送信、ユーザーは、任意のプロパティを変更する場合、 [ **DIF_PROPERTYCHANGE** ](https://docs.microsoft.com/windows-hardware/drivers/install/dif-propertychange)インストーラーをインストーラーが呼び出すことによって、新しいパラメーターを設定した後に差分コード[ **SetupDiSetDeviceInstallParams**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdeviceinstallparamsa)します。

詳細については、カスタムのデバイスのプロパティ ページを作成する方法についての[共同インストーラー](writing-a-co-installer.md)を参照してください[デバイスのプロパティ ページのプロバイダーの一般的な要件](general-requirements-for-device-property-page-providers.md)します。

 

 





