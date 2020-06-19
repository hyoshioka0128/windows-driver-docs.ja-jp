---
title: HMD と特殊なモニター用の EDID 拡張機能
description: HMD と特殊なモニター用の EDID 拡張機能
keywords:
- デバイスの WDK を表示する
- ドライバーの監視 WDK
- ドライバーの表示 WDK、ドライバーの監視
- monitors
- HMD
- 仮想現実
ms.author: windowsdriverdev
ms.date: 11/30/2018
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.localizationpriority: medium
ms.openlocfilehash: c97ee96359dddb76967d9dfe0e6c1577ad14bf31
ms.sourcegitcommit: 8143bb312ead6582b4b3e0ad34b6266dcfd74fb5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/18/2020
ms.locfileid: "84992486"
---
# <a name="edid-extension-vsdb-for-hmds-and-specialized-displays"></a>HMDs および特殊な表示用の EDID 拡張機能 (VSDB)

*ディスプレイの製造元の仕様*

このドキュメントでは、HMD (ヘッドマウントディスプレイ) での[EDID](https://en.wikipedia.org/wiki/Extended_Display_Identification_Data) CTA (コンシューマーテクノロジの関連付け) 拡張機能を実装する方法に関するガイダンスを提供します。また、windows が特別なディスプレイを認識できるようにし、windows OS の各レイヤーで適切に処理できるようにします。 このドキュメントでは、表示と監視という用語は同義です。

この EDID 拡張機能を使用しない場合、HMDs と特殊化された表示には次の問題があります。

* Windows デスクトップがディスプレイに拡張され、アプリを起動できるようになります。また、マウスカーソルを画面に移動できます。 ユーザーがこれを想定していない場合は、この状態から回復するのが混乱する可能性があります。
* サードパーティのコンポジターでは、HWND ベースまたは CoreWindow ベースのプレゼンテーション Api を使用する必要があります。これにより、ディスプレイへの排他アクセスは許可されません。 Windows デスクトップのコンポジターは、ウィンドウ表示 Api をディスプレイにルーティングする役割を担います。そのため、シナリオによっては、追加の非決定的な待機時間が発生することがあります。

このドキュメントの仕様で上記の問題を解決するには、次の2つの部分が必要です。

1. [EDID](https://en.wikipedia.org/wiki/Extended_Display_Identification_Data)を含むディスプレイのファームウェアは、ディスプレイの Windows 固有のユースケースを識別するために、[ベンダー固有のデータブロック](https://en.wikipedia.org/wiki/Extended_Display_Identification_Data#EIA.2FCEA-861_extension_block)を含むように変更されます。
2. Windows の表示サブシステムは、このドキュメントに記載されているベンダー固有のデータブロックを正しく認識し、表示を適切に処理します。 Windows OS のバージョンによって動作が異なる場合があることに注意してください。これについては、以下を参照してください。

1の組み合わせ。 と 2. 上記では、表示が最初に接続された時点から、正しい Windows 動作が得られます。 特に、HMDs と特定の特別な表示は通常の Windows デスクトップ環境には含まれませ[ん。また、コンポジター api を](https://docs.microsoft.com/uwp/api/windows.devices.display.core)使用したディスプレイへのアクセスは、サードパーティので使用できるようになります。

ビデオエレクトロニクス標準の関連付け (VESA) では、このドキュメントで定義されている VSDB と同様の情報へのアクセスを提供する DisplayId v2.0 の標準化されたフィールドが定義されています。  HMDs 用にこのデータを配信するには、DisplayID v2.0 以降が推奨されています。ただし、デバイスが他の理由で EDID を使用する必要がある場合は、この VSDB を使用する必要があります。

## <a name="vendor-specific-data-block-vsdb"></a>ベンダー固有データブロック (VSDB)

EDID を含むファームウェアコードを記述するパーティには、CTA 拡張ブロックが含まれている必要があります。このブロック内には、Microsoft が定義したベンダー固有のデータブロック (VSDB) が付属しています。 EDIDs の構造については、「VESA 拡張拡張ディスプレイ識別データ標準」 ([E EDID](https://vesa.org/vesa-standards/standards-summaries/)) で説明されています。「バージョン1.4、リリース A、リビジョン 2.2 2」を参照してください。  CTA extension ブロックは、CTA の861シリーズドキュメント「圧縮されていない高速デジタルインターフェイス用の DTV プロファイル」で定義されています。  VSDBs は、最新の (書き込み時の) 公開バージョンのセクション7.5.4 で説明されています。 [861 CTA](https://standards.cta.tech/kwspub/published_docs/CTA-861-G-Preview.pdf)は、他のデータブロックに対する vsdb の順序を含みます。 

VSDB 構造体には、次の表で説明されている形式と値が必要です。

![VSDB の仕様](images/specialized-displays-vsdb.png)

### <a name="vendor-specific-tag-code-3-bits"></a>ベンダー固有のタグコード [3 ビット]

このフィールドは、に設定する必要があり `0x3` ます。

### <a name="length-5-bits"></a>長さ [5 ビット]

データブロックの合計長。このバイトは含まれません。  このフィールドは、に設定する必要があり `0x15` ます。

### <a name="ieee-oui-3-bytes"></a>IEEE OUI [3 バイト]

を識別するために Microsoft に割り当てられた IEEE 組織的一意識別子 (OUI) は、、、 `0x5C` `0x12` `0xCA` の順に、バイト順に表示されます。

### <a name="version-1-byte"></a>バージョン [1 バイト]

Microsoft のコンテンツに関連付けられているバージョン番号は、ベンダー固有のデータブロックを表示します。

| 推奨されるユースケース | Version | サポートされている Windows リリース |
|----------------------|---------|---------------------------|
| HMD (VR/AR) Windows Mixed Reality エクスペリエンスで使用されるデバイスを表示する | `0x1` | Windows 10 Creator Update 以降でサポートされています |
| HMD (VR/AR) サードパーティ製のコンポジター (Windows Mixed Reality エクスペリエンス以外) で使用されるデバイスを表示します。 | `0x2` | Windows 10 10 月 2018 Update 以降でサポートされています |
| HMDs 以外の特殊なディスプレイデバイス | `0x3` | 次の Windows vNext 以降でサポートされています |

### <a name="desktop-usage-flag-1-bit"></a>デスクトップの使用状況フラグ [1 ビット]

`0x3`この VSDB のバージョン以降では、このビットはディスプレイがデスクトップに含まれる必要があるかどうかを示します。

* 表示をデスクトップの一部にする必要がある場合は、これをに設定する必要があり `0x1` ます。
* 表示がデスクトップに含まれていない場合は、これをに設定する必要があり `0x0` ます。

`0x1` `0x2` この vsdb のバージョンおよびでは、この値は常にに設定する必要があり `0x0` ます。

### <a name="third-party-usage-flag-1-bit"></a>サードパーティの使用フラグ [1 ビット]

`0x3`この VSDB のバージョン以降では、このビットは、ディスプレイがサードパーティ製のコンポジターによって使用可能であるか、または Microsoft が提供する Windows コンポジターだけを使用する必要があるかを示します。

* Windows 以外のソフトウェアコンポジターで表示を使用できるようにするには、これをに設定する必要があり `0x1` ます。
* Windows コンポジターでのみ表示を使用する場合は、これをに設定する必要があり `0x0` ます。

`0x1` `0x2` この vsdb のバージョンおよびでは、この値は常にに設定する必要があり `0x0` ます。

### <a name="display-product-primary-use-case-5-bits"></a>製品の主なユースケースを表示する [5 ビット]

ディスプレイデバイスの主なユースケースは次のとおりです。

* テスト機器-`0x1`
* 汎用表示-`0x2`
* テレビディスプレイ-`0x3`
* デスクトップ生産性の表示-`0x4`
* デスクトップゲームの表示-`0x5`
* プレゼンテーションの表示-`0x6`
* 仮想現実のヘッドセット-`0x7`
* 拡張現実-`0x8`
* ビデオの壁面ディスプレイ-`0x10`
* 医療イメージングの表示-`0x11`
* 専用ゲームの表示-`0x12`
* 専用のビデオモニターの表示-`0x13`
* アクセサリディスプレイ-`0x14`

### <a name="containerid-16-bytes"></a>ContainerID [16 バイト]

各デバイスに固有の16バイトの汎用一意識別子。 これは、ファクトリフロアで書き込まれた識別子です。 

## <a name="remarks"></a>Remarks

以前のオペレーティングシステムとの互換性を最大限に保つために、HMDs では `0x1` `0x2` この EDID 拡張機能のバージョンとを引き続き使用することをお勧めします。 HMDs に使用する値については、上記のセクションを参照してください。
