---
title: ストレージクラスのメモリについて
description: Windows の記憶域ドライバースタックとプラットフォームファームウェア間のデバイスクラス固有の通信をサポートするために、Microsoft では、記憶域ドライバーで使用できるデバイス固有のメソッド (_DSM) を定義しています。
ms.assetid: e4f354d0-f292-4dc2-a7e3-edd8dfa63b90
ms.localizationpriority: medium
ms.date: 12/15/2019
ms.openlocfilehash: 1e47c9a6b6fea8200241e624c1ae5ba5ce3667b6
ms.sourcegitcommit: e1ff1dd43b87dfb7349cebf70ed2878dc8d7c794
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/02/2020
ms.locfileid: "75606538"
---
# <a name="about-storage-class-memory"></a>ストレージクラスのメモリについて

Windows の記憶域ドライバースタックとプラットフォームファームウェア間のデバイスクラス固有の通信をサポートするために、Microsoft では、記憶域ドライバーで使用できるデバイス固有のメソッド (_DSM) を定義しています。

バイトアドレッシング可能なエネルギーサポート関数クラス (関数インターフェイス 1) の _DSM インターフェイスは、BIOS の複雑さを最小限に抑えるために、JEDEC バイトのアドレス指定可能なエネルギーサポートインターフェイス標準にマップされるように設計されています。 これは、デバイスの機能をレポートするための一般的な機能を提供します。これは、OS ソフトウェアが同じメカニズムを使用してさまざまな実装と対話できるようにするための機能 & ます。 さらに、I2C レジスタにアクセスすることによって、ベンダー固有の機能をサポートできます。 JEDEC バイトのアドレス指定可能なエネルギーサポートインターフェイス標準をサポートする NVDIMM-N には、バイトアドレス可能なエネルギー (0x1) と関数インターフェイス値0x1 の関数クラスがあります。

## <a name="related-topics"></a>関連トピック

[記憶域ドライバーの設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/storage)

[JEDEC バイトのアドレス指定可能なエネルギー関数クラスのインターフェイスの _DSM (関数インターフェイス 1)](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)
