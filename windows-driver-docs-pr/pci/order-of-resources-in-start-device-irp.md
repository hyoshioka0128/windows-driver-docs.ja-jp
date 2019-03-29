---
title: 開始デバイス IRP でのリソースの順序
description: 開始デバイス IRP でのリソースの順序
ms.assetid: df55105e-3da3-40cc-9f57-05632cb2d043
keywords:
- WDK の PCI リソースの順序
- デバイスの起動 IRP WDK PCI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 95d42a0e70ca1fd6db46c0b73b8a78f413dbdd9a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574892"
---
# <a name="order-of-resources-in-start-device-irp"></a>開始デバイス IRP でのリソースの順序


デバイスの起動の I/O 要求パケット (IRP) で報告されるリソースの順序は、PCI ベース アドレス レジスタ (棒) に記載されているリソースの順序と一致する必要があります。 リソースの一覧、生と翻訳の 2 種類があります。 各リソースのリストには、リソースの記述子があります。 リソースの一覧内のリソースの記述子では、PCI デバイスのベース アドレス レジスタ (バー) の順序です。 Raw と翻訳されたリスト内のリソースの順序は同じです。 2 つの連続するリソースの記述子の間でデバイスのユーザーの記述子のデータがあります。 バーのリソースの記述子は、拡張メッセージ シグナル割り込み (MSI X) のメッセージの 1 つまたは複数の記述子または記述子が 1 つの MSI、またはハードウェア ベースの割り込みの 1 つまたは複数の記述子に続きます。 場合によってなどビデオ デバイスは、たとえば、バーの記述子が続きますレガシ ビデオ リソースの記述子。 すべてのハードウェア プラットフォーム上の PCI デバイス上のバーと一致するリソース一覧の横棒の記述子の順序が保証されます。

 

 




