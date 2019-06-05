---
title: NDKPI の INF 要件
description: Network Direct カーネル (NDK) をサポートしているミニポート ドライバーの INF ファイルには、次の要件を満たす必要があります。
ms.assetid: 1399CEB8-82A5-4F91-833E-66FC5A5663C7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 39664bd7126518774e80a9e75ce8d71ad39d6557
ms.sourcegitcommit: 288c03841f90e6b03c98924a8d7cc44b5975b6f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/05/2019
ms.locfileid: "66686946"
---
# <a name="inf-requirements-for-ndkpi"></a>NDKPI の INF 要件


Network Direct カーネル (NDK) をサポートしているミニポート ドライバーの INF ファイルには、次の要件を満たす必要があります。

-   ミニポート ドライバーの INF ファイルでは、Windows コンポーネントを検出して、ドライバーによってサービスが提供される NDK 対応のミニポート アダプターを使用するために、"ndis5"の NDIS 範囲の上限値を指定する必要があります。 この値はよう指定します。

    ```INF
    HKR, Ndi\Interfaces, UpperRange, 0, "ndis5"
    ```

-   INF ファイルを指定する必要があります、  **\*NetworkDirect**キーワード値を次のようにします。 ドライバーがインストールされると、管理者を更新できる、  **\*NetworkDirect**でキーワード値、 **[詳細設定]** アダプターのプロパティ ページ。 

    **注**ミニポート ドライバーが自動的に再起動で、変更を行った後、 **[詳細設定]** アダプターのプロパティ ページ。

    ```INF
    HKR, Ndi\Params\*NetworkDirect,        ParamDesc,  0, "NetworkDirect Functionality"
    HKR, Ndi\Params\*NetworkDirect,        Type,       0, "enum"
    HKR, Ndi\Params\*NetworkDirect,        Default,    0, "1"
    HKR, Ndi\Params\*NetworkDirect\enum,   "0",        0, "Disabled"
    HKR, Ndi\Params\*NetworkDirect\enum,   "1",        0, "Enabled"
    ```

-   INF ファイルを指定する必要があります、  **\*NetworkDirectTechnology**キーワード値を次のようにします。 ドライバーがインストールされると、管理者を更新できる、  **\*NetworkDirectTechnology**でキーワード値、 **[詳細設定]** アダプターのプロパティ ページ。 列挙体は相互に排他的な他のすべてのユーザーを除外 NetworkDirectTechnology 値の選択を意味します。  これにより、厳密なデバイスの動作を定義するプラットフォーム。  
-   デバイスは、サポートされているトランスポートのみを表現する必要があります。  トランスポートの値は WDK にマップされる識別子**NDK_RDMA_TECHNOLOGY**します。  識別子の再定義は禁止されています。
-   同時実行の複数のトランスポートを使用したデバイスの動作は定義されません。  デバイス**する必要があります**トランスポートの種類を指定します。

    **注**ミニポート ドライバーが自動的に再起動で、変更を行った後、 **[詳細設定]** アダプターのプロパティ ページ。

    ```INF
    HKR, Ndi\Params\*NetworkDirectTechnology,        ParamDesc,  0,  "NetworkDirect Technology"
    HKR, Ndi\Params\*NetworkDirectTechnology,        Default,    0,  "0"
    HKR, Ndi\Params\*NetworkDirectTechnology,        Type,       0,  "enum"
    HKR, Ndi\Params\*NetworkDirectTechnology\enum,   1,          0,  "iWARP"
    HKR, Ndi\Params\*NetworkDirectTechnology\enum,   2,          0,  "InfiniBand"
    HKR, Ndi\Params\*NetworkDirectTechnology\enum,   3,          0,  "RoCE"
    HKR, Ndi\Params\*NetworkDirectTechnology\enum,   4,          0,  "RoCEv2"
    HKR, Ndi\Params\*NetworkDirectTechnology,        Optional,   0,  "0"
    ```

    高度なプロパティの詳細については、次を参照してください。[プロパティの詳細 ページの構成パラメーターを指定する](specifying-configuration-parameters-for-the-advanced-properties-page.md)します。

    詳細については、標準化された INF キーワードを使用して、次を参照してください。[ネットワーク デバイスの標準化された INF キーワード](standardized-inf-keywords-for-network-devices.md)します。

## <a name="related-topics"></a>関連トピック


[ネットワーク ダイレクト カーネル プロバイダー インターフェイス (NDKPI)](network-direct-kernel-programming-interface--ndkpi-.md)

 
