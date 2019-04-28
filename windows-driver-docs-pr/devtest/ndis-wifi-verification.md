---
title: NDIS/WIFI 検証
description: NDIS/WIFI の確認オプションは、NDIS かどうかを決定します。 または、Windows オペレーティング システムのカーネルと WIFI のドライバーが適切にやり取りします。
ms.assetid: EB553449-9460-403D-8ED2-343048C4B38C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a264380ac31820651232bd8ea018243ff99e117f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379494"
---
# <a name="ndiswifi-verification"></a>NDIS/WIFI 検証


NDIS/WIFI の確認オプションは、NDIS かどうかを決定します。 または、Windows オペレーティング システムのカーネルと WIFI のドライバーが適切にやり取りします。

**注**  このオプションは、Windows 8.1 以降から使用できます。

 

NDIS/WIFI の確認オプションには、ドライバーが正しくさまざまなコンテキストで Oid を処理し、Microsoft が推奨されるベスト プラクティスに依存していることを確認するためのルールが適用されます。

Driver Verifier では、このオプションがアクティブで、Driver Verifier は、ドライバーが違反 NDIS または WIFI の規則のいずれかを検出 (パラメーター 1 が特定のコンプライアンス規則の識別子に等しい) でのバグ チェック 0xC4 が発行されます。

検証ルールの一覧、次のとおりです。

[**NdisOidComplete**](https://msdn.microsoft.com/library/windows/hardware/dn305115)

[**NdisOidDoubleComplete**](https://msdn.microsoft.com/library/windows/hardware/dn305116)

[**NdisOidDoubleRequest**](https://msdn.microsoft.com/library/windows/hardware/dn305117)

[**NdisTimedDataHang**](https://msdn.microsoft.com/library/windows/hardware/dn305118)

[**NdisTimedDataSend**](https://msdn.microsoft.com/library/windows/hardware/dn305119)

[**NdisTimedOidComplete**](https://msdn.microsoft.com/library/windows/hardware/dn305120)

[**WlanAssociation**](https://msdn.microsoft.com/library/windows/hardware/dn305122)

[**WlanConnectionRoaming**](https://msdn.microsoft.com/library/windows/hardware/dn305123)

[**WlanDisassociation**](https://msdn.microsoft.com/library/windows/hardware/dn305124)

[**WlanTimedAssociation**](https://msdn.microsoft.com/library/windows/hardware/dn305125)

[**WlanTimedConnectionRoaming**](https://msdn.microsoft.com/library/windows/hardware/dn305126)

[**WlanTimedConnectRequest**](https://msdn.microsoft.com/library/windows/hardware/dn305127)

[**WlanTimedScan**](https://msdn.microsoft.com/library/windows/hardware/dn305129)

[**WlanTimedLinkQuality**](https://msdn.microsoft.com/library/windows/hardware/dn305128)

## <a name="span-idactivatingthisoptionspanspan-idactivatingthisoptionspanspan-idactivatingthisoptionspanactivating-this-option"></a><span id="Activating_this_option"></span><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>このオプションをアクティブ化します。


ドライバー検証マネージャーまたは Verifier.exe コマンドラインを使用して、1 つまたは複数のドライバーの NDIS/WIFI 検証の機能をアクティブにできます。 詳細については、次を参照してください。[ドライバー検証ツールのオプションの選択](selecting-driver-verifier-options.md)します。 NDIS/WIFI の確認オプションをアクティブ化またはコンピューターを再起動する必要があります。

-   **コマンドラインで**

    によって表される NDIS/WIFI 検証、コマンドラインで**verifier/flags 0x200000** (21 ビット)。 NDIS/WIFI の検証を有効にするには、0x200000 のフラグの値を使用して、または 0x200000 をフラグ値に追加します。 次に、例を示します。

    ```
    verifier /flags 0x200000 /driver MyDriver.sys
    ```

    この機能は、[次へ] の起動後にアクティブになります。

-   **ドライバー検証マネージャーを使用します。**

    1.  ドライバー検証マネージャーを起動します。 型**Verifier**コマンド プロンプト ウィンドウでします。
    2.  選択 **(コード開発者) 用のカスタム設定を作成する**順にクリックします**次**します。
    3.  選択**完全な一覧から個々 の設定を選択します。** します。
    4.  選択 (チェック) **NDIS/WIFI 検証**です。
    5.  コンピューターを再起動します。

 

 





