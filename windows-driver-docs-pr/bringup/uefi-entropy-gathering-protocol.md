---
title: UEFI エントロピ収集プロトコル
description: プロトコルを収集する UEFI エントロピは、よく知られている方法でランダムな数の生成 (RNG) の値を生成するために使用されます。
ms.assetid: 616F178F-B4A0-4B8B-B71D-F7474738EA35
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a1ce227750ac8a71300da634487ad586357a5140
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551472"
---
# <a name="uefi-entropy-gathering-protocol"></a>UEFI エントロピ収集プロトコル


プロトコルを収集する UEFI エントロピは、よく知られている方法でランダムな数の生成 (RNG) の値を生成するために使用されます。

このプロトコルを実装する UEFI RNG サービスは、RNG アルゴリズムを識別し、入力値とのエントロピのソースの状態も含め、内部の状態に基づいて RNG 値を提供する、省略可能な入力値を受け取る。 生のエントロピのソースの出力では、確定的なランダム ビット ジェネレーター (DRBG) を使用するときに、セキュリティ レベルは 256 ビット以上である必要があります。

このプロトコルで使用する RNG 値を作成する標準的なメソッドについてのガイダンスについては、[確定的なランダム ビット ジェネレーターを使用して乱数の NIST SP 800-90A に関する推奨事項]( https://go.microsoft.com/fwlink/p/?LinkId=523737)を参照してください。

## <a name="protocol-interface"></a>プロトコル インターフェイス


-   [EFI\_RNG\_サービス\_バインド\_プロトコル](efi-rng-service-binding-protocol.md)

-   [EFI\_RNG\_プロトコル](efi-rng-protocol.md)

-   [**EFI\_RNG\_アルゴリズム\_一覧**](efi-rng-algorithm-list.md)

 

 




