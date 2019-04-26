---
title: 多機能 PC カード デバイスのサポート
description: 多機能 PC カード デバイスのサポート
ms.assetid: 4da3b99c-0731-41b5-9f67-29c7e181342f
keywords:
- 多機能デバイス WDK、PC カード
- PC カード多機能標準 WDK
- リソース マップ WDK 多機能デバイス
- 16 ビット PC カード多機能デバイス WDK
- 構成は、WDK の多機能デバイスを登録します。
- WDK の多機能デバイスを登録します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b33988d24ad7fd53dc3c620d7187a676a70ca1cf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342342"
---
# <a name="supporting-multifunction-pc-card-devices"></a>多機能 PC カード デバイスのサポート





PC カード多機能標準では、多機能デバイスにある各関数の属性のメモリでレジスタのセットを指定します。 これらのレジスタは、たとえば、各関数を個別に有効にし、各関数にのみ含まれている範囲の I/O リソースを定義する PCMCIA バス ドライバーを許可します。 標準では、多機能デバイスが含まれている、属性のメモリ内の各レジスタのセットのアドレスにはも指定します。 これらのアドレスは、プログラムの構成のレジスタに PCMCIA バス ドライバーを有効にします。

16 ビット PC カード デバイス、PC カード多機能標準を完全に実装して、このようなデバイスの製造元を確実にデバイスとドライバーの INF の最小要件が正しく場合、は、NT ベースのシステムで正しく構成されます。 参照してください[をサポートしている PC カードに準拠している多機能標準](supporting-pc-cards-that-conform-to-the-multifunction-standard.md)詳細についてはします。

16 ビット PC カードのデバイスが、PC カード多機能標準が完全に実装しない場合、ベンダーは、INF ファイルの不足情報を提供する必要があります。 多機能 PC カード デバイスは、多機能の標準を実装するために障害が発生する 2 つの方法はあります。

1.  デバイスは、関数ごとの多機能構成レジスタのセットを実装が、その属性のメモリでのレジスタのセットはすべての場所が含まれていません。

2.  デバイスは、関数ごとの多機能構成レジスタのセットを実装していません。

デバイスの INF に必要な情報がある場合、デバイスに前述の制限事項がある場合は、PCMCIA バス ドライバーでは構成レジスタをプログラミングできます*DDInstall*.**LogConfigOverride**セクション。 詳細については、次のセクションを参照してください。

[不完全な構成を持つ PC カードのサポートがアドレスを登録します。](supporting-pc-cards-that-have-incomplete-configuration-register-addres.md)

[不完全な構成を持つ PC カードのサポートを登録します](supporting-pc-cards-that-have-incomplete-configuration-registers.md)

PCI 多機能規則は、基本的に Cardbus デバイスに従います。 参照してください[多機能 PCI デバイスをサポートしている](supporting-multifunction-pci-devices.md)します。

 

 




