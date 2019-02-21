---
title: 純粋なデバイス
description: 純粋なデバイス
ms.assetid: 6ad3412c-fd80-41c0-9abc-117aacc5ddae
keywords:
- Windows 2000 の WDK の表示、純粋なデバイスの DirectX 8.0 リリース ノートします。
- 純粋なデバイス WDK DirectX 8.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dad6e90c59628d677f3ddc45d3dc4978fc04aecc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552125"
---
# <a name="pure-devices"></a>純粋なデバイス


## <span id="ddk_pure_devices_gg"></span><span id="DDK_PURE_DEVICES_GG"></span>


DirectX 8.0 では、「純粋な」デバイスの概念を紹介します。 純粋なデバイスを使用する場合、ランタイムはしない状態または状態のブロックを追跡または、ソフトウェアの頂点ハードウェアに代わって処理を実行します。 さらに、アプリケーションは、ランタイムから戻る状態を照会することはできません。 状態の追跡、状態のブロックを使用しているときに特にの不足は、アプリケーションの大幅なパフォーマンスを向上させる可能性があります。

ハードウェアで直接サポートされている唯一の頂点の処理は、純粋なデバイスを使用する場合、アプリケーションで使用できます。 たとえば、および照明は、ハードウェア変換をサポートしないカードは、pretransformed 頂点のみを Direct3D に渡すことができます。 さらに、API 関数**SetClipStatus**、 **GetClipStatus**と**ProcessVertices**純粋なデバイスでは使用できません。

純粋なデバイスを使用するには、アプリケーションする必要があります要求、デバイス作成フラグ D3DCREATE\_PUREDEVICE とドライバーは、純粋なデバイスとして動作する機能を報告する必要があります。

 

 





