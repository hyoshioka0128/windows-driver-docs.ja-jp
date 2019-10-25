---
title: リムーバブル子デバイスの処理
description: リムーバブル子デバイスの処理
ms.assetid: 0edc0331-7178-4986-b818-9f1ee8f12995
keywords:
- リムーバブル子デバイス WDK Windows 2000 ディスプレイ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e9654f75220144030e2f0f3171ade4e9bc0024f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838905"
---
# <a name="handling-removable-child-devices"></a>リムーバブル子デバイスの処理


ビデオミニポートドライバーは、リムーバブル子デバイスが別のデバイスで変更されたときに検出する必要があります。これにより、ドライバーが元の子デバイスのデータを使用することをプラグアンドプレイ (PnP) で防ぐことができます。 たとえば、ビデオミニポートドライバーは、ユーザーがモニターを切り替えるタイミングを検出する必要があります。

接続モニターの拡張表示情報データ (EDID) が、元のモニタースタックを破棄して新しいスタックを構築するのではなく、ビデオミニポートドライバーの[*HwVidGetVideoChildDescriptor*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_get_child_descriptor)関数の連続する呼び出し間で変更された場合新しいモニターでは、ビデオポートドライバーによって現在のスタックの状態が変更されます。 グラフィックスサブシステムは、新しいモニターの機能を判別できますが、元のスタックが破損していないため、他のオペレーティングシステムコンポーネント (PnP など) は元のモニターの機能データを使用します。

ビデオミニポートドライバーは、接続されているモニターの変更を検出し、次の操作のいずれかを実行して、PnP が元のモニターのデータを使用しないようにします。

1.  ビデオミニポートドライバーは、以前のモニタースタックを強制的に破棄するためのモニターが存在しないことを報告できます。 次に、新しいモニターを報告するために、ビデオポートドライバーが子デバイスを再列挙するように強制するために、ビデオミニポートドライバーは[**VideoPortEnumerateChildren**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportenumeratechildren)関数を呼び出します。 ビデオミニポートドライバーは、 **VideoPortEnumerateChildren**を呼び出して、モニターが切断されたことを報告する最初の列挙が完了した後にのみ、子デバイスの再列挙をスケジュールする必要があります。

2.  適切なコンピューターおよび監視構成 (次の例外を参照) では、ビデオミニポートドライバーは、 *UId*パラメーターが指す変数内の新しいモニターの*HwVidGetVideoChildDescriptor*に応答できます。 この値は、以前のモニターでビデオミニポートドライバーが使用していた値とは異なる必要があります。

Advanced Configuration and Power Interface (ACPI) 列挙モニタでは、32ビットのデバイス Id が BIOS 実装に関連付けられているため、通常は最初のメカニズムが推奨されます。 したがって、別の32ビットデバイス ID を指定することはできません。

 

 





