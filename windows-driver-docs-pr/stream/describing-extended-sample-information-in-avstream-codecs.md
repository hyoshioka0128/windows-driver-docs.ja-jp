---
title: AVStream コーデックの拡張サンプル情報の記述
description: AVStream コーデックの拡張サンプル情報の記述
ms.assetid: 04447525-78f5-4c77-9a41-4e6e4729f729
keywords:
- AVStream ハードウェア コーデックをサポートして WDK、サンプルの詳細情報
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 87353cffc6772acf60dab9932edc0495d47c0d3e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353253"
---
# <a name="describing-extended-sample-information-in-avstream-codecs"></a>AVStream コーデックの拡張サンプル情報の記述


デコーダーのフィルターでは、拡張で拡張のサンプル情報が見つかります[ **KSSTREAM\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksstream_header)構造[ **KS\_フレーム\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagks_frame_info)、KSSTREAM に従う\_メモリ内のヘッダー。

ドライバーは KSSTREAM で指定された情報を伝達する必要があります\_ヘッダー。出力 (宛先) KS ピンへの入力 (ソース) から OptionsFlags します。

エンコーダーは、拡張 KSSTREAM で拡張のサンプル情報を含める必要があります\_ヘッダー構造、KS\_フレーム\_情報。 具体的には、エンコーダーは、メンバーを更新する必要があります**dwFrameFlags** KS を示す\_ビデオ\_フラグ\_は\_フレームと KS\_ビデオ\_フラグ\_P\_フレーム、該当するものです。

Stride のサーフェスが KS で指定された\_フレーム\_情報の lSurfacePitch メンバー (を含む共用体**Reserved1**メンバー)。 Stride のサーフェスの詳細については、次を参照してください。 [AVStream コーデックで Stride 処理](handling-stride-in-avstream-codecs.md)します。

 

 




