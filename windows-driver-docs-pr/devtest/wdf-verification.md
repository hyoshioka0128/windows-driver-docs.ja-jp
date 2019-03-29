---
title: WDF 検証
description: Driver Verifier の WDF の検証
ms.assetid: 9ee72369-878f-4710-a38b-1c93042178bd
keywords:
- Driver Verifier の WDF の検証
ms.date: 09/14/2018
ms.localizationpriority: medium
ms.openlocfilehash: 50c300f799b477fc353b70c5ea693bfbeeeb549f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572499"
---
# <a name="wdf-verification"></a>WDF の検証

WDF の検証チェックはカーネル モード ドライバーは、次のかどうか、[カーネル モード ドライバー フレームワーク (KMDF) 要件](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-the-framework-to-develop-a-driver)適切です。  

チェックと、この検証問題のある[チェック 0x10D のバグします。WDF_VIOLATION](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0x10d---wdf-violation)します。 


### <a name="activating-this-option"></a>このオプションをアクティブ化。

ドライバー検証マネージャーまたは Verifier.exe コマンドラインを使用して 1 つまたは複数のドライバーを確認するポート/ミニポート インターフェイスを有効にすることができます。 詳細については、次を参照してください。 [driver verifier のオプションを選択する](https://docs.microsoft.com/windows-hardware/drivers/devtest/selecting-driver-verifier-options)します。 オプションをオンにするポート/ミニポート インターフェイスをアクティブ化またはコンピューターを再起動する必要があります。

* **コマンドラインで**

    、コマンドラインでポート ミニポート インターフェイスのチェックで表される**0x00100000**します。 例:
    
    `verifier /flags 0x00100000 /driver MyDriver.sys`

    この機能は、[次へ] の起動後にアクティブになります。

* **ドライバー検証マネージャーを使用します。**

1. ドライバー検証マネージャーを起動します。 コマンド プロンプト ウィンドウで、検証方法を入力します。
2. (コードの開発者) の作成のカスタム設定を選択し、[次へ] をクリックします。
3. Select(check) ポート ミニポート インターフェイスをチェックします。
4. コンピューターを再起動します。
