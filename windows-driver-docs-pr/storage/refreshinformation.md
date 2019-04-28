---
title: RefreshInformation 関数
description: RefreshInformation WMI メソッドは、呼び出し元のインスタンスのオブジェクトに対応する HBA のすべてのテーブルを更新します。
ms.assetid: da78db30-0498-4d44-b5bc-76d08dc15938
keywords:
- 記憶装置の RefreshInformation 関数
topic_type:
- apiref
api_name:
- RefreshInformation
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: bcf4080e89dd4e018cb4db99ed21e9d7fb78818d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366356"
---
# <a name="refreshinformation-function"></a>RefreshInformation 関数


**RefreshInformation** WMI メソッドが呼び出し元のインスタンスのオブジェクトに対応する HBA のすべてのテーブルを更新します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void RefreshInformation(void);
```

<a name="parameters"></a>パラメーター
----------

この関数には、パラメーターがありません。

<a name="return-value"></a>戻り値
------------

適用できません。

<a name="remarks"></a>注釈
-------

**RefreshInformation** WMI メソッドには、次の WMI メソッドによって取得されるポート属性データが更新されます。

[**GetDiscoveredPortAttributes**](getdiscoveredportattributes.md)

[**GetFC3MgmtInfo**](getfc3mgmtinfo.md)

[**GetFC4Statistics**](getfc4statistics.md)

[**GetFCPStatistics**](getfcpstatistics.md)

[**GetPortAttributesByWWN**](getportattributesbywwn.md)

この WMI メソッドが属する、 [MSFC\_HBAAdapterMethods WMI クラス](msfc-hbaadaptermethods-wmi-class.md)します。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**GetDiscoveredPortAttributes**](getdiscoveredportattributes.md)

[**GetFC3MgmtInfo**](getfc3mgmtinfo.md)

[**GetFC4Statistics**](getfc4statistics.md)

[**GetFCPStatistics**](getfcpstatistics.md)

[**GetPortAttributesByWWN**](getportattributesbywwn.md)

 

 






