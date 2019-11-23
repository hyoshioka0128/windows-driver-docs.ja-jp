---
title: NDIS ドライバーのバージョン情報要件
description: NDIS ドライバーのバージョン情報要件
ms.assetid: a05e7dde-d1f9-458d-8d7b-ead9bb9af7af
keywords:
- NDIS バージョン情報 WDK、NDIS の役割
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f10408f8a868f56457826573d5c26b52cec4f385
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842960"
---
# <a name="version-information-requirements-for-ndis-drivers"></a>NDIS ドライバーのバージョン情報要件





バージョン情報を提供する NDIS 構造体には、**ヘッダーメンバーが**含まれています。これは、ヘッダーの構造体と\_して、ヘッダーの構造体として定義されています[ **\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_object_header)構造および ndis ドライバーでは、このようなバージョン情報

Ndis は、*現在のバージョン*の ndis (つまり、コンピューターが実行されているオペレーティングシステムのバージョンでサポートされているバージョンの ndis) よりも前のバージョンをサポートするドライバーをサポートできます。 また、ドライバーの登録されている*NDIS バージョン*(ドライバーが初期化中に報告したバージョン) は、ドライバーがサポートする最大バージョンよりも古い場合があります。 たとえば、ndis 5.1 ドライバーまたは NDIS 6.1 ドライバーは、NDIS 6.0 を実行しているオペレーティングシステムのバージョンで実行できます。 NDIS 5.1 ドライバーは、初期化中に NDIS 5.1 ドライバーとして登録するだけです。 ただし、NDIS 6.1 ドライバーでは、現在のバージョンの NDIS を確認する必要があり、使用可能な最高レベルの NDIS (この例では NDIS 6.0) をサポートするドライバーとして登録する必要があります。 現在の NDIS バージョンを取得する方法の詳細については、「 [Ndis バージョンの](obtaining-the-ndis-version.md)取得」を参照してください。

**ただし**、将来の構造のリビジョンでは、ドライバーがすべての機能をサポートする必要が  ことに注意してください。 たとえば、ミニポートドライバーでは、バージョン2の構造を作成し、バージョン1の構造に適した値を指定できます。

 

バージョン情報が含まれる構造体のメンバーにアクセスするには、NDIS ドライバーが次のプロセスを完了する必要があります。

-   構造体のメンバーにアクセスする前に、 **header**および**header.** のメンバーのサイズを確認してください。

-   以前のバージョンの構造体 (つまり、ドライバーがサポートする NDIS バージョンに関連付けられている数よりも低いリビジョン番号を持つ構造体) の場合は、次のようになります。
    -   ドライバーは、ヘッダーの**サイズ**の値が正しいことを確認する必要があります。 **Revision**値です。 たとえば、NDIS\_SIZEOF\_Xxx\_REVISION\_1 の値は、Xxx\_REVISION\_1 に対しては適切ですが、Xxx\_REVISION\_2 には小さすぎます。
    -   **ヘッダーのサイズ**値は、NDIS\_SIZEOF\_XXX\_Revision\_Nn (ここで、 *nn*はドライバーが使用している構造体のリビジョン番号) 以上である必要があります。また、ドライバーは、そのリビジョンに適した構造体の情報を正しく処理する必要があります。
-   より新しいバージョン構造 (つまり、ドライバーがサポートする NDIS バージョンに関連付けられている数よりもリビジョン番号が高い構造体) の場合、ドライバーは構造体の古いリビジョンと同様に構造体を使用できます。 より新しいバージョンの構造は、常に古いバージョンと互換性があります。

-   ドライバーは、登録されている NDIS バージョンのドライバーについて、構造の正しいリビジョンを使用する必要があります。 たとえば、ndis 6.1 ドライバーは、ndis [ **\_オブジェクト\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_object_header)構造のメンバーを設定して、NDIS\_オフロード\_リビジョン\_2 を示すことによって、NDIS [ **\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload)構造のオフロード機能を報告する必要があります。 ただし、ドライバーは、NDIS\_オフロード\_リビジョン\_2 に含まれるすべての機能をサポートする必要はありません。

-   OID セット要求を正常に処理するドライバーは、OID セット要求から戻ったときに、 [**NDIS\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体で**supportedrevision**メンバーを設定する必要があります。 **Supportedrevision**メンバーは、ドライバーがサポートしているリビジョンの要求をイニシエーターに通知します。 たとえば、ミニポートドライバーでは、Xxx\_REVISION\_2 の構造を作成し、Xxx\_REVISION\_1 構造に適切な値を指定して、構造体の残りの部分に0を設定できます。 ミニポートドライバーは、 **supportedrevision**メンバーで XXX\_REVISION\_1 を報告します。 この場合、Xxx\_リビジョン\_2 をサポートするプロトコルドライバーでは、ミニポートドライバーがサポートする Xxx\_リビジョン\_1 の情報が使用されます。

-   基になるドライバーによって正常に処理された情報を確認するために、OID 要求を発行するドライバーは、oid 要求が返された後に、NDIS\_OID\_要求構造の**Supportedrevision**メンバーの値を確認する必要があります。

## <a name="related-topics"></a>関連トピック


[NDIS バージョンの概要](overview-of-ndis-versions.md)

[NDIS バージョン情報の指定](specifying-ndis-version-information.md)

 

 






