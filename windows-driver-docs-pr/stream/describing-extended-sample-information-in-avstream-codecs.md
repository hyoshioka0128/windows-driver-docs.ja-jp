---
title: AVStream コーデックの拡張サンプル情報の記述
description: AVStream コーデックの拡張サンプル情報の記述
ms.assetid: 04447525-78f5-4c77-9a41-4e6e4729f729
keywords:
- AVStream ハードウェア コーデックをサポートして WDK、サンプルの詳細情報
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76148fe0ae5617f948b271213e8e87b0c7218552
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374082"
---
# <a name="describing-extended-sample-information-in-avstream-codecs"></a>AVStream コーデックの拡張サンプル情報の記述


デコーダーのフィルターでは、拡張で拡張のサンプル情報が見つかります[ **KSSTREAM\_ヘッダー** ](https://msdn.microsoft.com/library/windows/hardware/ff567138)構造[ **KS\_フレーム\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff567645)、KSSTREAM に従う\_メモリ内のヘッダー。

ドライバーは KSSTREAM で指定された情報を伝達する必要があります\_ヘッダー。出力 (宛先) KS ピンへの入力 (ソース) から OptionsFlags します。

エンコーダーは、拡張 KSSTREAM で拡張のサンプル情報を含める必要があります\_ヘッダー構造、KS\_フレーム\_情報。 具体的には、エンコーダーは、メンバーを更新する必要があります**dwFrameFlags** KS を示す\_ビデオ\_フラグ\_は\_フレームと KS\_ビデオ\_フラグ\_P\_フレーム、該当するものです。

Stride のサーフェスが KS で指定された\_フレーム\_情報の lSurfacePitch メンバー (を含む共用体**Reserved1**メンバー)。 Stride のサーフェスの詳細については、次を参照してください。 [AVStream コーデックで Stride 処理](handling-stride-in-avstream-codecs.md)します。

 

 




