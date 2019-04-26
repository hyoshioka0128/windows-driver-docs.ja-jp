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
ms.openlocfilehash: 9276b12ec7d0b8e9c5238bc526f2d66b518e02a4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349144"
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


[NPIV 状態コード](https://msdn.microsoft.com/library/windows/hardware/dn386176)

 

 






