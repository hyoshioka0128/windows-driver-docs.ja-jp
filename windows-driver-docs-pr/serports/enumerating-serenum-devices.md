---
title: Serenum デバイスの列挙
description: Serenum デバイスの列挙
ms.assetid: c850c52b-82d7-48c2-a6c4-bfd071756632
keywords:
- Serenum ドライバー WDK、デバイスの列挙
- Serenum デバイス WDK シリアル デバイスを列挙します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db8c6cf08bc875c2f096b0d1c3b5156b1caaf8d9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552294"
---
# <a name="enumerating-serenum-devices"></a>Serenum デバイスの列挙





Microsoft Windows 2000 では、起動時に遅れる可能性がありますが大幅に高容量のマルチポート アダプター (16 個以上のポートを含む) を自動的に列挙するためにかかる時間。 この問題、Windows XP と後で次の拡張機能をサポートしています。

-   Windows 2000 と比較して、Serenum が自動的に処理能力の高いマルチポート アダプターを列挙するために必要な時間は大幅に減少します。

-   Serenum サポート、省略可能な Windows XP 以降では、 **SkipEnumerations**システムにインストールされているシリアル ポートごとのレジストリ エントリの値。 仕入先は、(またはデバイス マネージャーまたはハードウェアの追加ウィザードを使用してユーザーをシステム ブートによって開始された) かどうか、Serenum がポートを列挙するかどうか、コントロールにこのエントリの値を使用できます。

詳細については、シリアル ポートを設定する方法について**SkipEnumerations** Windows xp の場合、エントリの値を参照してください[Serenum のレジストリ設定](registry-settings-for-serenum.md)します。

Windows では、グローバルに、すべてのシリアル ポートの列挙を制御する 1 つのレジストリ設定はサポートされません。

Serenum には、それを列挙するシリアル ポートを開く必要があります。 ポートを開くを無期限に保持するデバイスでは、Serenum は使用しないでください。

 

 




