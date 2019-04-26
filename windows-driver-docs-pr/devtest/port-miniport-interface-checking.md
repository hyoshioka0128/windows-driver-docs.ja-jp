---
title: ポート/ミニポート インターフェイスのチェック
description: ポート/ミニポート インターフェイスのチェック
ms.assetid: ad6c4762-354d-446d-bcda-a2e99c37c589
keywords:
- ポート/ミニポート インターフェイスのチェック
ms.date: 09/14/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f71ea841e0304bb0c9924b99098a4307b789f61
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338704"
---
# <a name="portminiport-interface-checking"></a>ポート/ミニポート インターフェイス チェック

ポート/ミニポート インターフェイスのチェックには、Driver Verifier PortCls.sys やオーディオのミニポート ドライバーは、ks.sys AVStream ミニポート ドライバーとの間の DDI インターフェイスの検査を有効になります。 参照してください[AVStream ドライバー ルール](https://docs.microsoft.com/windows-hardware/drivers/devtest/rules-for-avstream-drivers)と[オーディオ ドライバーの規則](https://docs.microsoft.com/windows-hardware/drivers/devtest/rules-for-audio-drivers)

### <a name="activating-this-option"></a>このオプションをアクティブ化。

ドライバー検証マネージャーまたは Verifier.exe コマンドラインを使用して 1 つまたは複数のドライバーを確認するポート/ミニポート インターフェイスを有効にすることができます。 詳細については、次を参照してください。 [driver verifier のオプションを選択する](https://docs.microsoft.com/windows-hardware/drivers/devtest/selecting-driver-verifier-options)します。 オプションをオンにするポート/ミニポート インターフェイスをアクティブ化またはコンピューターを再起動する必要があります。

* **コマンドラインで**

    、コマンドラインでポート ミニポート インターフェイスのチェックで表される**0x0 x 00010000 (ビット 16)** します。 次に、例を示します。
    
    `verifier /flags 0x00010000 /driver MyDriver.sys`

    この機能は、[次へ] の起動後にアクティブになります。

* **ドライバー検証マネージャーを使用します。**

1. ドライバー検証マネージャーを起動します。 コマンド プロンプト ウィンドウで、検証方法を入力します。
2. (コードの開発者) の作成のカスタム設定を選択し、[次へ] をクリックします。
3. Select(check) ポート ミニポート インターフェイスをチェックします。
4. コンピューターを再起動します。
