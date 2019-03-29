---
title: HMD と特殊なモニター用の EDID 拡張機能
description: HMD と特殊なモニター用の EDID 拡張機能
keywords:
- WDK のデバイスを表示します。
- ドライバー WDK を監視します。
- ディスプレイ ドライバー WDK、モニターのドライバー
- モニタ
- HMD
- 仮想現実
ms.author: windowsdriverdev
ms.date: 11/30/2018
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.localizationpriority: medium
ms.openlocfilehash: b3d0009724a22ad2aceb221c4dc99d89c21e8bc4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571737"
---
# <a name="edid-extension-vsdb-for-hmds-and-specialized-displays"></a>EDID 拡張機能 (VSDB) HMDs し、特殊な表示

*表示の製造元の仕様*

実装する方法のガイダンスを提供する[EDID](https://en.wikipedia.org/wiki/Extended_Display_Identification_Data) CTA (コンシューマー Technology Association) 拡張機能 (ヘッドを表示するマウント) ッドマウントまたはにより、Windows がディスプレイを特別なとして認識する特殊な表示ファームウェアそれらを正しく処理する Windows OS で各レイヤーを有効にするためです。 このドキュメントの条項を表示し、モニターは同義です。

この EDID 拡張子のない HMDs と特殊な表示は次の問題があります。

* Windows デスクトップを拡張して、表示には、上に、アプリを起動できますおよび表示上にマウス カーソルを移動できます。 この想定していないユーザー場合、は、この状態から回復すると混乱ができます。
* サード パーティ製のコンポジターには、HWND ベースまたは CoreWindow ベースのプレゼンテーション表示への排他的アクセスを許可しない Api を使用する必要があります。 Windows デスクトップ コンポジターは一部のシナリオで確定的な余分な待機時間が発生すると、表示するウィンドウ プレゼンテーション Api ルーティングします。

2 つの部分は、上記の問題を解決するには、このドキュメントで指定の必要があります。

1. 保持するディスプレイのファームウェア、 [EDID](https://en.wikipedia.org/wiki/Extended_Display_Identification_Data)を格納する変更は、[ベンダー固有のデータ ブロック](https://en.wikipedia.org/wiki/Extended_Display_Identification_Data#EIA.2FCEA-861_extension_block)ディスプレイの Windows に固有のユース ケースを特定します。
2. Windows のディスプレイ サブシステムは正しくこのドキュメントに記載されているベンダー固有のデータ ブロックを認識し、ディスプレイを適切に処理します。 異なるバージョンの Windows OS のさまざまな動作は、下に列記場合があることに注意してください。

1 の組み合わせ。 2 つです。 上記の動作が発生、正しい Windows でディスプレイが接続されている最初の瞬間から。 具体的には、HMDs と特定の特殊な表示は含まれません、標準の Windows デスクトップ環境とで、ディスプレイへのアクセスで、 [Windows.Devices.Display.Core](https://docs.microsoft.com/en-us/uwp/api/windows.devices.display.core) Api はサード パーティで使用できるようになりますコンポジターです。

ビデオ Electronics Standards Association (VESA) には、このドキュメントで定義されている VSDB と同様の情報へのアクセスを提供する DisplayId v2.0 で標準化されたフィールドが定義します。  DisplayID v2.0 またはそれ以降は HMDs のデータの実現に推奨されるメカニズムが、デバイスは、他の理由から、EDID を使用する必要がある場合は、この VSDB を使用する必要があります。

## <a name="vendor-specific-data-block-vsdb"></a>ベンダー固有のデータ ブロック (VSDB)

EDID を含むファームウェア コードの作成を担当のパーティは、CTA 拡張機能のブロックを含めるし、そのブロック内で、マイクロソフトによって定義されたベンダー固有のデータ ブロック (VSDB) を配置する必要があります。 Standard では、"VESA 拡張拡張表示識別データ"EDIDs の構造が説明されている ([E EDID](https://www.vesa.org/vesa-standards/standards-summaries/))、version 1.4、release A を 2 にリビジョン セクション 2.2 の記述の拡張機能要素を参照してください。  CTA 拡張機能のブロックは、CTA の 861 シリーズ ドキュメント「するデジタル テレビのプロファイルの圧縮されていない高速デジタル インターフェイス」で定義されます。  7.5.4 (記事の執筆時) の最新版の公開されたバージョンでは、VSDBs が説明されている[CTA-g 861](https://standards.cta.tech/kwspub/published_docs/CTA-861-G-Preview.pdf)などその他のデータ ブロックを基準と VSDB の順序。 

VSDB 構造体は、形式と、次の表に記載されている値が必要です。

![VSDB 仕様](images/specialized-displays-vsdb.png)

### <a name="vendor-specific-tag-code-3-bits"></a>ベンダー固有のタグ コード [3 ビット]

このフィールドを設定する必要があります`0x3`します。

### <a name="length-5-bits"></a>長さ [5 ビット]

このバイトを含まない、データ ブロックの長さの合計。  このフィールドを設定する必要があります`0x15`します。

### <a name="ieee-oui-3-bytes"></a>IEEE OUI [3 バイト]

IEEE 組織的一意識別子 (OUI) が表示されますを識別するため、Microsoft に割り当てられている: `0x5C`、 `0x12`、 `0xCA`、シーケンシャル バイト順でします。

### <a name="version-1-byte"></a>バージョン [1 バイト]

Microsoft 表示のベンダー固有のデータ ブロックの内容に関連付けられているバージョン番号です。

| 推奨されるユース ケース | バージョン | サポートされている Windows のリリース |
|----------------------|---------|---------------------------|
| Windows Mixed Reality によって使用されるッドマウント (VR/AR) のディスプレイ デバイス エクスペリエンスします。 | `0x1` | Windows 10 Creators Update 以降でサポート |
| ッドマウント (VR/AR) (Windows Mixed Reality エクスペリエンス) 以外のサード パーティ製コンポジターで使用されるデバイスを表示します。 | `0x2` | Windows でサポートされている 10 年 2018年 10 月の更新以降 |
| HMDs ではない特殊な表示デバイス | `0x3` | 以降では、次の Windows vNext のサポート |

### <a name="desktop-usage-flag-1-bit"></a>デスクトップの使用法フラグ 1 のビット

バージョン `0x3`を示し、上のこの VSDB では、このビット ディスプレイがデスクトップの一部にするかどうか。

* これに設定する場合は、表示は、デスクトップの一部にする必要があります、`0x1`します。
* これに設定する場合は、表示はデスクトップの一部をすることはできません、`0x0`します。

バージョンで`0x1`と`0x2`VSDB このは、この値に設定が常に`0x0`します。

### <a name="third-party-usage-flag-1-bit"></a>サード パーティの使用法フラグ 1 のビット

バージョン `0x3`を示し、上のこの VSDB では、このビット ディスプレイをサード パーティ製のコンポジター、または Microsoft 提供の Windows コンポジターのみで使用可能にするかどうか。

* これに設定する場合は、表示は、Windows 以外のソフトウェアのコンポジターで使用できるように、`0x1`します。
* 表示は、Windows コンポジターでのみ使用される場合、これを 0x0 に設定する必要があります。

バージョンで`0x1`と`0x2`VSDB このは、この値に設定が常に`0x0`します。

### <a name="display-product-primary-use-case-5-bits"></a>製品の主なユース ケース 5 のビットを表示します。

ディスプレイ デバイスの主な用途します。

* テスト装置- `0x1`
* 汎用的な表示: `0x2`
* テレビの表示: `0x3`
* デスクトップ生産性表示: `0x4`
* デスクトップ ゲームの表示: `0x5`
* プレゼンテーションの表示- `0x6`
* Virtual reality ヘッドセット- `0x7`
* 拡張現実は- `0x8`
* ビデオの壁の表示: `0x10`
* 医療のイメージングの表示: `0x11`
* 専用ゲームの表示: `0x12`
* ビデオ モニターの表示 - 専用 `0x13`
* アクセサリの表示: `0x14`

### <a name="containerid-16-bytes"></a>ContainerID [16 バイト]

16 バイト ユニバーサル一意の識別子の各デバイスに一意であります。 これは、工場でに書き込まれる識別子です。 

## <a name="remarks"></a>コメント

以前のオペレーティング システムとの最大限の互換性を維持するために勧め HMDs がバージョンを使用し続けることに注意してください。`0x1`と`0x2`この EDID 拡張機能の。 HMDs に使用する値を指定のバージョンでは、前のセクションを参照してください。
