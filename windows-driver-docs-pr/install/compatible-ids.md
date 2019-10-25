---
title: 互換性 ID
description: 互換性のある ID とは、Windows がデバイスを INF ファイルに一致させるために使用するベンダー定義の識別文字列です。
ms.assetid: 3d20b43a-9e2b-4a8d-9a1a-eb9217233405
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aacb5ed0833711d7c054b8f39f32a5d46ecf25a1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837533"
---
# <a name="compatible-id"></a>互換性 ID

互換性のある ID とは、Windows がデバイスを INF ファイルに一致させるために使用するベンダー定義の識別文字列です。 デバイスは、互換性のある Id の一覧に関連付けることができます。 互換性 Id は、適合性を下げるためにリストされている必要があります。 デバイスのハードウェア Id のいずれかに一致する INF ファイルが見つからない場合は、互換性のある Id を使用して INF ファイルを見つけます。 互換性 Id は、[ハードウェア id](hardware-ids.md)と同じ形式です。 ただし、互換性のある Id は通常、ハードウェア Id よりも一般的です。

ベンダーからドライバーノードの互換性のある ID を指定する INF ファイルが提供されている場合、ベンダーは、その INF ファイルが互換性 ID と一致するすべてのハードウェアをサポートしているかどうかを確認する必要があります。

デバイスの互換性のある Id の一覧を取得するには、 *deviceproperty*パラメーターを**Devicepropertyの id**に設定して[**iogetdeviceproperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceproperty)を呼び出します。 このルーチンが取得する互換性 Id の一覧は、 [REG_MULTI_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)値です。 互換性 id リストに含まれる最大文字数は、互換性のある各 ID と最後の NULL 終端文字の後の NULL 終端文字を含む、REGSTR_VAL_MAX_HCID_LEN です。 互換性 Id のリストに含まれる Id の最大数は64です。
