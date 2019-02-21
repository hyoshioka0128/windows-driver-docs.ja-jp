---
title: 記憶域クラス メモリ
description: Microsoft Windows での記憶域ドライバー スタックとプラットフォームのファームウェア間のデバイス固有クラスの通信をサポートするデバイス固有のメソッドを定義します (\_DSM) で記憶装置ドライバーを使用できます。
ms.assetid: e4f354d0-f292-4dc2-a7e3-edd8dfa63b90
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: abdc8fa4f230f816119a4f21f73b7371b1241909
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529057"
---
# <a name="storage-class-memory"></a>記憶域クラス メモリ


Microsoft Windows での記憶域ドライバー スタックとプラットフォームのファームウェア間のデバイス固有クラスの通信をサポートするデバイス固有のメソッドを定義します (\_DSM) で記憶装置ドライバーを使用できます。

\_DSM クラスのインターフェイスをバイト アドレス指定可能なエネルギー バックアップ関数 (関数のインターフェイスの 1) が BIOS の複雑さを軽減するために、JEDEC バイト アドレス指定可能なエネルギー バックアップ インターフェイスの標準にマップするように設計します。 OS ソフトウェアが同じメカニズムを通じてさまざまな実装が操作できるよう、デバイスの機能と機能、レポートの共通の基盤を提供します。 さらに、I2C レジスタへのアクセスによりベンダー固有の機能をサポートできます。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[ストレージ ドライバーの設計ガイド](https://go.microsoft.com/fwlink/p/?LinkId=798409)

[JEDEC バイトのアドレス指定可能なエネルギー バックアップ インターフェイス NVDIMM デバイス固有のメソッド (\_DSM)](jedec-byte-addressable-energy-backed-interface-nvdimms-device-specific-method---dsm-.md)

[\_バイトのアドレス指定可能なエネルギーの DSM インターフェイス関数クラス (関数インターフェイス 1) のバックアップ](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






