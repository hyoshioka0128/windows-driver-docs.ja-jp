---
title: デバイス セットアップ クラスの概要
description: デバイス セットアップ クラスの概要
ms.assetid: 318ec3f4-f2c2-437c-a767-494ac240cb89
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 433dec1ec7f9de7b0113e04bdeabdce8472be9db
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330233"
---
# <a name="overview-of-device-setup-classes"></a>デバイス セットアップ クラスの概要


デバイスのインストールを容易に設定され、同じ方法で構成されているデバイスは、デバイス セットアップ クラスに分類されます。 たとえば、メディア チェンジャーの SCSI デバイスが MediumChanger デバイス セットアップ クラスにグループ化されます。 デバイス セットアップ クラスは、デバイスのインストールで、クラスのインストーラーと関連するクラス co-installer を定義します。

Microsoft では、ほとんどのデバイス セットアップ クラスを定義します。 Ihv と Oem は、新しいデバイス セットアップ クラスを定義できますが、場合にのみ、既存のクラスが適用されます。 たとえば、カメラの製造元は、カメラ イメージのセットアップ クラスに分類するために、新しいセットアップ クラスを定義するはありません。 同様に、無停電電源装置 (UPS) は、バッテリ クラスに該当します。

各デバイス セットアップ クラスに関連付けられている GUID があります。 システム定義のセットアップ クラス Guid がで定義されている*Devguid.h*フォーム GUID_DEVCLASS_ のシンボル名は、通常に*Xxx*します。

デバイス セットアップ クラス GUID を定義、 **.\\CurrentControlSet\\コントロール\\クラス\\**<em>ClassGuid</em>レジストリ キーを標準的なセットアップの特定のデバイスの新しいサブキーを作成するにはクラス。

 

 





