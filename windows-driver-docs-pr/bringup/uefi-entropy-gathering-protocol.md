---
title: UEFI エントロピー収集プロトコル
description: UEFI エントロピ収集プロトコルは、よく知られた方法でランダム数値生成 (RNG) 値を生成するために使用されます。
ms.assetid: 616F178F-B4A0-4B8B-B71D-F7474738EA35
ms.date: 05/22/2020
ms.localizationpriority: medium
ms.openlocfilehash: 5e06b39ed9dde5d401fe231c909b35fa70c03d7b
ms.sourcegitcommit: 5273e44c5c6c1c87952d74e95e5473c32a916d10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/28/2020
ms.locfileid: "84122681"
---
# <a name="uefi-entropy-gathering-protocol"></a>UEFI エントロピー収集プロトコル

UEFI エントロピ収集プロトコルは、よく知られた方法でランダム数値生成 (RNG) 値を生成するために使用されます。

このプロトコルを実装する UEFI RNG サービスは、RNG アルゴリズムを識別するオプションの入力値を受け取り、入力値と内部状態 (エントロピソースの状態を含む) に基づいて RNG 値を提供します。 未加工のランダムビットジェネレーター (DRBG) が未加工のエントロピソースの出力で使用される場合、そのセキュリティレベルは少なくとも256ビットである必要があります。

このプロトコルで使用される RNG 値を作成するための標準的な方法については、「 [NIST SP 800-90A Rev. 1-決定的ランダムビットジェネレーターを使用した乱数生成の推奨事項](https://csrc.nist.gov/publications/detail/sp/800-90a/rev-1/final)」を参照してください。

## <a name="protocol-interface"></a>プロトコルインターフェイス

- [EFI \_ RNG \_ サービス \_ バインド \_ プロトコル](efi-rng-service-binding-protocol.md)

- [EFI \_ RNG \_ プロトコル](efi-rng-protocol.md)

- [**EFI \_ RNG \_ アルゴリズムの \_ 一覧**](efi-rng-algorithm-list.md)
