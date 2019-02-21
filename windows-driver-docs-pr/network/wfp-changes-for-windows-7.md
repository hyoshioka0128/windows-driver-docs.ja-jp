---
title: Windows 7 の WFP 変更
description: Windows 7 の WFP 変更
ms.assetid: c7b15182-592a-4cdb-98aa-5283ed2f51a0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a743b026f257a29ae6edb8ec8d69125d977f3ae
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549946"
---
# <a name="wfp-changes-for-windows-7"></a>Windows 7 の WFP 変更


使用可能な関数と、Windows フィルタ リング プラットフォームを開始する Windows 7 での動作では、いくつかの変更が加えられました。 多くの場合、新しい機能を利用する必要がありますのコンパイル時またはを持つ、NTDDI コールアウト ドライバーを再コンパイル\_バージョン マクロ設定 NTDDI\_WIN7 します。

-   新しい関数:
    - [**FwpsAcquireClassifyHandle0**](https://msdn.microsoft.com/library/windows/hardware/ff550085)
    - [**FwpsAcquireWritableLayerDataPointer0**](https://msdn.microsoft.com/library/windows/hardware/ff550087)
    - [**FwpsApplyModifiedLayerData0**](https://msdn.microsoft.com/library/windows/hardware/ff551137)
    - [**FwpsCalloutRegister1**](https://msdn.microsoft.com/library/windows/hardware/ff551143)
    - [**FwpsCompleteClassify0**](https://msdn.microsoft.com/library/windows/hardware/ff551150)
    - [**FwpsPendClassify0**](https://msdn.microsoft.com/library/windows/hardware/ff551197)
    - [**FwpsReleaseClassifyHandle0**](https://msdn.microsoft.com/library/windows/hardware/ff551208)
    - [*classifyFn1*](https://msdn.microsoft.com/library/windows/hardware/ff544893)
    - [*notifyFn1*](https://msdn.microsoft.com/library/windows/hardware/ff568804)
    - [**FWPS\_NET\_バッファー\_一覧\_通知\_FN0**](https://msdn.microsoft.com/library/windows/hardware/ff552406)
    - [**FwpsInjectTransportSendAsync1**](https://msdn.microsoft.com/library/windows/hardware/ff551189)
    - [**FwpsNetBufferListAssociateContext0**](https://msdn.microsoft.com/library/windows/hardware/ff551191)
    - [**FwpsNetBufferListGetTagForContext0**](https://msdn.microsoft.com/library/windows/hardware/ff551192)
    - [**FwpsNetBufferListRemoveContext0**](https://msdn.microsoft.com/library/windows/hardware/ff551194)
    - [**FwpsNetBufferListRetrieveContext0**](https://msdn.microsoft.com/library/windows/hardware/ff551196)
    - [**FwpsAleEndpointCreateEnumHandle0**](https://msdn.microsoft.com/library/windows/hardware/ff550089)
    - [**FwpsAleEndpointDestroyEnumHandle0**](https://msdn.microsoft.com/library/windows/hardware/ff550091)
    - [**FwpsAleEndpointEnum0**](https://msdn.microsoft.com/library/windows/hardware/ff551126)
    - [**FwpsAleEndpointGetById0**](https://msdn.microsoft.com/library/windows/hardware/ff551128)
    - [**FwpsAleEndpointGetSecurityInfo0**](https://msdn.microsoft.com/library/windows/hardware/ff551131)
    - [**FwpsAleEndpointSetSecurityInfo0**](https://msdn.microsoft.com/library/windows/hardware/ff551133)
-   新しい構造および列挙体。
    - [**FWPS\_ALE\_エンドポイント\_ENUM\_TEMPLATE0**](https://msdn.microsoft.com/library/windows/hardware/ff551216)
    - [**FWPS\_ALE\_エンドポイント\_PROPERTIES0**](https://msdn.microsoft.com/library/windows/hardware/ff551218)
    - [**FWPS\_バインド\_REQUEST0**](https://msdn.microsoft.com/library/windows/hardware/ff551221)
    - [**FWPS\_CALLOUT1**](https://msdn.microsoft.com/library/windows/hardware/ff551226)
    - [**FWPS\_CONNECT\_REQUEST0**](https://msdn.microsoft.com/library/windows/hardware/ff551231)
    - [**FWPS\_フィールド\_ALE\_バインド\_リダイレクト\_V4**](https://msdn.microsoft.com/library/windows/hardware/ff551247)
    - [**FWPS\_フィールド\_ALE\_バインド\_リダイレクト\_V6**](https://msdn.microsoft.com/library/windows/hardware/ff551249)
    - [**FWPS\_フィールド\_ALE\_CONNECT\_リダイレクト\_V4**](https://msdn.microsoft.com/library/windows/hardware/ff551251)
    - [**FWPS\_フィールド\_ALE\_CONNECT\_リダイレクト\_V6**](https://msdn.microsoft.com/library/windows/hardware/ff551254)
    - [**FWPS\_フィールド\_ALE\_エンドポイント\_クロージャ\_V4**](https://msdn.microsoft.com/library/windows/hardware/ff551256)
    - [**FWPS\_フィールド\_ALE\_エンドポイント\_クロージャ\_V6**](https://msdn.microsoft.com/library/windows/hardware/ff551258)
    - [**FWPS\_フィールド\_ALE\_リソース\_リリース\_V4**](https://msdn.microsoft.com/library/windows/hardware/ff551269)
    - [**FWPS\_フィールド\_ALE\_リソース\_リリース\_V6**](https://msdn.microsoft.com/library/windows/hardware/ff551272)
    - [**FWPS\_フィールド\_受信\_MAC\_フレーム\_802\_3**](https://msdn.microsoft.com/library/windows/hardware/ff551291)
    - [**FWPS\_フィールド\_KM\_承認**](https://msdn.microsoft.com/library/windows/hardware/ff551312)
    - [**FWPS\_フィールド\_名前\_解決\_キャッシュ\_V4**](https://msdn.microsoft.com/library/windows/hardware/ff551316)
    - [**FWPS\_フィールド\_名前\_解決\_キャッシュ\_V6**](https://msdn.microsoft.com/library/windows/hardware/ff551320)
    - [**FWPS\_フィールド\_送信\_MAC\_フレーム\_802\_3**](https://msdn.microsoft.com/library/windows/hardware/ff551334)
    - [**FWPS\_フィールド\_ストリーム\_パケット\_V4**](https://msdn.microsoft.com/library/windows/hardware/ff552379)
    - [**FWPS\_フィールド\_ストリーム\_パケット\_V6**](https://msdn.microsoft.com/library/windows/hardware/ff552383)
    - [**FWPS\_FILTER1**](https://msdn.microsoft.com/library/windows/hardware/ff552389)
    - [**FWPS\_NET\_バッファー\_一覧\_イベント\_TYPE0**](https://msdn.microsoft.com/library/windows/hardware/ff552403)
    - [**FWPS\_トランスポート\_送信\_PARAMS1**](https://msdn.microsoft.com/library/windows/hardware/ff552423)
-   新しいドキュメントのトピック:
    - [Bind を使用して、またはリダイレクトの接続](using-bind-or-connect-redirection.md)
    - [パケットがタグ付けを使用してください。](using-packet-tagging.md)
    - [ALE エンドポイントの有効期間管理](ale-endpoint-lifetime-management.md)

 

 





