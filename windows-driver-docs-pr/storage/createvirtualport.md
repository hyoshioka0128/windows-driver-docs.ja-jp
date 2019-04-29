---
title: CreateVirtualPort メソッド
description: CreateVirtualPort メソッドでは、特定のワールド ワイド ポート名 (WWPN) を仮想ポートを作成します。
ms.assetid: B4274FB7-2850-4E17-ACDE-5592B0390E8B
keywords:
- 記憶装置の CreateVirtualPort メソッド
topic_type:
- apiref
api_name:
- CreateVirtualPort
api_type:
- COM
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 8bab66a53593ea632f35c83dc5c59e881098045e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392748"
---
# <a name="createvirtualport-method"></a>CreateVirtualPort メソッド


**CreateVirtualPort**メソッドは、特定のワールド ワイド ポート名 (WWPN) を仮想ポートを作成します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void CreateVirtualPort(
   [in] uint8   WWPN[8],
   [in] uint8   WWNN[8],
   [in] uint8   Tag[16],
   [in] uint16  VirtualName[64],
   [out] uint16 Status
);
```

<a name="parameters"></a>パラメーター
----------

*WWPN\[8\]*   
作成する仮想ポートのワールド ワイド ポート名。

*WWNN\[8\]*   
仮想ポートに関連付けるワールド ワイド ノード名。

*タグ\[16\]*   
仮想ポートのタグ識別子です。

*VirtualName\[64\]*   
仮想ポートのシンボリック名。

*状態*   
に返された場合、操作の状態を格納します。

<a name="return-value"></a>戻り値
------------

WMI メソッドには適用されません。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[NPIV 状態コード](https://msdn.microsoft.com/library/windows/hardware/dn386176)

 

 






