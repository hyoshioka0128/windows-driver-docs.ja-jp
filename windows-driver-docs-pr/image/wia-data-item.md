---
title: WIA データ項目
description: WIA データ項目
ms.assetid: 3ce01393-4a0b-4b70-8087-abe989aa00a9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 73119df2bb7643da3501d70cba548b556e67c6d0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375354"
---
# <a name="wia-data-item"></a>WIA データ項目





このトピックには、Windows Vista 以降が適用されます。

データ転送に使用できる任意の項目は、データ項目と見なされます。 これに付いている項目が含まれています、 **WiaItemTypeProgrammableDataSource**フラグ。 マークされた任意の項目、 **WiaItemTypeTransfer**フラグは、データを転送する機能を公開できます。 このフラグを設定して、任意の項目は、次の WIA プロパティを提供する必要があります。

[**WIA\_IPA\_アクセス\_権限**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-access-rights)

[**WIA\_IPA\_項目\_サイズ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-item-size)

[**WIA\_IPA\_バッファー\_サイズ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-buffer-size)

[**WIA\_IPA\_形式**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-format)

[**WIA\_IPA\_優先\_形式**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-preferred-format)

[**WIA\_IPA\_TYMED**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-tymed)

[**WIA\_IPA\_FILENAME\_拡張機能**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-filename-extension)

プログラミング可能なデータ ソースでマークされた項目、 **WiaItemTypeTransfer**フラグは、これらの WIA プロパティを指定する必要があります。 たとえば、フラット ベッド スキャナーの項目には、これらのプロパティを適切にデータ転送を構成する必要があります。

WIA データ項目は項目のフラグの設定に応じて他のプロパティがあります。 たとえば、WIA 項目が付いて、 **WiaItemTypeImage**フラグでは、イメージに固有の情報のプロパティをなどが必要[ **WIA\_IPA\_深さ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-depth)と[ **WIA\_IPA\_数\_の\_行**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-number-of-lines)します。

 

 




