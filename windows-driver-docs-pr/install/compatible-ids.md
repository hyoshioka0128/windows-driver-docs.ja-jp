---
title: 互換性 ID
description: 互換性のある ID は、Windows を使用して、INF ファイルをデバイスに一致するベンダ定義の識別文字列です。
ms.assetid: 3d20b43a-9e2b-4a8d-9a1a-eb9217233405
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca1396eab5f1f442f791a7bf8323771823c96079
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578169"
---
# <a name="compatible-id"></a>互換性 ID

互換性のある ID は、Windows を使用して、INF ファイルをデバイスに一致するベンダ定義の識別文字列です。 デバイスを関連付けることができますと互換性のある Id の一覧。 互換性 Id は、適合性が高い順に表示する必要があります。 Windows では、デバイスのハードウェア Id のいずれかに一致する INF ファイルで特定できない場合は、INF ファイルを検索する互換性 Id が使用されます。 互換性のある Id と同じ形式である[ハードウェア Id](hardware-ids.md)します。 ただし、互換性 Id は通常、ハードウェア Id よりも汎用的な。

仕入先には、互換性のあるドライバー ノードの ID を指定する INF ファイルが付属しています場合、は、仕入先が、INF ファイルで互換性のある ID と一致するすべてのハードウェアがサポートしていることを確認する必要がありますください。

デバイスの互換性 Id の一覧を取得する呼び出し[ **IoGetDeviceProperty** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdeviceproperty)で、 *DeviceProperty*パラメーターに設定**DevicePropertyCompatibleID**します。 このルーチンを取得する互換性 Id の一覧は、 [REG_MULTI_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)値。 互換性のある各 ID と最終的な NULL 終端文字の後に、NULL 終端文字を含む、互換性のある ID 一覧内の文字の最大数は、REGSTR_VAL_MAX_HCID_LEN です。 互換性 Id の一覧で、Id の考えられる最大数は、64 です。
