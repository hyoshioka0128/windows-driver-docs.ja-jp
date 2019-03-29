---
title: さまざまな地理的な地域向けにファームウェアをカスタマイズする
description: システムは、世界中のさまざまな市場や地域で販売できるは。 これを有効にするには、Oem は、リージョン固有のファームウェアが必要とするこれらのデバイス/システム ファームウェアの一意の GUID 値を定義する必要があります。
ms.assetid: 47E1C9EC-ED6E-4626-B61F-A19D1546FA08
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9cc960e400fa4ecc40af77cc28ecd8e34b41ba53
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571056"
---
# <a name="customizing-firmware-for-different-geographic-regions"></a>さまざまな地理的な地域向けにファームウェアをカスタマイズする


システムは、世界中のさまざまな市場や地域で販売できるは。 これを有効にするには、Oem は、リージョン固有のファームウェアが必要とするこれらのデバイス/システム ファームウェアの一意の GUID 値を定義する必要があります。

たとえば、リージョン固有のファームウェアはモバイル ブロード バンド (MBB) デバイスを頻繁に必要です。 MBB デバイスのファームウェアは、、特定モバイル ネットワーク オペレーター (MNO)、特定のリージョンでローカル MNO および政府の規制を遵守する多くの場合、カスタマイズします。 このようなデバイスにファームウェアのターゲット設定できるように、OEM 割り当てる必要がありますの一意の GUID、ESRT でそのデバイスに製造時にします。

![さまざまな地理的なロケールに向けて 2 つのハードウェアと同じ soc システム](images/socsfordifferentlocales.png)

前の図で、システムが、システムが異なる地理的環境に再販の宛先が例外をすべての点では、同じことに注意してください。 そのため、各システムに MBB デバイスのファームウェアでは、個別に不要である必要があり、ESRT で異なる GUID が割り当てられます。 これにより、ファームウェア更新プログラムのターゲットは、それらにより、運用の地域で販売システムに MNO できます。 Geography、または再販するチャネルによってカスタム ファームウェアが必要とするすべてのデバイスのような考慮事項を指定する必要があります。

## <a name="related-topics"></a>関連トピック
[ファームウェアのドライバー パッケージを使用してシステムとデバイスのファームウェア更新プログラム](system-and-device-firmware-updates-via-a-firmware-driver-package.md)  
[ESRT テーブルの作成](populating-the-esrt-table.md)  
[ファームウェアの更新プログラム パッケージの作成](authoring-a-firmware-update-package.md)  
[認定と更新プログラム パッケージの署名](certifying-and-signing-the-update-package.md)  
[更新プログラムのインストール](installing-the-update.md)  



