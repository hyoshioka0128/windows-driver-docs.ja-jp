---
title: NDIS のヘッダー バージョンのサポートの概要
description: NDIS のヘッダー バージョンのサポートの概要
ms.assetid: f73baf8d-f6da-486c-b0e2-c3c57aeab269
keywords:
- NDIS バージョン情報 WDK、構造の要件
- NDIS バージョン情報 WDK、ヘッダーのメンバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e202b391daab20778cbbe2bfbe28ee02a986930
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569943"
---
# <a name="overview-of-ndis-support-for-header-versions"></a>NDIS のヘッダー バージョンのサポートの概要





多くの NDIS 構造体には、構造体のバージョン情報が含まれます。 NDIS または NDIS ドライバーの初期化、**ヘッダー**構造ごとに必要に応じて、このような構造内のメンバー。 NDIS ドライバーが存在する場合、バージョン情報を確認する必要があります構造体のメンバーにアクセスする前に、各構造にします。

**ヘッダー**メンバーは、 [ **NDIS\_オブジェクト\_ヘッダー** ](https://msdn.microsoft.com/library/windows/hardware/ff566588)構造体。 この構造体には、リビジョン番号、型、およびを含む構造体のサイズが含まれています、**ヘッダー**メンバー。

構造体が含まれる、**ヘッダー**メンバーは、次の要件を満たします。

-   構造体は、新しい NDIS バージョンについては、メンバーの一覧に新しい情報が追加された場合、新しいリビジョン値があります。 たとえば、構造体の NDIS 6.1 バージョンは、共用体、または、ビットマスクのメンバーの一覧の最後に新しいメンバーを持つと、NDIS 6.0 のバージョンから別のリビジョン値があります。

-   構造体が変更された後は、構造体の新しいバージョンのサイズは、構造体の以前のリビジョンのサイズ以上にできますより小さいことはできません。 新しいサイズが以前のリビジョンのサイズより大きい場合は、新しいメンバーは、メンバー リストの末尾に追加されます。

-   構造体は、以前のバージョン情報が有効であり、完全な場合は、新しいリビジョンを必要のみがあります。 つまり、構造体の新しいバージョンには、以前のバージョンのメンバーのスーパー セットが含まれています。
    **注**  場合は、上記の条件のいずれかを満たすことができない、NDIS は既存の構造の改訂版を提供する代わりに既存の構造を置換する新しい名前を持つ新しい構造体を提供します。

     

-   NDIS ドライバーでは、定義済みのリビジョン値を常に使用する必要があります。 NDIS Xxx の形式では、このような定義を提供する\_リビジョン\_Nn と NDIS\_SIZEOF\_Xxx\_リビジョン\_Nn の**リビジョン**と**サイズ**のメンバー [ **NDIS\_オブジェクト\_ヘッダー** ](https://msdn.microsoft.com/library/windows/hardware/ff566588)それぞれします。 また、Xxx は、構造体の名前を表す、Nn はリビジョン番号。 リビジョンとの最初のリビジョンのサイズなど、 [ **NDIS\_フィルター\_部分\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff565544)構造は NDIS\_フィルター\_部分\_特性\_リビジョン\_1 および NDIS\_SIZEOF\_フィルター\_部分\_特性\_リビジョン\_1 それぞれします。

-   **Header.Size**値が同じにする必要があります、 **Header.Revision**値。 つまり場合、**リビジョン**メンバーには Xxx が含まれています\_リビジョン\_1、**サイズ**NDIS 以上のメンバー値がある必要があります\_SIZEOF\_Xxx\_リビジョン\_1。

## <a name="related-topics"></a>関連トピック


[NDIS のバージョンの概要](overview-of-ndis-versions.md)

[NDIS バージョン情報を指定します。](specifying-ndis-version-information.md)

 

 






