---
title: I/O リソース使用量の削減
description: I/O リソース使用量の削減
ms.assetid: ad83856c-ad1a-42fc-97f0-7881f745174d
keywords:
- I/O リソース使用量削減 WDK
- WDK リソースの使用状況
- I/O リソース WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9dd8e2275454ce40ab7afab5195fe834b41b8701
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527980"
---
# <a name="io-resource-usage-reduction"></a>I/O リソース使用量の削減


Microsoft では、PCI や PCI X、PCI Express デバイスが I/O のベース アドレス レジスタ (棒) によってアクセスされる入力/出力 (I/O) 領域のアドレスの使用量がある依存関係を減らすためにサポートを実装しました。 パーソナル コンピューターで使用される I/O リソースの数は、長年にわたり増加を続けています。 PCI や PCI X、バスの PCI Express でこの I/O リソースの使用量には、リソースの競合の問題の原因が、ますます。 これらの問題を悪化 PCI Express バス、PCI を使用するものと比較し、クライアントとサーバーの両方のシステムで使用されている仮想の PCI の PCI ブリッジの数が原因の PCI X バスを使用してシステムの必要があります。 遷移ハードウェアの設計とメモリ リソースより十分にあるを使用してに I/O リソースの依存から離れた場所に必要なことがそのためにします。 どのデバイスの製造元、ドライバーの開発者は、ファームウェア エンジニア、およびシステム製造元未使用の I/O バーを無効にし、軽減または解消できますコンピューターで使用される I/O の領域の量の詳細についてを参照してください、 [I/O リソースの使用量削減](https://go.microsoft.com/fwlink/p/?linkid=74197)ホワイト ペーパー。

Windows 10 の I/O リソースの使用量を減らすためには、デバイス ドライバーの INF ファイルで、次のエントリを配置します。

```cpp
[DDInstall.HW]
Include=pci.inf
Needs=PciIoSpaceNotRequired.HW
```

Windows 8.1 以降では、このエントリを使用します。

```cpp
[DDInstall.HW]
Include=machine.inf
Needs=PciIoSpaceNotRequired
```
