---
title: Bug Check 0x1D9 HAL_IOMMU_INTERNAL_ERROR
description: HAL_IOMMU_INTERNAL_ERROR のバグ チェックでは、0x000001D9 の値を持ちます。 これは、UcmUcsi ドライバーにエラーが発生することを示します。
keywords:
- Bug Check 0x1D9 HAL_IOMMU_INTERNAL_ERROR
- HAL_IOMMU_INTERNAL_ERROR
ms.date: 01/14/2019
topic_type:
- apiref
api_name:
- HAL_IOMMU_INTERNAL_ERROR
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f7d410ad4eb9d1e82016b692f11e8b1d71f016ae
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67519629"
---
# <a name="bug-check-0x1d9-haliommuinternalerror"></a>バグ チェック 0x1D9:HAL\_IOMMU\_内部\_エラー

HAL\_IOMMU\_内部\_エラーのバグ チェックが 0x000001D9 の値を持ちます。 HAL IOMMU ライブラリで内部エラーが検出されたことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。

 
## <a name="haliommuinternalerror-parameters"></a>HAL\_IOMMU\_内部\_エラー パラメーター

|パラメーター|説明|
|-------- |---------- |
|1| 失敗した操作を示します。 次の値を参照してください。|
|2| 次の値を参照してください。 |
|3| 次の値を参照してください。 |
|4| 次の値を参照してください。 |

**失敗した操作の値**

```text
0x00 : Failed to delete IOMMU domain
     Parameter 2 - Status
     Parameter 3 - Pointer to the IOMMU domain object

0x01 : Failed to unmap pages from IOMMU domain
     Parameter 2 - Status
     Parameter 3 - Pointer to the IOMMU domain object
     Parameter 4 - Logical address

0x02 : Failed to leave IOMMU domain
     Parameter 2 - Status
     Parameter 3 - Pointer to the IOMMU domain object
```

## <a name="cause"></a>原因
-----

HAL IOMMU ライブラリで内部エラーが検出されました。

## <a name="see-also"></a>関連項目
----------

[バグチェック コード リファレンス](bug-check-code-reference2.md)
