---
title: RemoveVirtualPort メソッド
description: RemoveVirtualPort メソッドは、特定のワールド ワイド ポート名 (WWPN) の仮想ポートを削除します。
ms.assetid: 47A85B72-821C-4552-BA6E-1742D58B54A4
keywords:
- 記憶装置の RemoveVirtualPort メソッド
topic_type:
- apiref
api_name:
- RemoveVirtualPort
api_type:
- COM
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ad9797ed32f6342c250075053b59930097a07844
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368913"
---
# <a name="removevirtualport-method"></a>RemoveVirtualPort メソッド


**RemoveVirtualPort**メソッドは、特定のワールド ワイド ポート名 (WWPN) の仮想ポートを削除します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void RemoveVirtualPort(
   [in] uint8   WWPN[8],
   [out] uint16 Status
);
```

<a name="parameters"></a>パラメーター
----------

*WWPN\[8\]*    
削除する仮想ポートのワールド ワイド ポート名。

*状態*   
に返された場合、操作の状態を格納します。

<a name="return-value"></a>戻り値
------------

WMI メソッドには適用されません。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[NPIV 状態コード](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/dn386176(v=vs.85))

 

 






