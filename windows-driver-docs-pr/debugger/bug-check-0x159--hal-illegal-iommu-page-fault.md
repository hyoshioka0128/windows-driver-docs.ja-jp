---
title: バグ チェック 0x159 HAL_ILLEGAL_IOMMU_PAGE_FAULT
description: HAL_ILLEGAL_IOMMU_PAGE_FAULT のバグ チェックでは、0x00000159 の値を持ちます。
ms.assetid: 2431EDC4-53B3-4E17-86D8-3B6911B21C98
keywords:
- バグ チェック 0x159 HAL_ILLEGAL_IOMMU_PAGE_FAULT
- HAL_ILLEGAL_IOMMU_PAGE_FAULT
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- HAL_ILLEGAL_IOMMU_PAGE_FAULT
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 205a130063e804f91179758b12e432d72fd798f0
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67520031"
---
# <a name="bug-check-0x159-halillegaliommupagefault"></a>バグ チェック 0x159:HAL\_不正な\_IOMMU\_ページ\_エラー


HAL\_不正な\_IOMMU\_ページ\_フォールトのバグ チェックが 0x00000159 の値を持ちます。 これは、IOMMU が解放中にあった、ASID に対してページ フォールトを配信されたことを示します。 ドライバーは、実行中の要求を完了する前に、時間とこのバグチェックのこの時点では、システム内のドライバーでは、実行していないことを示します担当しました。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


## <a name="halillegaliommupagefault-parameters"></a>HAL\_不正な\_IOMMU\_ページ\_フォールト パラメーター


| パラメーター | 説明                       |
|-----------|-----------------------------------|
| 1         | IOMMU ベンダー曖昧性除去       |
| 2         | パケットのエラーへのポインター           |
| 3         | 仕入先の特定のエラー パケット データ |
| 4         | 仕入先の特定のエラー パケット データ |

 

| パラメーター | 説明                           |
|-----------|---------------------------------------|
| 1         | IOMMU ベンダー曖昧性除去 0x3xxx を = です。 |
| 2         | 状況                                |
| 3         | PASID                                 |
| 4         | DirectoryBase                         |

 

 

 




