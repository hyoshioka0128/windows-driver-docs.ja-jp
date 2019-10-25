---
title: AVStream コーデックの拡張サンプル情報の記述
description: AVStream コーデックの拡張サンプル情報の記述
ms.assetid: 04447525-78f5-4c77-9a41-4e6e4729f729
keywords:
- AVStream ハードウェアコーデックサポート WDK、拡張サンプル情報
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17df3e29dead68150a4ae31539355eae380a1b7e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844191"
---
# <a name="describing-extended-sample-information-in-avstream-codecs"></a>AVStream コーデックの拡張サンプル情報の記述


デコーダーフィルターでは、extended サンプル情報が拡張された[**Ksk ストリーム\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_header)構造[**KS\_フレーム\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_frame_info)に表示されます。これは、メモリ内の ksk ストリーム\_ヘッダーに従います。

このドライバーは、KSK ストリーム\_ヘッダーで指定された情報を伝達する必要があります。入力 (ソース) から出力 (destination) KS ピンまでのオプションフラグ。

エンコーダーには拡張されたサンプル情報が含まれている必要があります拡張された KSK ストリーム\_ヘッダー構造、KS\_フレーム\_情報です。 具体的には、エンコーダーは、\_I\_FRAME および KS\_VIDEO\_フラグを示すために、メンバー **Dwframe フラグ**を更新する必要があります (該当する場合)\_P\_フレームを\_\_します。

Surface stride は、KS\_FRAME\_INFO の lSurfacePitch member (union と**Reserved1** member) で指定されています。 Surface stride の詳細については、「 [AVStream コーデックでの stride の処理](handling-stride-in-avstream-codecs.md)」を参照してください。

 

 




