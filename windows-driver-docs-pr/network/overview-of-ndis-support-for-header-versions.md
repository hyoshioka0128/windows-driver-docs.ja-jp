---
title: NDIS のヘッダー バージョンのサポートの概要
description: NDIS のヘッダー バージョンのサポートの概要
ms.assetid: f73baf8d-f6da-486c-b0e2-c3c57aeab269
keywords:
- NDIS バージョン情報 WDK、構造要件
- NDIS バージョン情報 WDK、ヘッダーメンバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15ef790e46a20d284d924b0053c74b2fec20b253
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843735"
---
# <a name="overview-of-ndis-support-for-header-versions"></a>NDIS のヘッダー バージョンのサポートの概要





多くの NDIS 構造体には、構造のバージョン情報が含まれています。 NDIS または NDIS ドライバーは、構造体ごとに必要に応じて、このような構造体の**ヘッダー**メンバーを初期化します。 NDIS ドライバーは、構造体のメンバーにアクセスする前に、各構造内のバージョン情報 (存在する場合) を確認する必要があります。

**ヘッダー**メンバーは、[**ヘッダー構造\_の NDIS\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_object_header)です。 この構造体には、**ヘッダー**メンバーを含む構造体のリビジョン番号、型、およびサイズが含まれます。

**ヘッダー**メンバーを含む構造体は、次の要件を満たしています。

-   新しいバージョンの NDIS のメンバーリストに新しい情報が追加されると、構造体に新しいリビジョン値が設定されます。 たとえば、構造体の NDIS 6.1 バージョンに、メンバーリストの末尾、共用体、またはビットマスクの新しいメンバーが含まれている場合、NDIS 6.0 バージョンとは異なるリビジョン値になります。

-   構造体が変更された後、構造体の新しいリビジョンのサイズは、構造体の以前のリビジョンのサイズ以上になることがありますが、それほど小さくはなりません。 新しいサイズが以前のリビジョンのサイズより大きい場合は、メンバーリストの末尾に新しいメンバーが追加されます。

-   構造体には、以前のリビジョン情報がまだ有効で完全な場合にのみ、新しいリビジョンが含まれます。 つまり、構造体の新しいバージョンには、以前のバージョンのメンバーのスーパーセットが含まれています。
    **注**  上記のいずれかの条件を満たすことができない場合は、既存の構造の改訂版を提供するのではなく、既存の構造を置き換える新しい名前を持つ新しい構造体が NDIS によって提供されます。

     

-   NDIS ドライバーは、常に定義済みのリビジョン値を使用する必要があります。 Ndis は、このような定義を Xxx\_REVISION\_Nn という形式で提供し、NDIS\_SIZEOF\_Xxx\_REVISION\_Nn を提供します。これには、それぞれ[**ndis\_OBJECT\_HEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_object_header)の**リビジョン**と**Size**メンバーが含まれます。 また、Xxx は構造体の名前を表し、Nn はリビジョン番号です。 たとえば、Ndis\_フィルターの最初のリビジョンのリビジョンとサイズ[ **\_部分的な\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_partial_characteristics)の構造は、\_リビジョン\_1 および NDIS\_SIZEOF\_フィルター\_部分的\_な\_の特性\_リビジョン\_1 に\_ます。\_

-   **ヘッダーのサイズ**値は、 **header. Revision**値と一致している必要があります。 つまり、**リビジョン**メンバーに XXX\_revision\_1 が含まれている場合、 **Size**メンバーの値は、NDIS\_SIZEOF\_Xxx\_Revision\_1 と同じかそれ以上である必要があります。

## <a name="related-topics"></a>関連トピック


[NDIS バージョンの概要](overview-of-ndis-versions.md)

[NDIS バージョン情報の指定](specifying-ndis-version-information.md)

 

 






