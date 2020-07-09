---
title: KSK プロパティ \_ CAMERACONTROL \_ EXTENDED OPTIMIZATIONHINT (拡張された \_ ハードウェア最適化)
description: KSK プロパティ \_ CAMERACONTROL \_ EXTENDED \_ OPTIMIZATIONHINT は、フォトキャプチャとビデオキャプチャの主なユースケースを制御するために使用されます。 Windows 10 では、このコントロールは拡張されたハードウェア最適化ヒントをサポートするように拡張されています。
ms.assetid: 1E2787B7-4BC2-4FBC-8909-ACB122B87F08
keywords:
- ストリーミングメディアデバイスの KSPROPERTY_CAMERACONTROL_EXTENDED_OPTIMIZATIONHINT
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_OPTIMIZATIONHINT
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 07/08/2020
ms.localizationpriority: medium
ms.openlocfilehash: 8238b07a8fc7936184becb5bca2202d86fde6e81
ms.sourcegitcommit: 8b6d83bcedea8c872ec8c7df874344421a39dd57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86128859"
---
# <a name="ksproperty_cameracontrol_extended_optimizationhint-expanded-hardware-optimization"></a>KSK プロパティ \_ CAMERACONTROL \_ EXTENDED OPTIMIZATIONHINT (拡張された \_ ハードウェア最適化)

KSK プロパティ \_ CAMERACONTROL \_ EXTENDED \_ OPTIMIZATIONHINT は、フォトキャプチャとビデオキャプチャの主なユースケースを制御するために使用されます。 Windows 10 では、このコントロールは拡張されたハードウェア最適化ヒントをサポートするように拡張されています。

## <a name="usage-summary-table"></a>使用状況の概要テーブル

| スコープ | Control | Type |
|--|--|--|
| Version 1 | フィルター | 同期 |

次のフラグは、KSCAMERA \_ extendedprop ヘッダーに配置でき \_ ます。ドライバーのハードウェア最適化ヒントにフラグを入力します。

```cpp
#define KSCAMERA_EXTENDEDPROP_OPTIMIZATION_DEFAULT      0x0000000000000000
#define KSCAMERA_EXTENDEDPROP_OPTIMIZATION_PHOTO        0x0000000000000001
#define KSCAMERA_EXTENDEDPROP_OPTIMIZATION_VIDEO        0x0000000000000002
#define KSCAMERA_EXTENDEDPROP_OPTIMIZATION_QUALITY      0x0000000000000004
#define KSCAMERA_EXTENDEDPROP_OPTIMIZATION_LATENCY      0x0000000000000008
#define KSCAMERA_EXTENDEDPROP_OPTIMIZATION_POWER        0x0000000000000010
```

写真とビデオのヒントは、主なユースケースを指定するために引き続き使用されます。

Windows 10 では、追加のビットフラグによって、ドライバーの品質、速度、電力消費のトレードオフを支援します。 既定では、ドライバーは KSCAMERA extendedprop 最適化の写真を持っている必要があり \_ \_ \_ ます。

ドライバーがこのコントロールをサポートしている場合は、KSCAMERA \_ extendedprop の \_ 最適化 \_ の写真と KSCAMERA \_ extendedprop の \_ 最適化ビデオをサポートする必要があり \_ ます。

ドライバーが最適化ヒントをサポートしていない場合、ドライバーはこのコントロールを実装しません。

次の表では、フラグ機能について説明します。

| フラグ | 説明 |
|--|--|
| KSCAMERA_EXTENDEDPROP_OPTIMIZATION_DEFAULT | これは必須の機能です。 指定した場合、ドライバーは以前にドライバーで設定されたヒントをクリアし、ドライバーの既定の電力、品質、待機時間のトレードオフを適用します。 |
| KSCAMERA_EXTENDEDPROP_OPTIMIZATION_PHOTO | これは必須の機能です。 指定されている場合、主なユースケースは写真キャプチャで、ドライバーはビデオ記録の写真キャプチャに優先順位を付ける必要があります。 このフラグは、プレビューの pin が [停止] 状態になっているときに、写真の品質を優先するセンサーモードを選択する場合、またはビデオ記録中の写真キャプチャの [実行中] 状態の場合に指定できます。 ビデオ記録中に写真キャプチャに指定した場合、ビデオストリームのエラーは、写真の品質向上のために許容されます。 このフラグは、ビデオフラグと同時には使用できません。このフラグは、1つまたは2つの品質、待機時間、および電源フラグと共に使用できます。 |
| KSCAMERA_EXTENDEDPROP_OPTIMIZATION_VIDEO | これは必須の機能です。 指定されている場合、主なユースケースはビデオキャプチャで、ドライバーは写真キャプチャに対するビデオ記録の優先順位を決定します。 このフラグは、プレビューの pin が [停止] 状態になっているときに、ビデオ記録を優先するセンサーモードを選択する場合、またはビデオ記録中の写真キャプチャの [実行中] 状態の場合に指定できます。 ビデオ記録中に写真キャプチャに指定した場合、ビデオストリームのエラーは許可されません。 このフラグは、写真フラグと同時に指定することはできません。また、1つまたは2つの品質、待機時間、および電源フラグと共に使用できます。 |
| KSCAMERA_EXTENDEDPROP_OPTIMIZATION_QUALITY | この機能は省略可能です。 指定した場合、ドライバーは写真キャプチャのイメージ品質とビデオ記録のビデオ品質を最適化する必要があります。 このフラグは、フォトキャプチャ (通常の写真、VPS、および履歴フレームのない PS を含む) やビデオ記録の開始前、または pin が停止状態のときに指定できます。 このフラグは、PHOTO フラグと共に使用することも、ビデオフラグと共に待機時間や電源フラグと共に使用することもできます。 |
| KSCAMERA_EXTENDEDPROP_OPTIMIZATION_LATENCY | この機能は省略可能です。 指定した場合、ドライバーは写真キャプチャとビデオ記録の速度と待機時間を最適化する必要があります。 このフラグは、フォトキャプチャ (通常の写真、VPS、および履歴フレームのない PS を含む) 施しビデオ記録を開始する前、または pin が停止状態のときに指定できます。 このフラグは、PHOTO フラグと共に使用することも、ビデオフラグと共に品質または電源フラグと共に使用することもできます。 |
| KSCAMERA_EXTENDEDPROP_OPTIMIZATION_POWER | この機能は省略可能です。 指定した場合、ドライバーは写真キャプチャとビデオ記録の電力消費を最適化する必要があります。 このフラグは、フォトキャプチャ (通常の写真、VPS、および、履歴のない PS を含む) やビデオ記録の開始前に指定することも、pin が stopped 状態のときに指定することもできます。 このフラグは、ビデオフラグと共に、品質または待機時間フラグと共に使用できます。 |

次の表に、コントロールを使用する場合の[**KSCAMERA \_ extendedprop \_ ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)構造のフィールドの説明と要件を示します。

| メンバー | 値 |
|--|--|
| Version | 1 |
| PinId | KSCAMERA_EXTENDEDPROP_FILTERSCOPE (0xFFFFFFFF) |
| サイズ | sizeof (KSCAMERA_EXTENDEDPROP_HEADER) + sizeof (KSCAMERA_EXTENDEDPROP_VALUE) |
| 結果 | 最後の設定操作のエラー結果を示します。 設定操作が行われていない場合は、0にする必要があります。 |
| 機能 | は、前述のように、サポートされている KSCAMERA_EXTENDEDPROP_OPTIMIZATION_ * フラグのビットごとの OR である必要があります。 |
| フラグ | これは、読み取り/書き込みフィールドです。 これは、上記で定義されている、サポートされている KSCAMERA_EXTENDEDPROP_OPTIMIZATION_ * フラグの有効な組み合わせにすることができます。 |

## <a name="remarks"></a>解説

最適化ヒントを使用する場合は、次の項目に注意してください。

- 品質/待機時間/電力と写真/ビデオは、独立したヒントの2つのセットです。 同時に指定することも、別々の時刻に個別に指定することもできます。 品質/待機時間/電力を設定しても、写真やビデオは上書きされません。 別の時刻に指定した場合、ドライバーは GET 呼び出しで両方のヒントセットの現在の設定を返します。

- 品質/待機時間/電源については、ヒントが設定されている場合、ドライバーは制約内で最適化する必要があります。 最適化が使用できない場合、ドライバーはヒントを無視する必要があります。

- ビデオのユースケースに対して2つのヒントを同時に指定すると、ヒントを1つだけ指定した場合よりも、各ヒントの最適化が小さくなることがあります。 具体的には次のとおりです。

  - 品質またはパワーも指定されている場合、待機時間は品質またはパワーよりも優先されます。 このような場合、品質が指定されている場合よりも品質が低下する可能性があります。電力消費量は、[電源のみ] を指定した場合よりも高くなる可能性があります。

  - 品質と電力の両方が指定されている場合、品質が指定されている場合よりも品質が低下する可能性があります。電力消費量は、[電力] を指定した場合よりも高くなる可能性があります。

- 最適化ヒントは、アプリケーションで指定されたキャプチャシナリオの制約内で、3A、ISP 処理、センサー選択などの処理のトレードオフを容易にするために、ドライバーへのヒントとしてのみ提供されます。 アプリ開発者は、最適な結果を得るために、特定のキャプチャシナリオに最も適したコントロールと Api を選択して構成することが重要です。 そうしないと、最適化ヒントだけが効果が低下する可能性があります。 たとえば、高品質の写真キャプチャの場合、品質ヒントを利用するために、特定の IHV プラットフォームでは PS の代わりに VPS または LowLagPhoto/の写真を使用する必要があります。 同様に、待機時間が短く、電力消費が必要な場合は、ビデオ安定化を無効にする必要があります。

- 最適化ヒントは、各機能フラグの下で指定されている以外の時刻/状態で受信した場合は無視する必要があります。

ドライバーでビデオ安定化制御が有効になっている場合 (または自動):

- このドライバーは、待機時間の短いビデオ安定化アルゴリズムや、待ち時間や電源ヒントが設定されている場合の処理待機時間や電力消費量を減らすための、低待機時間または低電力ビデオ安定化アルゴリズムを含む、最も積極的なビデオ安定化を適用できます。 ビデオの安定化が [自動] に設定されている場合、ドライバーは、待ち時間や電力消費量をさらに削減するために、ビデオ安定化を無効にすることがあります。

- 品質に関するヒントが設定されている場合、ドライバーは、最大のアグレッシブなビデオ安定化を適用して、ビデオ品質を向上させることができます。

## <a name="requirements"></a>必要条件

**ヘッダー:** Ksmedia .h (Ksk を含む)
