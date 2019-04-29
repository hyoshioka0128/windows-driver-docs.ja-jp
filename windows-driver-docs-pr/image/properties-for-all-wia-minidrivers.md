---
title: すべての WIA ミニドライバーのプロパティ
description: すべての WIA ミニドライバーのプロパティ
ms.assetid: ba85dbbd-2333-4f4f-b12a-84985773eef6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f38043b8fabc7c914a86a76ffc93934d612fbd88
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392619"
---
# <a name="properties-for-all-wia-minidrivers"></a>すべての WIA ミニドライバーのプロパティ





### <a name="required-properties-on-root-or-child-items"></a>ルートまたは子項目に必要なプロパティ

WIA サービスには、次のプロパティが用意されています。

[**WIA\_IPA\_完全\_項目\_名**](https://msdn.microsoft.com/library/windows/hardware/ff551561)

[**WIA\_IPA\_項目\_フラグ**](https://msdn.microsoft.com/library/windows/hardware/ff551585)

[**WIA\_IPA\_項目\_名**](https://msdn.microsoft.com/library/windows/hardware/ff551590)

[**WIA\_IPA\_項目\_カテゴリ**](https://msdn.microsoft.com/library/windows/hardware/ff551581)

WIA ミニドライバーには、次のプロパティが用意されています。

[**WIA\_IPA\_アクセス\_権限**](https://msdn.microsoft.com/library/windows/hardware/ff551518)

### <a name="required-properties-on-root-items"></a>ルート項目に対して必要なプロパティ

WIA サービスには、次のルート項目のプロパティが用意されています。

[**WIA\_DIP\_BAUDRATE**](https://msdn.microsoft.com/library/windows/hardware/ff550244)

[**WIA\_DIP\_DEV\_DESC**](https://msdn.microsoft.com/library/windows/hardware/ff550247)

[**WIA\_DIP\_DEV\_ID**](https://msdn.microsoft.com/library/windows/hardware/ff550250)

[**WIA\_DIP\_DEV\_名**](https://msdn.microsoft.com/library/windows/hardware/ff550256)

[**WIA\_DIP\_DEV\_型**](https://msdn.microsoft.com/library/windows/hardware/ff550260)

[**WIA\_DIP\_ドライバー\_バージョン**](https://msdn.microsoft.com/library/windows/hardware/ff550263)

[**WIA\_DIP\_HW\_構成**](https://msdn.microsoft.com/library/windows/hardware/ff550268)

[**WIA\_DIP\_ポート\_名**](https://msdn.microsoft.com/library/windows/hardware/ff550278)

[**WIA\_DIP\_リモート\_DEV\_ID**](https://msdn.microsoft.com/library/windows/hardware/ff550282)

[**WIA\_DIP\_SERVER\_名**](https://msdn.microsoft.com/library/windows/hardware/ff550285)

[**WIA\_DIP\_STI\_GEN\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff550288)

[**WIA\_DIP\_UI\_CLSID**](https://msdn.microsoft.com/library/windows/hardware/ff550291)

[**WIA\_DIP\_VEND\_DESC**](https://msdn.microsoft.com/library/windows/hardware/ff550293)

[**WIA\_DIP\_WIA\_バージョン**](https://msdn.microsoft.com/library/windows/hardware/ff550296)

### <a name="optional-properties-on-root-items"></a>省略可能なプロパティでルート項目

WIA ミニドライバーは、ルート項目では、次の省略可能なプロパティを提供します。

[**WIA\_DPA\_CONNECT\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff550299)

[**WIA\_DPA\_デバイス\_時間**](https://msdn.microsoft.com/library/windows/hardware/ff550303)

[**WIA\_DPA\_ファームウェア\_バージョン**](https://msdn.microsoft.com/library/windows/hardware/ff550309)

### <a name="required-properties-on-child-items-able-to-transfer-data"></a>子項目のデータを転送することが必要なプロパティ

WIA サービスには、子項目では、次のプロパティが用意されています。

[**WIA\_IPA\_ICM\_PROFILE\_NAME**](https://msdn.microsoft.com/library/windows/hardware/ff551571)

WIA ミニドライバーには、次のプロパティを子項目が用意されています。

[**WIA\_IPA\_ビット\_1 秒あたり\_チャネル**](https://msdn.microsoft.com/library/windows/hardware/ff551526)

[**WIA\_IPA\_バッファー\_サイズ**](https://msdn.microsoft.com/library/windows/hardware/ff551527)

[**WIA\_IPA\_バイト\_1 秒あたり\_行**](https://msdn.microsoft.com/library/windows/hardware/ff551531)

[**WIA\_IPA\_チャネル\_1 秒あたり\_ピクセル**](https://msdn.microsoft.com/library/windows/hardware/ff551535)

[**WIA\_IPA\_圧縮**](https://msdn.microsoft.com/library/windows/hardware/ff551540)

[**WIA\_IPA\_データ型**](https://msdn.microsoft.com/library/windows/hardware/ff551543)

[**WIA\_IPA\_深さ**](https://msdn.microsoft.com/library/windows/hardware/ff551546)

[**WIA\_IPA\_FILENAME\_拡張機能**](https://msdn.microsoft.com/library/windows/hardware/ff551549)

[**WIA\_IPA\_形式**](https://msdn.microsoft.com/library/windows/hardware/ff551553)

[**WIA\_IPA\_項目\_サイズ**](https://msdn.microsoft.com/library/windows/hardware/ff551594)

[**WIA\_IPA\_数\_の\_行**](https://msdn.microsoft.com/library/windows/hardware/ff551611)

[**WIA\_IPA\_ピクセル\_1 秒あたり\_行**](https://msdn.microsoft.com/library/windows/hardware/ff551615)

[**WIA\_IPA\_平面**](https://msdn.microsoft.com/library/windows/hardware/ff551617)

[**WIA\_IPA\_優先\_形式**](https://msdn.microsoft.com/library/windows/hardware/ff551623)

[**WIA\_IPA\_TYMED**](https://msdn.microsoft.com/library/windows/hardware/ff551656)

### <a name="optional-properties-on-child-items-able-to-transfer-data"></a>子項目のデータを転送することで、省略可能なプロパティ

WIA ミニドライバーは、次のプロパティを提供します。

[**WIA\_IPA\_アプリ\_色\_マッピング**](https://msdn.microsoft.com/library/windows/hardware/ff551521)

[**WIA\_IPA\_色\_プロファイル**](https://msdn.microsoft.com/library/windows/hardware/ff551536)

[**WIA\_IPA\_ガンマ\_曲線**](https://msdn.microsoft.com/library/windows/hardware/ff551568)

[**WIA\_IPA\_項目\_時間**](https://msdn.microsoft.com/library/windows/hardware/ff551601)

[**WIA\_IPA\_PROP\_STREAM\_COMPAT\_ID**](https://msdn.microsoft.com/library/windows/hardware/ff551628)

[**WIA\_IPA\_リージョン\_型**](https://msdn.microsoft.com/library/windows/hardware/ff551646)

[**WIA\_IPA\_抑制\_プロパティ\_ページ**](https://msdn.microsoft.com/library/windows/hardware/ff551653)

 

 




