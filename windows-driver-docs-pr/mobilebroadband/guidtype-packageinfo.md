---
title: GUIDType (PackageInfo)
description: GUIDType (PackageInfo)
ms.assetid: 3f88df5a-2a17-4006-ad3b-aab9a12cbcb9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 56c027f7cbf898c7ff6035974eba89d08d0a0ea0
ms.sourcegitcommit: f017184b00f59b088df87a5bd85fec51b7aed8b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2019
ms.locfileid: "72323692"
---
# <a name="guidtype-packageinfo"></a>GUIDType (PackageInfo)

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

GUIDType XML 単純型は GUID を指定します。

``` syntax
<xs:simpleType name="GUIDType">
  <xs:restriction base="xs:string">
    <xs:pattern value="[0-9a-fA-F]{8}-[0-9a-fA-F]{4}-[0-9a-fA-F]{4}-[0-9a-fA-F]{4}-[0-9a-fA-F]{12}" />
  </xs:restriction>
</xs:simpleType>
```

## <a name="span-idpatternsspanspan-idpatternsspanspan-idpatternsspanpatterns"></a><span id="Patterns"></span><span id="patterns"></span><span id="PATTERNS"></span>タン


GUIDType 単純型は、次のパターンによって制限される**xs: string**です。

-   \[0-9a-z-F\]{8}-\[0-9a-z-F\]{4}-\[0-9a-z-f\]{4}-\[0-9a-z-f\]{4}-\[0-9a-z-F-F-F-F\]{12}

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈


GUIDType XML simple 型は、デバイスのメタデータパッケージ内のコンポーネント (デバイスの[ExperienceID](experienceid.md)、 [LanguageNeutralIdentifier](languageneutralidentifier.md)、 [modelid](modelid.md)の値など) を一意に識別する GUID を指定します。

 

 





