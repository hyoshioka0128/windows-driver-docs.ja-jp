---
title: バグ チェック 0x158 ILLEGAL_IOMMU_PAGE_FAULT
description: ILLEGAL_IOMMU_PAGE_FAULT のバグ チェックでは、0x00000158 の値を持ちます。 これは、IOMMU が、無効な ASID のページ フォールトのパケットを配信されたことを示します。
ms.assetid: E26C9B67-A332-4AE9-9325-9A3378EC9B36
keywords:
- バグ チェック 0x158 ILLEGAL_IOMMU_PAGE_FAULT
- ILLEGAL_IOMMU_PAGE_FAULT
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ILLEGAL_IOMMU_PAGE_FAULT
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2f0e6ab0034db9e7e5e302f1f5591c105ddc37de
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537809"
---
# <a name="bug-check-0x158-illegaliommupagefault"></a>バグ チェック 0x158 の。無効な\_IOMMU\_ページ\_エラー


不正な\_IOMMU\_ページ\_フォールトのバグ チェックが 0x00000158 の値を持ちます。 これは、IOMMU が、無効な ASID のページ フォールトのパケットを配信されたことを示します。 ASID が既に再利用されたため安全ではありません。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

## <a name="illegaliommupagefault-parameters"></a>無効な\_IOMMU\_ページ\_フォールト パラメーター


| パラメーター | 説明                           |
|-----------|---------------------------------------|
| 1         | 無効な ASID します。                     |
| 2         | 現在、ASIDs の数が使用されています。 |
| 3         | この ASID を使用して、プロセス。          |
| 4         | ASID の参照カウントします。           |

 

 

 




