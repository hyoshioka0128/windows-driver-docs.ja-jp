---
title: WIA データ項目
description: WIA データ項目
ms.assetid: 3ce01393-4a0b-4b70-8087-abe989aa00a9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a3da29a7fcd005bf354f9ded4185c81962b803d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354864"
---
# <a name="wia-data-item"></a>WIA データ項目





このトピックには、Windows Vista 以降が適用されます。

データ転送に使用できる任意の項目は、データ項目と見なされます。 これに付いている項目が含まれています、 **WiaItemTypeProgrammableDataSource**フラグ。 マークされた任意の項目、 **WiaItemTypeTransfer**フラグは、データを転送する機能を公開できます。 このフラグを設定して、任意の項目は、次の WIA プロパティを提供する必要があります。

[**WIA\_IPA\_アクセス\_権限**](https://msdn.microsoft.com/library/windows/hardware/ff551518)

[**WIA\_IPA\_項目\_サイズ**](https://msdn.microsoft.com/library/windows/hardware/ff551594)

[**WIA\_IPA\_バッファー\_サイズ**](https://msdn.microsoft.com/library/windows/hardware/ff551527)

[**WIA\_IPA\_形式**](https://msdn.microsoft.com/library/windows/hardware/ff551553)

[**WIA\_IPA\_優先\_形式**](https://msdn.microsoft.com/library/windows/hardware/ff551623)

[**WIA\_IPA\_TYMED**](https://msdn.microsoft.com/library/windows/hardware/ff551656)

[**WIA\_IPA\_FILENAME\_拡張機能**](https://msdn.microsoft.com/library/windows/hardware/ff551549)

プログラミング可能なデータ ソースでマークされた項目、 **WiaItemTypeTransfer**フラグは、これらの WIA プロパティを指定する必要があります。 たとえば、フラット ベッド スキャナーの項目には、これらのプロパティを適切にデータ転送を構成する必要があります。

WIA データ項目は項目のフラグの設定に応じて他のプロパティがあります。 たとえば、WIA 項目が付いて、 **WiaItemTypeImage**フラグでは、イメージに固有の情報のプロパティをなどが必要[ **WIA\_IPA\_深さ**](https://msdn.microsoft.com/library/windows/hardware/ff551546)と[ **WIA\_IPA\_数\_の\_行**](https://msdn.microsoft.com/library/windows/hardware/ff551611)します。

 

 




