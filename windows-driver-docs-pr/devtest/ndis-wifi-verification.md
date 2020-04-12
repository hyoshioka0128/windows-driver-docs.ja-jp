---
title: NDIS/WIFI 検証
description: NDIS/WIFI 検証オプションは、NDIS または WIFI ドライバーが Windows オペレーティングシステムのカーネルと正しく通信するかどうかを決定します。
ms.assetid: EB553449-9460-403D-8ED2-343048C4B38C
ms.date: 04/10/2020
ms.localizationpriority: medium
ms.openlocfilehash: b12907ab66033600c98bb34f1d55f711e3eeb28d
ms.sourcegitcommit: 84be9e06fd0886598df77dffcbc75632d613c8f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/11/2020
ms.locfileid: "81208133"
---
# <a name="ndiswifi-verification"></a>NDIS/WIFI 検証

NDIS/WIFI 検証オプションは、NDIS または WIFI ドライバーが Windows オペレーティングシステムのカーネルと正しく通信するかどうかを決定します。

**注**  このオプションは Windows 8.1 以降で使用できます。

NDIS/WIFI 検証オプションは、ドライバーがさまざまなコンテキストで Oid を正しく処理し、Microsoft が推奨するベストプラクティスに従っていることを確認するための規則を適用します。

このオプションがアクティブで、ドライバーの検証ツールが NDIS または WIFI の規則のいずれかに違反していることを検出した場合、ドライバーの検証ツールはバグチェック 0xC4 (パラメーター1は特定のコンプライアンス規則の識別子と同じ) を発行します。

検証規則の一覧には、次のものが含まれます。

[**NdisOidComplete**](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-ndisoidcomplete)

[**NdisOidDoubleComplete**](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-ndisoiddoublecomplete)

[**NdisOidDoubleRequest**](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-ndisoiddoublerequest)

[**NdisTimedDataHang**](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-ndistimeddatahang)

[**NdisTimedDataSend**](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-ndistimeddatasend)

[**NdisTimedOidComplete**](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-ndistimedoidcomplete)

[**WlanAssert**](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wlanassert)

[**WlanAssociation**](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wlanassociation)

[**WlanConnectionRoaming**](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wlanconnectionroaming)

[**WlanDisassociation**](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wlandisassociation)

[**WlanTimedAssociation**](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wlantimedassociation)

[**WlanTimedConnectionRoaming**](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wlantimedconnectionroaming)

[**WlanTimedConnectRequest**](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wlantimedconnectrequest)

[**WlanTimedScan**](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wlantimedscan)

[**WlanTimedLinkQuality**](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wlantimedlinkquality)

## <a name="span-idactivating_this_optionspanspan-idactivating_this_optionspanspan-idactivating_this_optionspanactivating-this-option"></a><span id="Activating_this_option"></span><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>このオプションをアクティブにする


ドライバー検証ツールマネージャーまたは Verifier コマンドラインを使用して、1つまたは複数のドライバーの NDIS/WIFI 検証機能をアクティブにすることができます。 詳細については、「[ドライバーの検証オプションの選択](selecting-driver-verifier-options.md)」を参照してください。 NDIS/WIFI 検証オプションをアクティブ化または非アクティブ化するには、コンピューターを再起動する必要があります。

-   **コマンドラインで**

    コマンドラインでは、NDIS/WIFI 検証は**ベリファイア/flags 0x200000** (ビット 21) で表されます。 NDIS/WIFI 検証をアクティブにするには、フラグ値0x200000 を使用するか、または0x200000 をフラグ値に追加します。 例 :

    ```
    verifier /flags 0x200000 /driver MyDriver.sys
    ```

    この機能は、次回の起動時にアクティブになります。

-   **ドライバー検証マネージャーの使用**

    1.  ドライバー検証マネージャーを起動します。 コマンドプロンプトウィンドウで「 **Verifier** 」と入力します。
    2.  [**カスタム設定の作成] (コード開発者向け)** を選択し、 **[次へ]** をクリックします。
    3.  [**完全な一覧から個々の設定を選択]** を選択します。
    4.  **[NDIS/WIFI の検証]** を選択します。
    5.  コンピューターを再起動します。

 

 





